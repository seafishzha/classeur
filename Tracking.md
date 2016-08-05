<h1 id="single-tracking-paper-and-codes">Single Tracking Paper and Codes</h1>
<p>[TOC]</p>
<h2 id="survey"><strong>Survey</strong></h2>
<h3 id="understanding-and-diagnosing-visual-tracking-systems-iccv2015">Understanding and Diagnosing Visual Tracking Systems (ICCV2015)</h3>
<pre><code>Naiyan Wangy Jianping Shiz Dit-Yan Yeungy Jiaya Jia
</code></pre>
<blockquote>
<p><strong>Contributions:</strong> a framework by breaking a tracker down into five constituent parts, namely,</p>
<ul>
<li>motion model,</li>
<li>feature extractor,</li>
<li>observation model,</li>
<li>model updater,</li>
<li>ensemble post-processor.</li>
</ul>
</blockquote>
<blockquote>
<p><strong>Findings:</strong></p>
<ul>
<li>the <strong>feature extractor</strong> plays the most important role in a tracker.</li>
<li><strong>observation model</strong> brings no significant improvement.</li>
<li>the <strong>motion model</strong> and <strong>model updater</strong> could affect the result.</li>
<li>the <strong>ensemble post-processor</strong> can improve the result<br>
substantially when the constituent trackers have high <strong>diversity</strong>.</li>
</ul>
</blockquote>
<blockquote>
<p><strong>Dataset</strong></p>
</blockquote>
<table>
<thead>
<tr>
<th>Dataset</th>
<th>Year</th>
<th>Videos</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>VTB1.0</strong> [39]</td>
<td>2013</td>
<td>50</td>
</tr>
<tr>
<td>VTB2.0 [40]</td>
<td>2015</td>
<td>100</td>
</tr>
<tr>
<td>VOT2014</td>
<td>2014</td>
<td>25</td>
</tr>
<tr>
<td>VOT2015</td>
<td>2015</td>
<td>30</td>
</tr>
<tr>
<td><strong>VOT2016</strong></td>
<td>2016</td>
<td>60</td>
</tr>
<tr>
<td>NUS-PRO [19]</td>
<td>2015</td>
<td>365</td>
</tr>
<tr>
<td>PTB [29]</td>
<td>2013</td>
<td>100</td>
</tr>
<tr>
<td>ALOV++ [28]</td>
<td>2013</td>
<td>314</td>
</tr>
</tbody>
</table>
<p><img src="http://winsty.net/diagnose/pipeline.png" alt="enter image description here"></p>
<blockquote>
<p><strong>Feature Extractor</strong><br>
The feature extractor is the most important component of a tracker. Using proper features can dramatically improve the tracking performance. Developing a good and effective feature representation for tracking is still an open problem.</p>
</blockquote>
<blockquote>
<p><strong>Observation Model</strong><br>
Different observation models indeed affect the performance when the features are weak. However, the performance gaps diminish when the features are strong enough. Consequently, satisfactory results can be obtained even using simple classifiers from textbooks.</p>
<p><strong>Motion Model</strong><br>
When compared to the feature extractor and observation model components, in general the motion model only has minor effects on the performance.  However, under scale variation and fast motion, setting the parameters properly is still crucial to obtaining good performance. Furthermore, for some specific scenarios such as egocentric video, it is beneficial to design the motion model carefully. Due to its ability to adapt to scale changes which are not uncommon in practice, we will still take the particle filter approach with resized input as the default motion model in the sequel.</p>
</blockquote>
<blockquote>
<p><strong>Model Updater</strong><br>
Although implementation of the model updater is often treated as engineering tricks in papers especially for discriminative trackers, their impact on  performance is usually very significant and hence is worth studying. Unfortunately, very few work focuses on this component.</p>
</blockquote>
<blockquote>
<p><strong>Ensemble Postprocessor</strong><br>
The ensemble post-processor can improve the performance substantially especially when the trackers have high diversity. This component is universal and effective yet it is least explored.</p>
<p><strong>Matlab Codes:</strong></p>
</blockquote>
<blockquote>
<p>运行函数:<code>run_individual</code><br>
运行函数:<code>run_individual</code></p>
<ol>
<li>设置参数（globalParam ）；</li>
<li>读取数据（图像序列）；</li>
<li>获得目标的真实状态；</li>
<li>draw results图。</li>
</ol>
</blockquote>
<pre class=" language-matlab"><code class="prism  language-matlab">
<span class="token comment" spellcheck="true">% step0: parameters setting</span>
globalParam <span class="token operator">=</span> <span class="token function">struct</span><span class="token punctuation">(</span><span class="token punctuation">...</span>
    <span class="token string">'MotionModel'</span><span class="token punctuation">,</span>                  <span class="token operator">@</span>ParticleFilterMotionModel<span class="token punctuation">,</span> <span class="token punctuation">...</span>
    <span class="token string">'FeatureExtractor'</span><span class="token punctuation">,</span>             <span class="token operator">@</span>HogRawPixelNormExtractor<span class="token punctuation">,</span> <span class="token punctuation">...</span>
    <span class="token string">'ConfidenceJudger'</span><span class="token punctuation">,</span>             <span class="token operator">@</span>ClassificationScoreJudger<span class="token punctuation">,</span> <span class="token punctuation">...</span>
    <span class="token string">'ObservationModelTrain'</span><span class="token punctuation">,</span>        <span class="token operator">@</span>LogisticRegressionTrain<span class="token punctuation">,</span> <span class="token punctuation">...</span>
    <span class="token string">'ObservationModelTest'</span><span class="token punctuation">,</span>         <span class="token operator">@</span>LogisticRegressionTest<span class="token punctuation">,</span> <span class="token punctuation">...</span>
    <span class="token string">'NegSampler'</span><span class="token punctuation">,</span>                   <span class="token operator">@</span>NegSlidingWindowSampler<span class="token punctuation">,</span> <span class="token punctuation">...</span>
    <span class="token string">'PosSampler'</span><span class="token punctuation">,</span>                   <span class="token operator">@</span>PosSlidingWindowSampler <span class="token punctuation">...</span> 
<span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<pre class=" language-matlab"><code class="prism  language-matlab"><span class="token comment" spellcheck="true">% step1.1: load data</span>
dataPath <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token string">'E:\Data\OTB2013\dataset\'</span><span class="token punctuation">,</span> name<span class="token punctuation">]</span><span class="token punctuation">;</span>
fullPath <span class="token operator">=</span> <span class="token punctuation">[</span>dataPath<span class="token punctuation">,</span> <span class="token string">'/img/'</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
d <span class="token operator">=</span> <span class="token function">dir</span><span class="token punctuation">(</span><span class="token punctuation">[</span>fullPath<span class="token punctuation">,</span> <span class="token string">'*.jpg'</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token keyword">if</span> <span class="token function">size</span><span class="token punctuation">(</span>d<span class="token punctuation">,</span> <span class="token number">1</span><span class="token punctuation">)</span> <span class="token operator">==</span> <span class="token number">0</span>
    d <span class="token operator">=</span> <span class="token function">dir</span><span class="token punctuation">(</span><span class="token punctuation">[</span>fullPath<span class="token punctuation">,</span> <span class="token string">'*.png'</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token keyword">end</span>
<span class="token keyword">if</span> <span class="token function">size</span><span class="token punctuation">(</span>d<span class="token punctuation">,</span> <span class="token number">1</span><span class="token punctuation">)</span> <span class="token operator">==</span> <span class="token number">0</span>
    d <span class="token operator">=</span> <span class="token function">dir</span><span class="token punctuation">(</span><span class="token punctuation">[</span>fullPath<span class="token punctuation">,</span> <span class="token string">'*.bmp'</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token keyword">end</span>

<span class="token comment" spellcheck="true">% step1.2: groundtruth</span>
<span class="token keyword">if</span> <span class="token function">strcmp</span><span class="token punctuation">(</span>name<span class="token punctuation">,</span> <span class="token string">'Jogging'</span><span class="token punctuation">)</span> <span class="token operator">==</span> <span class="token number">0</span>
    rects <span class="token operator">=</span> <span class="token function">importdata</span><span class="token punctuation">(</span><span class="token punctuation">[</span>dataPath<span class="token punctuation">,</span> <span class="token string">'/groundtruth_rect.txt'</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token keyword">else</span>
    rects <span class="token operator">=</span> <span class="token function">importdata</span><span class="token punctuation">(</span><span class="token punctuation">[</span>dataPath<span class="token punctuation">,</span> <span class="token string">'/groundtruth_rect.2.txt'</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token keyword">end</span>

<span class="token comment" spellcheck="true">% call main function</span>
results <span class="token operator">=</span> <span class="token function">run_Diagnose</span><span class="token punctuation">(</span>seq<span class="token punctuation">,</span> res_path<span class="token punctuation">,</span> bSaveImage<span class="token punctuation">)</span>

</code></pre>
<pre class=" language-matlab"><code class="prism  language-matlab"><span class="token comment" spellcheck="true">% Step2: initialization（初始化）</span>
	 <span class="token keyword">if</span> <span class="token punctuation">(</span>frame <span class="token operator">==</span> <span class="token number">1</span><span class="token punctuation">)</span> 
            tmplPos <span class="token operator">=</span> globalParam<span class="token punctuation">.</span><span class="token function">PosSampler</span><span class="token punctuation">(</span>p<span class="token punctuation">,</span> seq<span class="token punctuation">.</span>opt<span class="token punctuation">)</span><span class="token punctuation">;</span>
            tmplNeg <span class="token operator">=</span> globalParam<span class="token punctuation">.</span><span class="token function">NegSampler</span><span class="token punctuation">(</span>p<span class="token punctuation">,</span> seq<span class="token punctuation">.</span>opt<span class="token punctuation">)</span><span class="token punctuation">;</span>
            <span class="token punctuation">[</span>dataPos<span class="token punctuation">,</span> seq<span class="token punctuation">.</span>opt<span class="token punctuation">]</span> <span class="token operator">=</span> globalParam<span class="token punctuation">.</span><span class="token function">FeatureExtractor</span><span class="token punctuation">(</span>frame<span class="token punctuation">,</span> tmplPos<span class="token punctuation">,</span> seq<span class="token punctuation">.</span>opt<span class="token punctuation">)</span><span class="token punctuation">;</span>
            <span class="token punctuation">[</span>dataNeg<span class="token punctuation">,</span> seq<span class="token punctuation">.</span>opt<span class="token punctuation">]</span> <span class="token operator">=</span> globalParam<span class="token punctuation">.</span><span class="token function">FeatureExtractor</span><span class="token punctuation">(</span>frame<span class="token punctuation">,</span> tmplNeg<span class="token punctuation">,</span> seq<span class="token punctuation">.</span>opt<span class="token punctuation">)</span><span class="token punctuation">;</span>
            model   <span class="token operator">=</span> globalParam<span class="token punctuation">.</span><span class="token function">ObservationModelTrain</span><span class="token punctuation">(</span>dataPos<span class="token punctuation">,</span> dataNeg<span class="token punctuation">,</span> seq<span class="token punctuation">.</span>opt<span class="token punctuation">)</span><span class="token punctuation">;</span>  
            <span class="token keyword">if</span> <span class="token punctuation">(</span>seq<span class="token punctuation">.</span>opt<span class="token punctuation">.</span>useFirstFrame<span class="token punctuation">)</span>
                <span class="token function">assert</span><span class="token punctuation">(</span><span class="token operator">~</span><span class="token function">strcmp</span><span class="token punctuation">(</span><span class="token function">func2str</span><span class="token punctuation">(</span>globalParam<span class="token punctuation">.</span>ObservationModelTrain<span class="token punctuation">)</span><span class="token punctuation">,</span> <span class="token string">'SOSVMTrain'</span><span class="token punctuation">)</span><span class="token punctuation">,</span> <span class="token punctuation">...</span>
                    <span class="token string">'SOSVM does not support useFirstFrame option!!'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
                dataPosFirstFrame <span class="token operator">=</span> dataPos<span class="token punctuation">;</span>
            <span class="token keyword">end</span>

	<span class="token keyword">end</span>


<span class="token comment" spellcheck="true">% Step3: tracking(跟踪)</span>
<span class="token keyword">if</span> <span class="token punctuation">(</span>f <span class="token operator">~=</span> <span class="token number">1</span><span class="token punctuation">)</span>
            tmpl    <span class="token operator">=</span> globalParam<span class="token punctuation">.</span><span class="token function">MotionModel</span><span class="token punctuation">(</span>tmpl<span class="token punctuation">,</span> prob<span class="token punctuation">,</span> seq<span class="token punctuation">.</span>opt<span class="token punctuation">)</span><span class="token punctuation">;</span>
            <span class="token punctuation">[</span>feat<span class="token punctuation">,</span> seq<span class="token punctuation">.</span>opt<span class="token punctuation">]</span> <span class="token operator">=</span> globalParam<span class="token punctuation">.</span><span class="token function">FeatureExtractor</span><span class="token punctuation">(</span>frame<span class="token punctuation">,</span> tmpl<span class="token punctuation">,</span> seq<span class="token punctuation">.</span>opt<span class="token punctuation">)</span><span class="token punctuation">;</span>
            prob    <span class="token operator">=</span> globalParam<span class="token punctuation">.</span><span class="token function">ObservationModelTest</span><span class="token punctuation">(</span>feat<span class="token punctuation">,</span> model<span class="token punctuation">)</span><span class="token punctuation">;</span>    
            
            <span class="token punctuation">[</span>maxProb<span class="token punctuation">,</span> maxIdx<span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token function">max</span><span class="token punctuation">(</span>prob<span class="token punctuation">)</span><span class="token punctuation">;</span> 
            p <span class="token operator">=</span> <span class="token function">tmpl</span><span class="token punctuation">(</span>maxIdx<span class="token punctuation">,</span> <span class="token operator">:</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
            model<span class="token punctuation">.</span>lastOutput <span class="token operator">=</span> p<span class="token punctuation">;</span>
            model<span class="token punctuation">.</span>lastProb <span class="token operator">=</span> maxProb<span class="token punctuation">;</span>
            <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token function">strcmp</span><span class="token punctuation">(</span><span class="token function">func2str</span><span class="token punctuation">(</span>globalParam<span class="token punctuation">.</span>ConfidenceJudger<span class="token punctuation">)</span><span class="token punctuation">,</span> <span class="token string">'UpdateDifferenceJudger'</span><span class="token punctuation">)</span><span class="token punctuation">)</span>
                w1 <span class="token operator">=</span> <span class="token function">max</span><span class="token punctuation">(</span><span class="token function">round</span><span class="token punctuation">(</span><span class="token function">tmpl</span><span class="token punctuation">(</span><span class="token operator">:</span><span class="token punctuation">,</span> <span class="token number">1</span><span class="token punctuation">)</span> <span class="token operator">-</span> <span class="token function">tmpl</span><span class="token punctuation">(</span><span class="token operator">:</span><span class="token punctuation">,</span> <span class="token number">3</span><span class="token punctuation">)</span> <span class="token operator">/</span> <span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">,</span> <span class="token function">round</span><span class="token punctuation">(</span><span class="token function">p</span><span class="token punctuation">(</span><span class="token operator">:</span><span class="token punctuation">,</span> <span class="token number">1</span><span class="token punctuation">)</span> <span class="token operator">-</span> <span class="token function">p</span><span class="token punctuation">(</span><span class="token operator">:</span><span class="token punctuation">,</span> <span class="token number">3</span><span class="token punctuation">)</span> <span class="token operator">/</span> <span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
                w2 <span class="token operator">=</span> <span class="token function">min</span><span class="token punctuation">(</span><span class="token function">round</span><span class="token punctuation">(</span><span class="token function">tmpl</span><span class="token punctuation">(</span><span class="token operator">:</span><span class="token punctuation">,</span> <span class="token number">1</span><span class="token punctuation">)</span> <span class="token operator">+</span> <span class="token function">tmpl</span><span class="token punctuation">(</span><span class="token operator">:</span><span class="token punctuation">,</span> <span class="token number">3</span><span class="token punctuation">)</span> <span class="token operator">/</span> <span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">,</span> <span class="token function">round</span><span class="token punctuation">(</span><span class="token function">p</span><span class="token punctuation">(</span><span class="token operator">:</span><span class="token punctuation">,</span> <span class="token number">1</span><span class="token punctuation">)</span> <span class="token operator">+</span> <span class="token function">p</span><span class="token punctuation">(</span><span class="token operator">:</span><span class="token punctuation">,</span> <span class="token number">3</span><span class="token punctuation">)</span> <span class="token operator">/</span> <span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
                h1 <span class="token operator">=</span> <span class="token function">max</span><span class="token punctuation">(</span><span class="token function">round</span><span class="token punctuation">(</span><span class="token function">tmpl</span><span class="token punctuation">(</span><span class="token operator">:</span><span class="token punctuation">,</span> <span class="token number">2</span><span class="token punctuation">)</span> <span class="token operator">-</span> <span class="token function">tmpl</span><span class="token punctuation">(</span><span class="token operator">:</span><span class="token punctuation">,</span> <span class="token number">4</span><span class="token punctuation">)</span> <span class="token operator">/</span> <span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">,</span> <span class="token function">round</span><span class="token punctuation">(</span><span class="token function">p</span><span class="token punctuation">(</span><span class="token operator">:</span><span class="token punctuation">,</span> <span class="token number">2</span><span class="token punctuation">)</span> <span class="token operator">-</span> <span class="token function">p</span><span class="token punctuation">(</span><span class="token operator">:</span><span class="token punctuation">,</span> <span class="token number">4</span><span class="token punctuation">)</span> <span class="token operator">/</span> <span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
                h2 <span class="token operator">=</span> <span class="token function">min</span><span class="token punctuation">(</span><span class="token function">round</span><span class="token punctuation">(</span><span class="token function">tmpl</span><span class="token punctuation">(</span><span class="token operator">:</span><span class="token punctuation">,</span> <span class="token number">2</span><span class="token punctuation">)</span> <span class="token operator">+</span> <span class="token function">tmpl</span><span class="token punctuation">(</span><span class="token operator">:</span><span class="token punctuation">,</span> <span class="token number">4</span><span class="token punctuation">)</span> <span class="token operator">/</span> <span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">,</span> <span class="token function">round</span><span class="token punctuation">(</span><span class="token function">p</span><span class="token punctuation">(</span><span class="token operator">:</span><span class="token punctuation">,</span> <span class="token number">2</span><span class="token punctuation">)</span> <span class="token operator">+</span> <span class="token function">p</span><span class="token punctuation">(</span><span class="token operator">:</span><span class="token punctuation">,</span> <span class="token number">4</span><span class="token punctuation">)</span> <span class="token operator">/</span> <span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
                interArea <span class="token operator">=</span> <span class="token function">max</span><span class="token punctuation">(</span>w2 <span class="token operator">-</span> w1<span class="token punctuation">,</span> <span class="token number">0</span><span class="token punctuation">)</span> <span class="token operator">.*</span> <span class="token function">max</span><span class="token punctuation">(</span>h2 <span class="token operator">-</span> h1<span class="token punctuation">,</span> <span class="token number">0</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
                jointArea <span class="token operator">=</span> <span class="token punctuation">(</span><span class="token function">round</span><span class="token punctuation">(</span><span class="token function">tmpl</span><span class="token punctuation">(</span><span class="token operator">:</span><span class="token punctuation">,</span> <span class="token number">3</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token operator">.*</span> <span class="token function">round</span><span class="token punctuation">(</span><span class="token function">tmpl</span><span class="token punctuation">(</span><span class="token operator">:</span><span class="token punctuation">,</span> <span class="token number">4</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token operator">+</span> <span class="token function">round</span><span class="token punctuation">(</span><span class="token function">p</span><span class="token punctuation">(</span><span class="token number">3</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token operator">*</span> <span class="token function">round</span><span class="token punctuation">(</span><span class="token function">p</span><span class="token punctuation">(</span><span class="token number">4</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token operator">-</span> interArea<span class="token punctuation">;</span>
                overlapRatio <span class="token operator">=</span> interArea <span class="token operator">./</span> jointArea<span class="token punctuation">;</span>
                idx <span class="token operator">=</span> <span class="token punctuation">(</span>overlapRatio <span class="token operator">&lt;</span> seq<span class="token punctuation">.</span>opt<span class="token punctuation">.</span>UpdateDifferenceJudger<span class="token punctuation">.</span>overlap<span class="token punctuation">)</span><span class="token punctuation">;</span>
                model<span class="token punctuation">.</span>secondProb <span class="token operator">=</span> <span class="token function">max</span><span class="token punctuation">(</span><span class="token function">prob</span><span class="token punctuation">(</span>idx<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
            <span class="token keyword">end</span>
        <span class="token keyword">end</span>


<span class="token comment" spellcheck="true">%step4: updating(更新)</span>

            <span class="token keyword">if</span> <span class="token punctuation">(</span>globalParam<span class="token punctuation">.</span><span class="token function">ConfidenceJudger</span><span class="token punctuation">(</span>model<span class="token punctuation">,</span> seq<span class="token punctuation">.</span>opt<span class="token punctuation">)</span><span class="token punctuation">)</span>
                tmplPos <span class="token operator">=</span> globalParam<span class="token punctuation">.</span><span class="token function">PosSampler</span><span class="token punctuation">(</span>p<span class="token punctuation">,</span> seq<span class="token punctuation">.</span>opt<span class="token punctuation">)</span><span class="token punctuation">;</span>
                tmplNeg <span class="token operator">=</span> globalParam<span class="token punctuation">.</span><span class="token function">NegSampler</span><span class="token punctuation">(</span>p<span class="token punctuation">,</span> seq<span class="token punctuation">.</span>opt<span class="token punctuation">)</span><span class="token punctuation">;</span>
                <span class="token punctuation">[</span>dataPos<span class="token punctuation">,</span> seq<span class="token punctuation">.</span>opt<span class="token punctuation">]</span> <span class="token operator">=</span> globalParam<span class="token punctuation">.</span><span class="token function">FeatureExtractor</span><span class="token punctuation">(</span>frame<span class="token punctuation">,</span> tmplPos<span class="token punctuation">,</span> seq<span class="token punctuation">.</span>opt<span class="token punctuation">)</span><span class="token punctuation">;</span>
                <span class="token punctuation">[</span>dataNeg<span class="token punctuation">,</span> seq<span class="token punctuation">.</span>opt<span class="token punctuation">]</span> <span class="token operator">=</span> globalParam<span class="token punctuation">.</span><span class="token function">FeatureExtractor</span><span class="token punctuation">(</span>frame<span class="token punctuation">,</span> tmplNeg<span class="token punctuation">,</span> seq<span class="token punctuation">.</span>opt<span class="token punctuation">)</span><span class="token punctuation">;</span>
                <span class="token keyword">if</span> <span class="token punctuation">(</span>seq<span class="token punctuation">.</span>opt<span class="token punctuation">.</span>useFirstFrame<span class="token punctuation">)</span>
                    dataPos<span class="token punctuation">.</span>feat <span class="token operator">=</span> <span class="token punctuation">[</span>dataPosFirstFrame<span class="token punctuation">.</span>feat<span class="token punctuation">,</span> dataPos<span class="token punctuation">.</span>feat<span class="token punctuation">]</span><span class="token punctuation">;</span>
                    dataPos<span class="token punctuation">.</span>tmpl <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token function">zeros</span><span class="token punctuation">(</span><span class="token function">size</span><span class="token punctuation">(</span>dataPosFirstFrame<span class="token punctuation">.</span>tmpl<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span> dataPos<span class="token punctuation">.</span>tmpl<span class="token punctuation">]</span><span class="token punctuation">;</span>
                <span class="token keyword">end</span>
                model   <span class="token operator">=</span> globalParam<span class="token punctuation">.</span><span class="token function">ObservationModelTrain</span><span class="token punctuation">(</span>dataPos<span class="token punctuation">,</span> dataNeg<span class="token punctuation">,</span> seq<span class="token punctuation">.</span>opt<span class="token punctuation">,</span> model<span class="token punctuation">)</span><span class="token punctuation">;</span>  
            <span class="token keyword">end</span>

</code></pre>
<h2 id="kernel-correlation-filter-tracking">Kernel Correlation Filter Tracking</h2>
<h3 id="deformable-parts-correlation-filters-for-robust-visual-trackingcvpr2016">Deformable Parts Correlation Filters for Robust Visual Tracking(CVPR2016)</h3>
<p>Alan Lukežič, Luka Čehovin, Matej Kristan<br>
针对非刚性和遮挡物体的跟踪问题，首先利用基于颜色的KCF获取目标的初略位置，然后利用中层的patches，分别做KCF，通过最小化能量函数（由各个patches构造），精确定位目标的位置。</p>
<h3 id="staple-complementary-learners-for-real-time-tracking">Staple: Complementary Learners for Real-Time Tracking</h3>
<p>Luca Bertinetto, Jack Valmadre, Stuart Golodetz, Ondrej Miksik, Philip H.S. Torr<br>
<img src="http://www.robots.ox.ac.uk/~luca/stuff/pipeline_horizontal.png" alt=""></p>
<p>discrator + HOG</p>
<p>Matlab Code: <a href="https://github.com/bertinetto/staple">github</a></p>
<hr>
<h3 id="beyond-correlation-filters-learning-continuous-convolution-operators-for-visual-trackingeccv16">Beyond Correlation Filters: Learning Continuous Convolution Operators for Visual Tracking(ECCV16)</h3>
<ul>
<li>ompage:<a href="http://www.cvl.isy.liu.se/research/objrec/visualtracking/conttrack/index.html">http://www.cvl.isy.liu.se/research/objrec/visualtracking/conttrack/index.html</a></li>
<li>code: to coming</li>
<li>performance:
<ul>
<li>OTB-2015 (+5.1% in mean OP),</li>
<li>Temple-Color (+4.6% in mean OP)</li>
<li>VOT2015 (20% relative reduction in failure rate).</li>
</ul>
</li>
<li>speed:</li>
<li>method:   fusion Deep Features ( magenet-vgg-m-2048 ) for tracking<br>
<img src="http://www.cvl.isy.liu.se/research/objrec/visualtracking/conttrack/method_fig.jpg" alt=""></li>
</ul>
<h2 id="template----sparse"><strong>Template  +  Sparse</strong></h2>
<h3 id="least-soft-threshold-squares-tracking">Least Soft-threshold Squares Tracking</h3>
<p>Dong Wang, Huchuan Lu, and Ming-Hsuan Yang<br>
IEEE Conference on Computer Vision and Pattern Recognition (CVPR 2013), pp. 2371-2378, Portland, June, 2013.<br>
<a href="http://faculty.ucmerced.edu/mhyang/project/cvpr13_lss/LSST-MatlabCode-V1.zip">Matlab</a></p>
<h3 id="robust-object-tracking-via-sparsity-based-collaborative-model">Robust Object Tracking via Sparsity-based Collaborative Model</h3>
<p>Wei Zhong, Huchuan Lu, and Ming-Hsuan Yang<br>
IEEE Conference on Computer Vision and Pattern Recognition (CVPR 2012), pp. 1838-1845, Providence, June, 2012.<br>
<a href="http://faculty.ucmerced.edu/mhyang/project/cvpr12_scm.htm">Matlab</a></p>
<h3 id="visual-tracking-via-adaptive-structural-local-sparse-appearance-model">Visual Tracking via Adaptive Structural Local Sparse Appearance Model</h3>
<p>Xu Jia, Huchuan Lu, and Ming-Hsuan Yang<br>
IEEE Conference on Computer Vision and Pattern Recognition (CVPR 2012), pp. 1822-1829, Providence, June, 2012<br>
<a href="http://faculty.ucmerced.edu/mhyang/project/cvpr12_jia_project.htm">Matlab</a></p>
<h3 id="online-discriminative-object-tracking-with-local-sparse-representation">Online Discriminative Object Tracking with Local Sparse Representation</h3>
<p>Qing Wang, Feng Chen, Wenli Xu, and Ming-Hsuan Yang<br>
IEEE Workshop on Applications of Computer Vision (WACV 2012), pp. 425-432, Breckenridge, January, 2012.<br>
<a href="http://faculty.ucmerced.edu/mhyang/code/wacv12a_code.zip">Matlab</a></p>
<h2 id="patch--nn"><strong>Patch + NN</strong></h2>
<h3 id="best-buddies-similarity-for-robust-template-matching-pdf-bib">Best Buddies Similarity for Robust Template Matching PDF BIB</h3>
<p>Tali Dekel*, Shaul Oron*, Michael Rubinstein, Shai Avidan, William T. Freeman<br>
Computer Vision and Pattern Recognition, 2015<br>
<a href="http://www.eng.tau.ac.il/~oron/BBS/BBS.html">Project</a><br>
<a href="http://www.eng.tau.ac.il/~oron/BBS/BBS_code_and_data_release_v1.0.zip">Matlab</a></p>
<h3 id="approximate-nearest-neighbor-fields-in-video">Approximate Nearest Neighbor Fields in Video</h3>
<p>Nir Ben-Zrihem and Lihi Zelnik-Manor,CVPR 2015.<br>
<a href="http://cgm.technion.ac.il/Computer-Graphics-Multimedia/Software/RIANN/">Project</a><br>
<a href="http://cgm.technion.ac.il/Computer-Graphics-Multimedia/Software/RIANN/resources/RIANN-LOCAL-Code.zip">Matlab</a></p>
<h3 id="learning-to-compare-image-patches-via-convolutional-neural-networks">Learning to Compare Image Patches via Convolutional Neural Networks</h3>
<p>S. Zagoruyko, N. Komodakis<br>
In CVPR 2015.<br>
<a href="https://github.com/szagoruyko/cvpr15deepcompare">Project page with source code (Torch, Matlab, C++) and trained models</a></p>
<h3 id="visual-tracking-using-pertinent-patch-selection-and-masking">Visual Tracking Using Pertinent Patch Selection and Masking</h3>
<p>Dae-Youn Lee, Jae-Young Sim, and Chang-Su Kim<br>
International Conference on Computer Vision and Pattern Recognition (CVPR), 2014<br>
<a href="http://mcl.korea.ac.kr/dylee_cvpr2014/">Projcet</a><br>
<a href="http://mcl.korea.ac.kr/~inomi/CVPR2014/PPTv1.zip">OpenCV</a></p>
<h2 id="color----histogram"><strong>Color  +  Histogram</strong></h2>
<h3 id="in-defense-of-color-based-model-free-tracking">In Defense of Color-based Model-free Tracking</h3>
<p>Horst Possegger, Thomas Mauthner, and Horst Bischof<br>
In Proc. IEEE Conference on Computer Vision and Pattern Recognition (CVPR), 2015<br>
<a href="http://lrs.icg.tugraz.at/downloads/dat-v1.0.zip">Matlab</a></p>
<h3 id="visual-tracking-via-locality-sensitive-histograms">Visual Tracking via Locality Sensitive Histograms</h3>
<p>Shengfeng He, Qingxiong Yang, Rynson Lau, Jiang Wang, and Ming-Hsuan Yang<br>
IEEE Conference on Computer Vision and Pattern Recognition (CVPR 2013), pp. 2427-2434, Portland, June, 2013.<br>
<a href="http://www.cs.cityu.edu.hk/~shengfehe2/visual-tracking-via-locality-sensitive-histograms.html">Matlab</a></p>
<h3 id="dirichlet-based-histogram-feature-transform-for-image-classification">Dirichlet-based Histogram Feature Transform for Image Classification,</h3>
<p>T. Kobayashi,<br>
Proc. IEEE Conference on Computer Vision and Pattern Recognition (CVPR), pp. 3278-3285, 2014. pdf  <a href="https://staff.aist.go.jp/takumi.kobayashi/codes.html#DirFT">code</a></p>
<h2 id="motion--context"><strong>Motion + Context</strong></h2>
<h3 id="robust-online-learned-spatio-temporal-context-model-for-visual-tracking">Robust Online Learned Spatio-Temporal Context Model for Visual Tracking,</h3>
<p>Longyin Wen, Zhaowei Cai, Zhen Lei, Dong Yi, Stan Z. Li.<br>
IEEE Transaction on Image Processing (TIP), 2014<br>
<a href="http://www.cbsr.ia.ac.cn/users/lywen/codes/STTracker_v1.0.zip">C++</a></p>
<h3 id="robust-deformable-and-occluded-object-tracking-with-dynamic-graph">Robust Deformable and Occluded Object Tracking with Dynamic Graph,</h3>
<p>Zhaowei Cai, Longyin Wen, Zhen Lei, Nuno Vasconcelos, Stan Z. Li.<br>
IEEE Transaction on Image Processing (TIP), 2014<br>
<a href="http://www.cbsr.ia.ac.cn/users/lywen/codes/DGT_v2.1.zip">C++</a></p>
<h3 id="extended-lucas-kanade-tracking">Extended Lucas-Kanade Tracking</h3>
<p>Shaul Oron, Aharon Bar-Hillel, Shai Avidan<br>
European Conference on Computer Vision, 2014<br>
<a href="http://www.eng.tau.ac.il/~oron/ELK/ELK.html">Project</a><br>
<a href="http://www.eng.tau.ac.il/~oron/ELK/ELK_source.zip">Matlab</a></p>
<h2 id="patch--boosting"><strong>Patch + Boosting</strong></h2>
<h3 id="real-time-compressive-tracking">Real-Time Compressive Tracking</h3>
<p>Kaihua Zhang, Lei Zhang, and Ming-Hsuan Yang<br>
European Conference on Computer Vision (ECCV 2012), vol. 3, pp. 864-877, Florence, Italy, October, 2012.<br>
<a href="http://www4.comp.polyu.edu.hk/~cslzhang/CT/CT.htm">Matlab</a></p>
<h3 id="online-multiple-support-instance-tracking">Online Multiple Support Instance Tracking</h3>
<p>Qiuhong Zhou, Huchuan Lu, and Ming-Hsuan Yang<br>
IEEE Conference on Automatic Face and Gesture Recognition (FG 2011), pp. 545-552, Santa Barbara, March, 2011.<br>
<a href="http://faculty.ucmerced.edu/mhyang/code/fg11_omsit.zip">Matlab</a></p>
<h3 id="online-real-time-tracking-using-a-category-to-individual-detector">Online, Real-Time Tracking using a Category-to-Individual Detector</h3>
<p>D. Hall and P. Perona<br>
ECCV 2014, Zurich, Switzerland.<br>
<a href="http://www.vision.caltech.edu/~dhall/projects/CIT/">Project</a><br>
<a href="https://github.com/dchall88/CIT">Matlab</a></p>
<h2 id="superpixel"><strong>Superpixel</strong></h2>
<h3 id="superpixel-tracking">Superpixel Tracking</h3>
<p>Shu Wang, Huchuan Lu, Fan Yang, and Ming-Hsuan Yang<br>
IEEE International Conference on Computer Vision (ICCV 2011), pp. 1323-1330, Barcelona, Spain, November, 2011.<br>
<a href="http://faculty.ucmerced.edu/mhyang/papers/iccv11a.html">Matlab</a></p>
<h3 id="pixeltrack-a-fast-adaptive-algorithm-for-tracking-non-rigid-objects">Pixeltrack: a fast adaptive algorithm for tracking non-rigid objects</h3>
<p>S. Duffner and C. Garcia,<br>
In Proceedings of ICCV, 2013<br>
<a href="http://u0016403263.user.hosting-agency.de/research_pixeltrack.html">project</a><br>
<a href="http://u0016403263.user.hosting-agency.de/data/pixeltrack_v0.1.tgz">C++ OpenCV</a></p>
<h3 id="tracking-using-multilevel-quantizations">Tracking using Multilevel Quantizations</h3>
<p>Zhibin Hong, Chaohui Wang, Xue Mei, Danil Prokhorov, and Dacheng Tao, European Conference on Comptuer Vision(ECCV) 2014, Zurich, Switzerland<br>
<a href="https://sites.google.com/site/projectmqttracker/">Project</a></p>
<h2 id="dnn"><strong>DNN</strong></h2>
<h3 id="hierarchical-convolutional-features-for-visual-tracking">Hierarchical Convolutional Features for Visual Tracking</h3>
<p>Chao Ma, Jia-Bin Huang, Xiaokang Yang, and Ming-Hsuan Yang, accepted by International Conference on Computer Vision (ICCV), 2015.<br>
<a href="https://sites.google.com/site/chaoma99/">Project</a></p>
<h3 id="learning-a-temporally-invariant-representation-for-visual-tracking">Learning A Temporally Invariant Representation for Visual Tracking</h3>
<p>Chao Ma, Xiaokang Yang, Chongyang Zhang, and Ming-Hsuan Yang,<br>
in IEEE International Conference on Image Processing (ICIP), 2015. (Top 10% Paper)<br>
<a href="https://sites.google.com/site/chaoma99/icip15_tracking">Project</a></p>
<h3 id="stct-sequentially-training-convolutional-networks-for-visual-tracking">STCT: Sequentially Training Convolutional Networks for Visual Tracking</h3>
<p>Lijun Wang, Wanli Ouyang, Xiaogang Wang, Huchuan Lu, , CVPR2016,</p>
<h3 id="tracking-with-fully-convolutional-networks">Tracking with Fully Convolutional Networks,</h3>
<p>Lijun Wang, Wanli Ouyang, Xiaogang Wang, Huchuan Lu, Visual, ICCV2015,P3119-3127</p>
<h3 id="siamese-instance-search-for-tracking">Siamese Instance Search for Tracking</h3>
<p>Ran Tao,<br>
利用深度网络学习匹配函数，直接将候选目标与第一帧的目标匹配，最大值作为跟踪结果。</p>
<h3 id="hedged-deep-tracking">Hedged Deep Tracking</h3>
<p>Yuankai Qi, Shengping Zhang, Lei Qin, Hongxun Yao, Qingming Huang, Jongwoo Lim, Ming-Hsuan Yang.<br>
<img src="https://sites.google.com/site/yuankiqi/_/rsrc/1460602884304/hdt/hdt.png" alt=""></p>
<p>对每一层的特征作KCF，然后将结果Ensemble起来，这里他是用hedged（K. Chaudhuri, Y. Freund, and D. Hsu. A parameter-free hedging algorithm. In NIPS, 2009.）的集成方法。</p>
<hr>
<h2 id="learning-by-tracking-siamese-cnn-for-robust-target-associationarxiv1604.07866">Learning by tracking: Siamese CNN for robust target association(arXiv:1604.07866)</h2>
<ul>
<li>pdf: <a href="https://arxiv.org/pdf/1604.07866v3.pdf">https://arxiv.org/pdf/1604.07866v3.pdf</a></li>
<li>method :  Siamese convolutional neural network (CNN) -&gt; gradient boosting<br>
<img src="https://arxiv.org/pdf/1604.07866v3.pdf" alt=""></li>
</ul>
<h2 id="template-update"><strong>Template Update</strong></h2>
<h3 id="real-time-tracking-with-detection-for-coping-with-view-point-change-pdf-bib">Real Time Tracking-With-Detection for Coping with View Point Change PDF BIB</h3>
<p>Shaul Oron, Aharon Bar-Hillel, Shai Avidan<br>
Machine Vision and Application (MVAP) 2015<br>
<a href="http://www.eng.tau.ac.il/~oron/TWD/TWD.html">Project</a></p>
<h3 id="scribble-tracker-a-matting-based-approach-for-robust-tracking">Scribble Tracker: A Matting-based Approach for Robust Tracking</h3>
<p>Jialue Fan    Xiaohui Shen    Ying Wu</p>
<p>Northwestern University</p>
<p>IEEE Transactions on Pattern Analysis and Machine Intelligence (TPAMI), vol.34, no.8, pp.1633-1644, August 2012</p>
<p><a href="http://users.eecs.northwestern.edu/~jfa699/webpage/scribble_tracking/index.html">Project</a></p>
<h2 id="descriptor"><strong>Descriptor</strong></h2>
<h3 id="clustering-of-static-adaptive-correspondences-for-deformable-object-tracking">Clustering of Static-Adaptive Correspondences for Deformable Object Tracking</h3>
<p>Georg Nebehay and Roman Pflugfelder<br>
Computer Vision and Pattern Recognition, 2015<br>
<a href="http://www.gnebehay.com/cmt/">Project</a><br>
<a href="http://blog.csdn.net/songrotek/article/details/47662617">计算机视觉CV 之 CMT跟踪算法分析</a><br>
<a href="https://github.com/gnebehay/CppMT">C++ </a></p>
<h3 id="better-feature-tracking-through-subspace-constraints">Better Feature Tracking Through Subspace Constraints</h3>
<p>Bryan Poling, Gilad Lerman, Arthur Szlam<br>
cvpr2014<br>
<a href="http://www.math.umn.edu/~poli0048/">C++</a></p>
<h2 id="object-proposals--svm"><strong>Object Proposals + SVM</strong></h2>
<h3 id="struck-structured-output-tracking-with-kernels">Struck: Structured output tracking with kernels,</h3>
<p>Sam Hare, Amir Saffari, Stuart Golodetz, Vibhav Vineet, Ming-Ming Cheng, Stephen L. Hicks, Philip H. S. Torr. Submitted to IEEE TPAM<br>
International Conference on Computer Vision (ICCV), 2011</p>
<h3 id="beyond-local-search">Beyond local search</h3>
<p>G. Zhu, F. Porikli, and H. Li, “Beyond local search: Tracking objects everywhere with Instance-specic proposals,” in IEEE Conference on Computer Vision and Pattern Recognition (CVPR), 2016<br>
<img src="https://static.wixstatic.com/media/482d38_9492cc3ff82c48d29c9f41abd0472e6d.jpg/v1/fill/w_247,h_101,al_c,q_80,usm_0.66_1.00_0.01/482d38_9492cc3ff82c48d29c9f41abd0472e6d.jpg" alt=""></p>
<p>本文主要是利用EdgeBox，在整个图像上对可能存在目标概率大的区域提取出来，然后利用线性SVM进行分类，判断哪些是目标。</p>
<h3 id="robust-visual-tracking-with-deep-convolutional-neural-network-based-object-proposals-on-pets">Robust Visual Tracking with Deep Convolutional Neural Network based Object Proposals on PETS</h3>
<p>G. Zhu, F. Porikli, and H. Li,<br>
<img src="https://static.wixstatic.com/media/482d38_a6691fc90ee84b6ea75de13953d2190e.jpg/v1/fill/w_247,h_106,al_c,q_80,usm_0.66_1.00_0.01/482d38_a6691fc90ee84b6ea75de13953d2190e.jpg" alt=""><br>
在VGG16提取的特征基础上，做区域提取网络（RPN），获得候选目标区域，<br>
然后利用在线结构SVM进行分类，获取目标，实现跟踪。</p>
<h3 id="adaptive-objectness-for-object-tracking.">Adaptive Objectness for Object Tracking.</h3>
<p>P. Liang, Y. Pang, C. Liao, X. Mei and H. Ling.<br>
IEEE Signal Processing Letters, in press<br>
与原始的bing学习一般物体不同，本文利用bing学习特定物体–跟踪目标，然后利用SVM进行分类和更新，实现跟踪</p>
<h2 id="others"><strong>Others</strong></h2>
<h3 id="model-free-tracking.-ieee-transactions-on-pattern-recognition">Model-Free Tracking. IEEE Transactions on Pattern Recognition</h3>
<p>L. Zhang and L.J.P. van der Maaten. Preserving Structure in and Machine Intelligence, 36(4):756-769, 2014.<br>
<a href="http://visionlab.tudelft.nl/spot">Project</a><br>
<a href="http://homepage.tudelft.nl/19j49/SPOTv1.zip">Matlab</a></p>
<h3 id="speeding-up-tracking-by-ignoring-features.">Speeding Up Tracking by Ignoring Features.</h3>
<p>L. Zhang, H. Dibeklioglu, and L.J.P. van der Maaten.  In Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition (CVPR), pages 1266-1273, 2014.<br>
<a href="http://visionlab.tudelft.nl/spot">Project</a></p>
