<h1 id="single-tracking-paper-and-codes">Single Tracking Paper and Codes</h1>
<div class="toc"><ul><li><a href="#single-tracking-paper-and-codes">Single Tracking Paper and Codes</a><ul><li><a href="#survey">Survey</a><ul><li><a href="#understanding-and-diagnosing-visual-tracking-systems-iccv2015">Understanding and Diagnosing Visual Tracking Systems (ICCV2015)</a></li></ul></li><li><a href="#kernel-correlation-filter-tracking">Kernel Correlation Filter Tracking</a></li><li><a href="#template----sparse">Template  +  Sparse</a><ul><li><a href="#least-soft-threshold-squares-tracking">Least Soft-threshold Squares Tracking</a></li><li><a href="#robust-object-tracking-via-sparsity-based-collaborative-model">Robust Object Tracking via Sparsity-based Collaborative Model</a></li><li><a href="#visual-tracking-via-adaptive-structural-local-sparse-appearance-model">Visual Tracking via Adaptive Structural Local Sparse Appearance Model</a></li><li><a href="#online-discriminative-object-tracking-with-local-sparse-representation">Online Discriminative Object Tracking with Local Sparse Representation</a></li></ul></li><li><a href="#patch--nn">Patch + NN</a><ul><li><a href="#best-buddies-similarity-for-robust-template-matching-pdf-bib">Best Buddies Similarity for Robust Template Matching PDF BIB</a></li><li><a href="#approximate-nearest-neighbor-fields-in-video">Approximate Nearest Neighbor Fields in Video</a></li><li><a href="#learning-to-compare-image-patches-via-convolutional-neural-networks">Learning to Compare Image Patches via Convolutional Neural Networks</a></li><li><a href="#visual-tracking-using-pertinent-patch-selection-and-masking">Visual Tracking Using Pertinent Patch Selection and Masking</a></li></ul></li><li><a href="#color----histogram">Color  +  Histogram</a><ul><li><a href="#in-defense-of-color-based-model-free-tracking">In Defense of Color-based Model-free Tracking</a></li><li><a href="#visual-tracking-via-locality-sensitive-histograms">Visual Tracking via Locality Sensitive Histograms</a></li><li><a href="#dirichlet-based-histogram-feature-transform-for-image-classification">Dirichlet-based Histogram Feature Transform for Image Classification,</a></li></ul></li><li><a href="#motion--context">Motion + Context</a><ul><li><a href="#robust-online-learned-spatio-temporal-context-model-for-visual-tracking">Robust Online Learned Spatio-Temporal Context Model for Visual Tracking,</a></li><li><a href="#robust-deformable-and-occluded-object-tracking-with-dynamic-graph">Robust Deformable and Occluded Object Tracking with Dynamic Graph,</a></li><li><a href="#extended-lucas-kanade-tracking">Extended Lucas-Kanade Tracking</a></li></ul></li><li><a href="#patch--boosting">Patch + Boosting</a><ul><li><a href="#real-time-compressive-tracking">Real-Time Compressive Tracking</a></li><li><a href="#online-multiple-support-instance-tracking">Online Multiple Support Instance Tracking</a></li><li><a href="#online-real-time-tracking-using-a-category-to-individual-detector">Online, Real-Time Tracking using a Category-to-Individual Detector</a></li></ul></li><li><a href="#superpixel">Superpixel</a><ul><li><a href="#superpixel-tracking">Superpixel Tracking</a></li><li><a href="#pixeltrack-a-fast-adaptive-algorithm-for-tracking-non-rigid-objects">Pixeltrack: a fast adaptive algorithm for tracking non-rigid objects</a></li><li><a href="#tracking-using-multilevel-quantizations">Tracking using Multilevel Quantizations</a></li></ul></li><li><a href="#dnn">DNN</a><ul><li><a href="#hierarchical-convolutional-features-for-visual-tracking">Hierarchical Convolutional Features for Visual Tracking</a></li><li><a href="#learning-a-temporally-invariant-representation-for-visual-tracking">Learning A Temporally Invariant Representation for Visual Tracking</a></li></ul></li><li><a href="#template-update">Template Update</a><ul><li><a href="#real-time-tracking-with-detection-for-coping-with-view-point-change-pdf-bib">Real Time Tracking-With-Detection for Coping with View Point Change PDF BIB</a></li><li><a href="#scribble-tracker-a-matting-based-approach-for-robust-tracking">Scribble Tracker: A Matting-based Approach for Robust Tracking</a></li></ul></li><li><a href="#svm">SVM</a><ul><li><a href="#struck-structured-output-tracking-with-kernels">Struck: Structured output tracking with kernels,</a></li></ul></li><li><a href="#descriptor">Descriptor</a><ul><li><a href="#clustering-of-static-adaptive-correspondences-for-deformable-object-tracking">Clustering of Static-Adaptive Correspondences for Deformable Object Tracking</a></li><li><a href="#better-feature-tracking-through-subspace-constraints">Better Feature Tracking Through Subspace Constraints</a></li></ul></li><li><a href="#others">Others</a><ul><li><a href="#model-free-tracking.-ieee-transactions-on-pattern-recognition">Model-Free Tracking. IEEE Transactions on Pattern Recognition</a></li><li><a href="#speeding-up-tracking-by-ignoring-features.">Speeding Up Tracking by Ignoring Features.</a></li></ul></li></ul></li></ul></div><h2 id="survey"><strong>Survey</strong></h2>
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
<td>VTB1.0 [39]</td>
<td>2013</td>
<td>50</td>
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
<tr>
<td>VOT2014 [18]</td>
<td>2014</td>
<td>25</td>
</tr>
<tr>
<td>VTB2.0 [40]</td>
<td>2015</td>
<td>100</td>
</tr>
<tr>
<td>NUS-PRO [19]</td>
<td>2015</td>
<td>365</td>
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
<pre class=" language-matlab"><code class="prism  language-matlab"><span class="token comment" spellcheck="true">% step0: parameters setting</span>
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
<h2 id="svm"><strong>SVM</strong></h2>
<h3 id="struck-structured-output-tracking-with-kernels">Struck: Structured output tracking with kernels,</h3>
<p>Sam Hare, Amir Saffari, Stuart Golodetz, Vibhav Vineet, Ming-Ming Cheng, Stephen L. Hicks, Philip H. S. Torr. Submitted to IEEE TPAM<br>
International Conference on Computer Vision (ICCV), 2011</p>
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
<h2 id="others"><strong>Others</strong></h2>
<h3 id="model-free-tracking.-ieee-transactions-on-pattern-recognition">Model-Free Tracking. IEEE Transactions on Pattern Recognition</h3>
<p>L. Zhang and L.J.P. van der Maaten. Preserving Structure in and Machine Intelligence, 36(4):756-769, 2014.<br>
<a href="http://visionlab.tudelft.nl/spot">Project</a><br>
<a href="http://homepage.tudelft.nl/19j49/SPOTv1.zip">Matlab</a></p>
<h3 id="speeding-up-tracking-by-ignoring-features.">Speeding Up Tracking by Ignoring Features.</h3>
<p>L. Zhang, H. Dibeklioglu, and L.J.P. van der Maaten.  In Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition (CVPR), pages 1266-1273, 2014.<br>
<a href="http://visionlab.tudelft.nl/spot">Project</a></p>