<h1 id="kernelized-correlation-filters-for-visual-tracking">Kernelized Correlation Filters for Visual Tracking</h1>
<p>yufei<br>
December 1, 2015 5:37 PM</p>
<hr>
<h2 id="kcf-exploiting-the-circulant-structure-of-tracking-by-detection-with-kernelseccv2012">KCF: Exploiting the Circulant Structure of Tracking-by-detection with Kernels(ECCV2012)</h2>
<h2 id="high-speed-tracking-with-kernelized-correlation-filterspami2015">High-Speed Tracking with Kernelized Correlation Filters(PAMI2015)</h2>
<pre><code>J. F. Henriques, R. Caseiro, P. Martins, J. Batista
</code></pre>
<p><a href="http://home.isr.uc.pt/~henriques/circulant/">Project</a></p>
<hr>
<h3 id="problem"><strong>Problem</strong></h3>
<p><img src="KernelCorrelationFilter/motivation_kcf.png" alt=""></p>
<p><strong>Observation:</strong></p>
<ul>
<li>Such sets of samples are riddled with redundancies</li>
<li>any overlapping pixels are constrained to be the same.</li>
</ul>
<hr>
<h3 id="idea"><strong>Idea</strong></h3>
<p><img src="KernelCorrelationFilter/idea_kcf.png" alt=""></p>
<p>We can diagonalize it with the <em>Discrete Fourier Transform</em>, reducing both storage and computation by several orders of magnitude.</p>
<hr>
<h3 id="method"><strong>Method:</strong></h3>
<blockquote>
<p>KCF=ridge regression + Circulant data</p>
</blockquote>
<p><strong>ridge regression</strong><br>
<script type="math/tex; mode=display" id="MathJax-Element-133">
\min_\mathbb w \sum_i(f(\mathbb x_i) -y_i)^2+\lambda ||\mathbb w||^2
</script><br>
<script type="math/tex; mode=display" id="MathJax-Element-134">
\mathbb w =(X^TX + \lambda I)^{-1}X^Ty
</script></p>
<p><strong>Circulant data</strong><br>
<script type="math/tex; mode=display" id="MathJax-Element-135">
C(u)v= \mathcal F^{-1}(\mathcal F(u)\odot\mathcal F(v))
</script></p>
<blockquote>
<p><strong>卷积定理：空域卷积  ==  频域乘积</strong></p>
</blockquote>
<hr>
<p><strong>1. 卷积定理</strong></p>
<p>Given: $<script type="math/tex; mode=display" id="MathJax-Element-136">\mathbf x = [x_1,x_2,x_3]</script>$, $<script type="math/tex; mode=display" id="MathJax-Element-137">\mathbf x' = [x'_1,x'_2,x'_3]</script>$</p>
<p><script type="math/tex; mode=display" id="MathJax-Element-138">
corr(\mathbf x, \mathbf x')  = \mathcal F(\mathbf x)\odot \mathcal F(\mathbf x')
</script></p>
<table>
<thead>
<tr>
<th>0</th>
<th><script type="math/tex" id="MathJax-Element-139">x'_1</script></th>
<th><script type="math/tex" id="MathJax-Element-140">x'_2</script></th>
<th><script type="math/tex" id="MathJax-Element-141">x'_3</script></th>
<th>0</th>
</tr>
</thead>
<tbody>
<tr>
<td>0</td>
<td><script type="math/tex" id="MathJax-Element-142">x_1</script></td>
<td><script type="math/tex" id="MathJax-Element-143">x_2</script></td>
<td><script type="math/tex" id="MathJax-Element-144">x_3</script></td>
<td>0</td>
</tr>
<tr>
<td><script type="math/tex" id="MathJax-Element-145">x_1</script></td>
<td><script type="math/tex" id="MathJax-Element-146">x_2</script></td>
<td><script type="math/tex" id="MathJax-Element-147">x_3</script></td>
<td>0</td>
<td>0</td>
</tr>
<tr>
<td><script type="math/tex" id="MathJax-Element-148">x_2</script></td>
<td><script type="math/tex" id="MathJax-Element-149">x_3</script></td>
<td>0</td>
<td>0</td>
<td><script type="math/tex" id="MathJax-Element-150">x_1</script></td>
</tr>
<tr>
<td><script type="math/tex" id="MathJax-Element-151">x_3</script></td>
<td>0</td>
<td>0</td>
<td><script type="math/tex" id="MathJax-Element-152">x_1</script></td>
<td><script type="math/tex" id="MathJax-Element-153">x_2</script></td>
</tr>
<tr>
<td>0</td>
<td>0</td>
<td><script type="math/tex" id="MathJax-Element-154">x_1</script></td>
<td><script type="math/tex" id="MathJax-Element-155">x_2</script></td>
<td><script type="math/tex" id="MathJax-Element-156">x_3</script></td>
</tr>
</tbody>
</table>
<blockquote>
<p><script type="math/tex; mode=display" id="MathJax-Element-157">
corr(\mathbf x, \mathbf y)  = \mathcal F( \tilde {\mathbf x})\odot  \mathcal F(\tilde{\mathbf y})
</script></p>
</blockquote>
<hr>
<p><strong>2. Training</strong><br>
<script type="math/tex; mode=display" id="MathJax-Element-158">
\mathcal F({\mathbf w}) = \frac{\mathcal F(\mathbf x) \odot \mathcal F(\mathbf y)}{\mathcal F(\mathbf x) \odot \mathcal F(\mathbf x) + \lambda }
</script></p>
<hr>
<p><strong>3. testing</strong><br>
<script type="math/tex; mode=display" id="MathJax-Element-159">
\mathbf y'=\mathcal F^{-1}(\mathcal F(\mathbf w) \odot \mathcal F(\mathbf x') )
</script></p>
<p><script type="math/tex; mode=display" id="MathJax-Element-160">
[p_x,p_y] = \arg \max\mathbf y'
</script></p>
<p><strong>4. Kernel</strong><br>
<script type="math/tex; mode=display" id="MathJax-Element-161">
\kappa(\mathbf x, \mathbf x') = h(||\mathbf x - \mathbf x'||^2)
=h(||\mathbf x||^2 +||\mathbf x'||^2 - 2\mathbf x^T\mathbf x' )
</script><br>
<script type="math/tex; mode=display" id="MathJax-Element-162">
=h(||\mathbf x||^2 +||\mathbf x'||^2 - 2\mathcal F^{-1} (\mathcal F({\mathbf x}) \odot \mathcal F({\mathbf x'}) )
</script></p>
<p><strong>5. kernel ridge regression</strong><br>
<script type="math/tex; mode=display" id="MathJax-Element-163">
\alpha = (\kappa+ \lambda I)^{-1}\mathbf y
</script></p>
<blockquote>
<p><strong>Solustions:</strong></p>
</blockquote>
<ul>
<li><strong>Training:</strong><br>
<script type="math/tex; mode=display" id="MathJax-Element-164">
\alpha = \mathcal F^{-1}(\frac{\mathcal F(\mathbf y)}{\mathcal F(\kappa (\mathbf x, \mathbf x)) + \lambda})
</script></li>
<li><strong>Prediction:</strong><br>
<script type="math/tex; mode=display" id="MathJax-Element-165">
\hat {\mathbf y} = \mathcal F^{-1}( \mathcal F(\kappa(\mathbf x, \mathbf x')) \odot \mathcal F(\alpha))
</script></li>
</ul>
<hr>
<h3 id="implementation">Implementation</h3>
<hr>
<p><strong>Training:</strong></p>
<ol>
<li>$\mathcal F(\mathbf y) $</li>
</ol>
<pre class=" language-matlab"><code class="prism  language-matlab">    <span class="token comment" spellcheck="true">% expected response</span>
	state<span class="token punctuation">.</span>window <span class="token operator">=</span>  <span class="token function">floor</span><span class="token punctuation">(</span>state<span class="token punctuation">.</span>size<span class="token operator">*</span><span class="token number">2.5</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
    sz <span class="token operator">=</span> <span class="token function">fliplr</span><span class="token punctuation">(</span><span class="token function">floor</span><span class="token punctuation">(</span>state<span class="token punctuation">.</span>window<span class="token operator">/</span>state<span class="token punctuation">.</span>cell_size<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	<span class="token punctuation">[</span>rs<span class="token punctuation">,</span> cs<span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token function">ndgrid</span><span class="token punctuation">(</span><span class="token punctuation">(</span><span class="token number">1</span><span class="token operator">:</span><span class="token function">sz</span><span class="token punctuation">(</span><span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token operator">-</span>  <span class="token function">bitshift</span><span class="token punctuation">(</span><span class="token function">sz</span><span class="token punctuation">(</span><span class="token number">1</span><span class="token punctuation">)</span><span class="token operator">+</span><span class="token number">1</span><span class="token punctuation">,</span><span class="token operator">-</span><span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">,</span> <span class="token punctuation">(</span><span class="token number">1</span><span class="token operator">:</span><span class="token function">sz</span><span class="token punctuation">(</span><span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token operator">-</span> <span class="token function">bitshift</span><span class="token punctuation">(</span><span class="token function">sz</span><span class="token punctuation">(</span><span class="token number">2</span><span class="token punctuation">)</span><span class="token operator">+</span><span class="token number">1</span><span class="token punctuation">,</span><span class="token operator">-</span><span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	y <span class="token operator">=</span> <span class="token function">exp</span><span class="token punctuation">(</span><span class="token operator">-</span><span class="token number">0.5</span> <span class="token operator">/</span> output_sigma<span class="token operator">^</span><span class="token number">2</span> <span class="token operator">*</span> <span class="token punctuation">(</span>rs<span class="token operator">.^</span><span class="token number">2</span> <span class="token operator">+</span> cs<span class="token operator">.^</span><span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    y <span class="token operator">=</span> <span class="token function">circshift</span><span class="token punctuation">(</span>y<span class="token punctuation">,</span> <span class="token function">bitshift</span><span class="token punctuation">(</span>sz<span class="token operator">+</span><span class="token number">2</span><span class="token punctuation">,</span><span class="token operator">-</span><span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	state<span class="token punctuation">.</span>yf <span class="token operator">=</span> <span class="token function">fft2</span><span class="token punctuation">(</span>y<span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<ol start="2">
<li><script type="math/tex" id="MathJax-Element-166">\mathcal F(\kappa(\mathbf x, \mathbf x))</script></li>
</ol>
<pre class=" language-matlab"><code class="prism  language-matlab">        x <span class="token operator">=</span> <span class="token function">get_region</span><span class="token punctuation">(</span>im<span class="token punctuation">,</span> state<span class="token punctuation">)</span><span class="token punctuation">;</span>
        x <span class="token operator">=</span> <span class="token function">double</span><span class="token punctuation">(</span><span class="token function">fhog</span><span class="token punctuation">(</span><span class="token function">single</span><span class="token punctuation">(</span>x<span class="token punctuation">)</span> <span class="token operator">/</span> <span class="token number">255</span><span class="token punctuation">,</span> state<span class="token punctuation">.</span>cell_size<span class="token punctuation">,</span><span class="token number">9</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token function">x</span><span class="token punctuation">(</span><span class="token operator">:</span><span class="token punctuation">,</span><span class="token operator">:</span><span class="token punctuation">,</span><span class="token keyword">end</span><span class="token punctuation">)</span> <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
        x <span class="token operator">=</span> <span class="token function">bsxfun</span><span class="token punctuation">(</span><span class="token operator">@</span>times<span class="token punctuation">,</span> x<span class="token punctuation">,</span> state<span class="token punctuation">.</span>cos_window<span class="token punctuation">)</span><span class="token punctuation">;</span>
        xf <span class="token operator">=</span> <span class="token function">fft2</span><span class="token punctuation">(</span>x<span class="token punctuation">)</span><span class="token punctuation">;</span>
		kf <span class="token operator">=</span> <span class="token function">dense_gauss_kernel</span><span class="token punctuation">(</span>xf<span class="token punctuation">,</span>xf<span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<pre class=" language-matlab"><code class="prism  language-matlab"><span class="token keyword">function</span> kf <span class="token operator">=</span> <span class="token function">dense_gauss_kernel</span><span class="token punctuation">(</span>xf<span class="token punctuation">,</span> yf<span class="token punctuation">)</span>	
		sigma <span class="token operator">=</span> <span class="token number">0.5</span><span class="token punctuation">;</span>
		N <span class="token operator">=</span> <span class="token function">size</span><span class="token punctuation">(</span>xf<span class="token punctuation">,</span><span class="token number">1</span><span class="token punctuation">)</span> <span class="token operator">*</span> <span class="token function">size</span><span class="token punctuation">(</span>xf<span class="token punctuation">,</span><span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
		xx <span class="token operator">=</span> <span class="token function">xf</span><span class="token punctuation">(</span><span class="token operator">:</span><span class="token punctuation">)</span><span class="token operator">'</span> <span class="token operator">*</span> <span class="token function">xf</span><span class="token punctuation">(</span><span class="token operator">:</span><span class="token punctuation">)</span> <span class="token operator">/</span> N<span class="token punctuation">;</span>  <span class="token comment" spellcheck="true">%squared norm of x</span>
		yy <span class="token operator">=</span> <span class="token function">yf</span><span class="token punctuation">(</span><span class="token operator">:</span><span class="token punctuation">)</span><span class="token operator">'</span> <span class="token operator">*</span> <span class="token function">yf</span><span class="token punctuation">(</span><span class="token operator">:</span><span class="token punctuation">)</span> <span class="token operator">/</span> N<span class="token punctuation">;</span>  <span class="token comment" spellcheck="true">%squared norm of y</span>
		<span class="token comment" spellcheck="true">%cross-correlation term in Fourier domain</span>
		xyf <span class="token operator">=</span> xf <span class="token operator">.*</span> <span class="token function">conj</span><span class="token punctuation">(</span>yf<span class="token punctuation">)</span><span class="token punctuation">;</span>
		xy <span class="token operator">=</span> <span class="token function">sum</span><span class="token punctuation">(</span><span class="token function">real</span><span class="token punctuation">(</span><span class="token function">ifft2</span><span class="token punctuation">(</span>xyf<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">,</span> <span class="token number">3</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  <span class="token comment" spellcheck="true">%to spatial domain</span>
		kf <span class="token operator">=</span> <span class="token function">fft2</span><span class="token punctuation">(</span><span class="token function">exp</span><span class="token punctuation">(</span><span class="token operator">-</span><span class="token number">1</span> <span class="token operator">/</span> sigma<span class="token operator">^</span><span class="token number">2</span> <span class="token operator">*</span> <span class="token function">max</span><span class="token punctuation">(</span><span class="token number">0</span><span class="token punctuation">,</span> <span class="token punctuation">(</span>xx <span class="token operator">+</span> yy <span class="token operator">-</span> <span class="token number">2</span> <span class="token operator">*</span> xy<span class="token punctuation">)</span> <span class="token operator">/</span> <span class="token function">numel</span><span class="token punctuation">(</span>xf<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token keyword">end</span>
</code></pre>
<ol start="3">
<li><script type="math/tex" id="MathJax-Element-167">\alpha</script></li>
</ol>
<pre class=" language-matlab"><code class="prism  language-matlab">    	new_alphaf <span class="token operator">=</span> state<span class="token punctuation">.</span>yf <span class="token operator">./</span><span class="token punctuation">(</span>kf <span class="token operator">+</span> <span class="token number">0.0001</span><span class="token punctuation">)</span><span class="token punctuation">;</span> 
</code></pre>
<ol start="4">
<li><script type="math/tex" id="MathJax-Element-168">\mathcal F(\kappa(\mathbf x, \mathbf x'))</script></li>
</ol>
<pre class=" language-matlab"><code class="prism  language-matlab">	<span class="token comment" spellcheck="true">% next  frame</span>
    x <span class="token operator">=</span> <span class="token function">get_region</span><span class="token punctuation">(</span>im<span class="token punctuation">,</span> state<span class="token punctuation">)</span><span class="token punctuation">;</span>
    x <span class="token operator">=</span> <span class="token function">double</span><span class="token punctuation">(</span><span class="token function">fhog</span><span class="token punctuation">(</span><span class="token function">single</span><span class="token punctuation">(</span>x<span class="token punctuation">)</span> <span class="token operator">/</span> <span class="token number">255</span><span class="token punctuation">,</span> state<span class="token punctuation">.</span>cell_size<span class="token punctuation">,</span><span class="token number">9</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token function">x</span><span class="token punctuation">(</span><span class="token operator">:</span><span class="token punctuation">,</span><span class="token operator">:</span><span class="token punctuation">,</span><span class="token keyword">end</span><span class="token punctuation">)</span> <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">;</span> 
    x <span class="token operator">=</span> <span class="token function">bsxfun</span><span class="token punctuation">(</span><span class="token operator">@</span>times<span class="token punctuation">,</span> x<span class="token punctuation">,</span> state<span class="token punctuation">.</span>cos_window<span class="token punctuation">)</span><span class="token punctuation">;</span>
    xf <span class="token operator">=</span> <span class="token function">fft2</span><span class="token punctuation">(</span>x<span class="token punctuation">)</span><span class="token punctuation">;</span>
    kf <span class="token operator">=</span> <span class="token function">dense_gauss_kernel</span><span class="token punctuation">(</span> xf<span class="token punctuation">,</span> state<span class="token punctuation">.</span>z<span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment" spellcheck="true">% z is template</span>
</code></pre>
<pre class=" language-matlab"><code class="prism  language-matlab">	state<span class="token punctuation">.</span>z <span class="token operator">=</span> <span class="token punctuation">(</span><span class="token number">1</span> <span class="token operator">-</span> interp_factor<span class="token punctuation">)</span> <span class="token operator">*</span> state<span class="token punctuation">.</span>z <span class="token operator">+</span> interp_factor <span class="token operator">*</span> xf<span class="token punctuation">;</span>
</code></pre>
<ol start="5">
<li><script type="math/tex" id="MathJax-Element-169">[p_x,p_y] = \arg \max \hat{\mathbf y},</script></li>
</ol>
<pre class=" language-matlab"><code class="prism  language-matlab">	response <span class="token operator">=</span> <span class="token function">real</span><span class="token punctuation">(</span><span class="token function">ifft2</span><span class="token punctuation">(</span>state<span class="token punctuation">.</span>alphaf <span class="token operator">.*</span> kf<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>   
    <span class="token punctuation">[</span>yc<span class="token punctuation">,</span> xc<span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token function">find</span><span class="token punctuation">(</span>response <span class="token operator">==</span> <span class="token function">max</span><span class="token punctuation">(</span><span class="token function">response</span><span class="token punctuation">(</span><span class="token operator">:</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">,</span> <span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<hr>
<p><strong>Experiments:</strong></p>
<ol>
<li>dataset:  OTB 50 videoes</li>
<li>algorithms: MOSSE, TLD, CT, STRUCK,</li>
</ol>
<p><img src="KernelCorrelationFilter/re_kcf.png" alt=""></p>
<p><strong>Conlusions</strong></p>
<p><img src="KernelCorrelationFilter/KCF1.png" alt=""></p>
<p><strong>Contributions:</strong></p>
<ol>
<li>the connection between Ridge Regression with cyclically shifted samples and classical correlation filters.</li>
<li>it proposed closed-form solutions to compute kernels at all cyclic shifts.</li>
<li>extend the original work to deal with multiple channels.</li>
</ol>
<hr>
<p><strong>Beyond:</strong></p>
<ul>
<li>Scale ?</li>
<li>Loss functions: hingle loss?, exponent loss?</li>
<li>… …</li>
</ul>
<hr>
<h2 id="dsst-accurate-scale-estimation-for-robust-visual-trackingbmvc-2014">DSST: Accurate Scale Estimation for Robust Visual Tracking(BMVC 2014)</h2>
<p>Martin Danelljan, Gustav H?ger, Fahad Shahbaz Khan and Michael Felsberg.<br>
<a href="http://www.cvl.isy.liu.se/research/objrec/visualtracking/scalvistrack/DSST_code.zip">Matlab</a></p>
<hr>
<h3 id="problem-1">Problem</h3>
<p><strong>Accurate scale estimation</strong><br>
<img src="KernelCorrelationFilter/dsst1.png" alt=""></p>
<h3 id="idea-1">Idea</h3>
<blockquote>
<p>scale =  pyramid  +  correlation filter</p>
</blockquote>
<p>先估计目标空间位置，然后估计目标的尺度。</p>
<p><strong>step1: The Translation Filter:</strong><br>
<img src="KernelCorrelationFilter/dsst2.png" alt=""></p>
<p>*<strong>step2: The Scale Filter:</strong><br>
<img src="KernelCorrelationFilter/dsst3.png" alt=""></p>
<hr>
<p><strong>Algorithms DSST</strong><br>
<img src="KernelCorrelationFilter/dsst4.png" alt=""></p>
<h3 id="scale-estimation">Scale Estimation</h3>
<ul>
<li>object size : <script type="math/tex" id="MathJax-Element-170">P\times R</script></li>
<li>scales: <script type="math/tex" id="MathJax-Element-171">n \in \{ \lfloor -\frac{s-1}{2} \rfloor, \cdots,\lfloor \frac{s-1}{2} \rfloor \}</script></li>
<li>patch <script type="math/tex" id="MathJax-Element-172">J_n</script> size: <script type="math/tex" id="MathJax-Element-173">a^n P \times a^nR</script> :Scale increment factor</li>
</ul>
<p><strong>Step1: scales setting</strong></p>
<pre class=" language-matlab"><code class="prism  language-matlab">nScales<span class="token operator">=</span> <span class="token number">33</span><span class="token punctuation">;</span>           <span class="token comment" spellcheck="true">% number of scale levels (denoted "S" in the paper)</span>
scale_step <span class="token operator">=</span> <span class="token number">1.02</span><span class="token punctuation">;</span>               <span class="token comment" spellcheck="true">% Scale increment factor (denoted "a" in the paper)</span>
<span class="token comment" spellcheck="true">% scale factors</span>
ss <span class="token operator">=</span> <span class="token number">1</span><span class="token operator">:</span>nScales<span class="token punctuation">;</span>
scaleFactors <span class="token operator">=</span> scale_step<span class="token operator">.^</span><span class="token punctuation">(</span><span class="token function">ceil</span><span class="token punctuation">(</span>nScales<span class="token operator">/</span><span class="token number">2</span><span class="token punctuation">)</span> <span class="token operator">-</span> ss<span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p>**Step2: expected scale respons <script type="math/tex" id="MathJax-Element-174">\mathbf y</script>**</p>
<pre class=" language-matlab"><code class="prism  language-matlab"><span class="token comment" spellcheck="true">% desired scale filter output (gaussian shaped), bandwidth proportional to</span>
<span class="token comment" spellcheck="true">% number of scales</span>
scale_sigma <span class="token operator">=</span> nScales<span class="token operator">/</span><span class="token function">sqrt</span><span class="token punctuation">(</span><span class="token number">33</span><span class="token punctuation">)</span> <span class="token operator">*</span> scale_sigma_factor<span class="token punctuation">;</span>
ss <span class="token operator">=</span> <span class="token punctuation">(</span><span class="token number">1</span><span class="token operator">:</span>nScales<span class="token punctuation">)</span> <span class="token operator">-</span> <span class="token function">ceil</span><span class="token punctuation">(</span>nScales<span class="token operator">/</span><span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
ys <span class="token operator">=</span> <span class="token function">exp</span><span class="token punctuation">(</span><span class="token operator">-</span><span class="token number">0.5</span> <span class="token operator">*</span> <span class="token punctuation">(</span>ss<span class="token operator">.^</span><span class="token number">2</span><span class="token punctuation">)</span> <span class="token operator">/</span> scale_sigma<span class="token operator">^</span><span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
ysf <span class="token operator">=</span> <span class="token function">single</span><span class="token punctuation">(</span><span class="token function">fft</span><span class="token punctuation">(</span>ys<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p><strong>Step3: scale pathes extracting</strong></p>
<ul>
<li>将目标的尺度（宽度和高度）进行缩放，获取对应位置的图像patch；</li>
<li>将patch resize为模板的大小，以便和模板比对；</li>
<li>提取新patch的hog特征；</li>
<li>将hog特征转为一个列向量，然后乘以hanning窗</li>
</ul>
<pre class=" language-matlab"><code class="prism  language-matlab"><span class="token keyword">function</span> out <span class="token operator">=</span> <span class="token function">get_scale_sample</span><span class="token punctuation">(</span>im<span class="token punctuation">,</span> pos<span class="token punctuation">,</span> base_target_sz<span class="token punctuation">,</span> scaleFactors<span class="token punctuation">,</span> scale_window<span class="token punctuation">,</span> scale_model_sz<span class="token punctuation">)</span>
<span class="token comment" spellcheck="true">% out = get_scale_sample(im, pos, base_target_sz, scaleFactors, scale_window, scale_model_sz)</span>
<span class="token comment" spellcheck="true">% </span>
<span class="token comment" spellcheck="true">% Extracts a sample for the scale filter at the current</span>
<span class="token comment" spellcheck="true">% location and scale.</span>
nScales <span class="token operator">=</span> <span class="token function">length</span><span class="token punctuation">(</span>scaleFactors<span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token keyword">for</span> s <span class="token operator">=</span> <span class="token number">1</span><span class="token operator">:</span>nScales
    patch_sz <span class="token operator">=</span> <span class="token function">floor</span><span class="token punctuation">(</span>base_target_sz <span class="token operator">*</span> <span class="token function">scaleFactors</span><span class="token punctuation">(</span>s<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>    
    xs <span class="token operator">=</span> <span class="token function">floor</span><span class="token punctuation">(</span><span class="token function">pos</span><span class="token punctuation">(</span><span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token operator">+</span> <span class="token punctuation">(</span><span class="token number">1</span><span class="token operator">:</span><span class="token function">patch_sz</span><span class="token punctuation">(</span><span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token operator">-</span> <span class="token function">floor</span><span class="token punctuation">(</span><span class="token function">patch_sz</span><span class="token punctuation">(</span><span class="token number">2</span><span class="token punctuation">)</span><span class="token operator">/</span><span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    ys <span class="token operator">=</span> <span class="token function">floor</span><span class="token punctuation">(</span><span class="token function">pos</span><span class="token punctuation">(</span><span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token operator">+</span> <span class="token punctuation">(</span><span class="token number">1</span><span class="token operator">:</span><span class="token function">patch_sz</span><span class="token punctuation">(</span><span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token operator">-</span> <span class="token function">floor</span><span class="token punctuation">(</span><span class="token function">patch_sz</span><span class="token punctuation">(</span><span class="token number">1</span><span class="token punctuation">)</span><span class="token operator">/</span><span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">;</span>    
    <span class="token comment" spellcheck="true">% check for out-of-bounds coordinates, and set them to the values at</span>
    <span class="token comment" spellcheck="true">% the borders</span>
    <span class="token function">xs</span><span class="token punctuation">(</span>xs <span class="token operator">&lt;</span> <span class="token number">1</span><span class="token punctuation">)</span> <span class="token operator">=</span> <span class="token number">1</span><span class="token punctuation">;</span>
    <span class="token function">ys</span><span class="token punctuation">(</span>ys <span class="token operator">&lt;</span> <span class="token number">1</span><span class="token punctuation">)</span> <span class="token operator">=</span> <span class="token number">1</span><span class="token punctuation">;</span>
    <span class="token function">xs</span><span class="token punctuation">(</span>xs <span class="token operator">&gt;</span> <span class="token function">size</span><span class="token punctuation">(</span>im<span class="token punctuation">,</span><span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token operator">=</span> <span class="token function">size</span><span class="token punctuation">(</span>im<span class="token punctuation">,</span><span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token function">ys</span><span class="token punctuation">(</span>ys <span class="token operator">&gt;</span> <span class="token function">size</span><span class="token punctuation">(</span>im<span class="token punctuation">,</span><span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">)</span> <span class="token operator">=</span> <span class="token function">size</span><span class="token punctuation">(</span>im<span class="token punctuation">,</span><span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">;</span>    
    <span class="token comment" spellcheck="true">% extract image</span>
    im_patch <span class="token operator">=</span> <span class="token function">im</span><span class="token punctuation">(</span>ys<span class="token punctuation">,</span> xs<span class="token punctuation">,</span> <span class="token operator">:</span><span class="token punctuation">)</span><span class="token punctuation">;</span>    
    <span class="token comment" spellcheck="true">% resize image to model size</span>
    im_patch_resized <span class="token operator">=</span> <span class="token function">mexResize</span><span class="token punctuation">(</span>im_patch<span class="token punctuation">,</span> scale_model_sz<span class="token punctuation">,</span> <span class="token string">'auto'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>    
    <span class="token comment" spellcheck="true">% extract scale features</span>
    temp_hog <span class="token operator">=</span> <span class="token function">fhog</span><span class="token punctuation">(</span><span class="token function">single</span><span class="token punctuation">(</span>im_patch_resized<span class="token punctuation">)</span><span class="token punctuation">,</span> <span class="token number">4</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    temp <span class="token operator">=</span> <span class="token function">temp_hog</span><span class="token punctuation">(</span><span class="token operator">:</span><span class="token punctuation">,</span><span class="token operator">:</span><span class="token punctuation">,</span><span class="token number">1</span><span class="token operator">:</span><span class="token number">31</span><span class="token punctuation">)</span><span class="token punctuation">;</span>    
    <span class="token keyword">if</span> s <span class="token operator">==</span> <span class="token number">1</span>
        out <span class="token operator">=</span> <span class="token function">zeros</span><span class="token punctuation">(</span><span class="token function">numel</span><span class="token punctuation">(</span>temp<span class="token punctuation">)</span><span class="token punctuation">,</span> nScales<span class="token punctuation">,</span> <span class="token string">'single'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token keyword">end</span>    
    <span class="token comment" spellcheck="true">% window</span>
    <span class="token function">out</span><span class="token punctuation">(</span><span class="token operator">:</span><span class="token punctuation">,</span>s<span class="token punctuation">)</span> <span class="token operator">=</span> <span class="token function">temp</span><span class="token punctuation">(</span><span class="token operator">:</span><span class="token punctuation">)</span> <span class="token operator">*</span> <span class="token function">scale_window</span><span class="token punctuation">(</span>s<span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token keyword">end</span>
</code></pre>
<p>**step4:  计算<script type="math/tex" id="MathJax-Element-175">\alpha</script>**</p>
<pre class=" language-matlab"><code class="prism  language-matlab">	 xs <span class="token operator">=</span> <span class="token function">get_scale_sample</span><span class="token punctuation">(</span>im<span class="token punctuation">,</span> pos<span class="token punctuation">,</span> base_target_sz<span class="token punctuation">,</span> currentScaleFactor <span class="token operator">*</span> scaleFactors<span class="token punctuation">,</span> scale_window<span class="token punctuation">,</span> scale_model_sz<span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token comment" spellcheck="true">% calculate the scale filter update</span>
    xsf <span class="token operator">=</span> <span class="token function">fft</span><span class="token punctuation">(</span>xs<span class="token punctuation">,</span><span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">,</span><span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    new_sf_num <span class="token operator">=</span> <span class="token function">bsxfun</span><span class="token punctuation">(</span><span class="token operator">@</span>times<span class="token punctuation">,</span> ysf<span class="token punctuation">,</span> <span class="token function">conj</span><span class="token punctuation">(</span>xsf<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    new_sf_den <span class="token operator">=</span> <span class="token function">sum</span><span class="token punctuation">(</span>xsf <span class="token operator">.*</span> <span class="token function">conj</span><span class="token punctuation">(</span>xsf<span class="token punctuation">)</span><span class="token punctuation">,</span> <span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p>**Step5: Prediction <script type="math/tex" id="MathJax-Element-176">\mathbf y'</script>**</p>
<pre class=" language-matlab"><code class="prism  language-matlab">	 <span class="token comment" spellcheck="true">% extract the test sample feature map for the scale filter</span>
        xs <span class="token operator">=</span> <span class="token function">get_scale_sample</span><span class="token punctuation">(</span>im<span class="token punctuation">,</span> pos<span class="token punctuation">,</span> base_target_sz<span class="token punctuation">,</span> currentScaleFactor <span class="token operator">*</span> scaleFactors<span class="token punctuation">,</span> scale_window<span class="token punctuation">,</span> scale_model_sz<span class="token punctuation">)</span><span class="token punctuation">;</span>        
        <span class="token comment" spellcheck="true">% calculate the correlation response of the scale filter</span>
        xsf <span class="token operator">=</span> <span class="token function">fft</span><span class="token punctuation">(</span>xs<span class="token punctuation">,</span><span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">,</span><span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        scale_response <span class="token operator">=</span> <span class="token function">real</span><span class="token punctuation">(</span><span class="token function">ifft</span><span class="token punctuation">(</span><span class="token function">sum</span><span class="token punctuation">(</span>sf_num <span class="token operator">.*</span> xsf<span class="token punctuation">,</span> <span class="token number">1</span><span class="token punctuation">)</span> <span class="token operator">./</span> <span class="token punctuation">(</span>sf_den <span class="token operator">+</span> lambda<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p><strong>Step6: 估计目标尺度</strong></p>
<pre class=" language-matlab"><code class="prism  language-matlab"> 	<span class="token comment" spellcheck="true">% find the maximum scale response</span>
    recovered_scale <span class="token operator">=</span> <span class="token function">find</span><span class="token punctuation">(</span>scale_response <span class="token operator">==</span> <span class="token function">max</span><span class="token punctuation">(</span><span class="token function">scale_response</span><span class="token punctuation">(</span><span class="token operator">:</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">,</span> <span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
 	<span class="token comment" spellcheck="true">% update the scale</span>
    currentScaleFactor <span class="token operator">=</span> currentScaleFactor <span class="token operator">*</span> <span class="token function">scaleFactors</span><span class="token punctuation">(</span>recovered_scale<span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<h3 id="expeiments">Expeiments</h3>
<ol>
<li>dateset: ** 28 sequences**<sup class="footnote-ref"><a href="#fn1" id="fnref1">1</a></sup> annotated with the scale variation attribute</li>
<li>algorithms:</li>
</ol>
<p><img src="KernelCorrelationFilter/dsst5.png" alt=""></p>
<h3 id="conlusions">Conlusions:</h3>
<ol>
<li>learning discriminative correlation filters based on a scale pyramid representation.</li>
<li>transform = 2D correlation filter , scale = 1D correlation filter</li>
</ol>
<h3 id="contribution">Contribution:</h3>
<blockquote>
<p>pyramid + correlation filter</p>
</blockquote>
<h3 id="beyond">Beyond:</h3>
<ol>
<li>若空间位置不准，scale估计也会出现大的偏差；</li>
<li>没有用到kernel也取得了好的效果；</li>
<li>和以前的方法（NCC）相比，只是将响应期望由冲击响应变为gauss或者laplacian分布；</li>
</ol>
<hr>
<h2 id="scale-adaptive-kernel-correlation-filter-tracker-with-feature-integrationeccvw2014">Scale Adaptive Kernel Correlation Filter Tracker with Feature Integration(ECCVW2014)</h2>
<pre><code>Yang Li, Jianke Zhu
</code></pre>
<p><a href="https://github.com/ihpdep/samf">Matlab</a></p>
<ul>
<li>Problem: scale estimation</li>
<li>Idea:
<ul>
<li>multi-scales:  sampling the patch to different scales compared with template.</li>
<li>feature : hog + cn</li>
</ul>
</li>
<li>Codes</li>
</ul>
<pre class=" language-matlab"><code class="prism  language-matlab">	search_size <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token number">1</span>  <span class="token number">0.985</span> <span class="token number">0.99</span> <span class="token number">0.995</span> <span class="token number">1.005</span> <span class="token number">1.01</span> <span class="token number">1.015</span><span class="token punctuation">]</span><span class="token punctuation">;</span><span class="token comment" spellcheck="true">% 	</span>
	<span class="token keyword">for</span> <span class="token number">i</span><span class="token operator">=</span><span class="token number">1</span><span class="token operator">:</span><span class="token function">size</span><span class="token punctuation">(</span>search_size<span class="token punctuation">,</span><span class="token number">2</span><span class="token punctuation">)</span>
    tmp_sz <span class="token operator">=</span> <span class="token function">floor</span><span class="token punctuation">(</span><span class="token punctuation">(</span>target_sz <span class="token operator">*</span> <span class="token punctuation">(</span><span class="token number">1</span> <span class="token operator">+</span> padding<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token operator">*</span><span class="token function">search_size</span><span class="token punctuation">(</span><span class="token number">i</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    param0 <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token function">pos</span><span class="token punctuation">(</span><span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">,</span> <span class="token function">pos</span><span class="token punctuation">(</span><span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">,</span> <span class="token function">tmp_sz</span><span class="token punctuation">(</span><span class="token number">2</span><span class="token punctuation">)</span><span class="token operator">/</span><span class="token function">window_sz</span><span class="token punctuation">(</span><span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">,</span> <span class="token number">0</span><span class="token punctuation">,</span><span class="token punctuation">...</span>
                        <span class="token function">tmp_sz</span><span class="token punctuation">(</span><span class="token number">1</span><span class="token punctuation">)</span><span class="token operator">/</span><span class="token function">window_sz</span><span class="token punctuation">(</span><span class="token number">2</span><span class="token punctuation">)</span><span class="token operator">/</span><span class="token punctuation">(</span><span class="token function">window_sz</span><span class="token punctuation">(</span><span class="token number">1</span><span class="token punctuation">)</span><span class="token operator">/</span><span class="token function">window_sz</span><span class="token punctuation">(</span><span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">,</span><span class="token number">0</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
    param0 <span class="token operator">=</span> <span class="token function">affparam2mat</span><span class="token punctuation">(</span>param0<span class="token punctuation">)</span><span class="token punctuation">;</span> 
    patch <span class="token operator">=</span> <span class="token function">uint8</span><span class="token punctuation">(</span><span class="token function">warpimg</span><span class="token punctuation">(</span><span class="token function">double</span><span class="token punctuation">(</span>im<span class="token punctuation">)</span><span class="token punctuation">,</span> param0<span class="token punctuation">,</span> window_sz<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    zf <span class="token operator">=</span> <span class="token function">fft2</span><span class="token punctuation">(</span><span class="token function">get_features</span><span class="token punctuation">(</span>patch<span class="token punctuation">,</span> features<span class="token punctuation">,</span> cell_size<span class="token punctuation">,</span> cos_window<span class="token punctuation">,</span>w2c<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token function">response</span><span class="token punctuation">(</span><span class="token operator">:</span><span class="token punctuation">,</span><span class="token operator">:</span><span class="token punctuation">,</span><span class="token number">i</span><span class="token punctuation">)</span> <span class="token operator">=</span> <span class="token function">real</span><span class="token punctuation">(</span><span class="token function">ifft2</span><span class="token punctuation">(</span>model_alphaf <span class="token operator">.*</span> kzf<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  
	<span class="token keyword">end</span>
	<span class="token punctuation">[</span>vert_delta<span class="token punctuation">,</span>tmp<span class="token punctuation">,</span> horiz_delta<span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token function">find</span><span class="token punctuation">(</span>response <span class="token operator">==</span> <span class="token function">max</span><span class="token punctuation">(</span><span class="token function">response</span><span class="token punctuation">(</span><span class="token operator">:</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">,</span> <span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	szid <span class="token operator">=</span> <span class="token function">floor</span><span class="token punctuation">(</span><span class="token punctuation">(</span>tmp<span class="token number">-1</span><span class="token punctuation">)</span><span class="token operator">/</span><span class="token punctuation">(</span><span class="token function">size</span><span class="token punctuation">(</span>cos_window<span class="token punctuation">,</span><span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token operator">+</span><span class="token number">1</span><span class="token punctuation">;</span>
	horiz_delta <span class="token operator">=</span> tmp <span class="token operator">-</span> <span class="token punctuation">(</span><span class="token punctuation">(</span>szid <span class="token operator">-</span><span class="token number">1</span><span class="token punctuation">)</span><span class="token operator">*</span> <span class="token function">size</span><span class="token punctuation">(</span>cos_window<span class="token punctuation">,</span><span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	<span class="token keyword">if</span> vert_delta <span class="token operator">&gt;</span> <span class="token function">size</span><span class="token punctuation">(</span>zf<span class="token punctuation">,</span><span class="token number">1</span><span class="token punctuation">)</span> <span class="token operator">/</span> <span class="token number">2</span><span class="token punctuation">,</span> 
		vert_delta <span class="token operator">=</span> vert_delta <span class="token operator">-</span> <span class="token function">size</span><span class="token punctuation">(</span>zf<span class="token punctuation">,</span><span class="token number">1</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	<span class="token keyword">end</span>
	<span class="token keyword">if</span> horiz_delta <span class="token operator">&gt;</span> <span class="token function">size</span><span class="token punctuation">(</span>zf<span class="token punctuation">,</span><span class="token number">2</span><span class="token punctuation">)</span> <span class="token operator">/</span> <span class="token number">2</span><span class="token punctuation">,</span>  <span class="token comment" spellcheck="true">%same for horizontal axis</span>
		horiz_delta <span class="token operator">=</span> horiz_delta <span class="token operator">-</span> <span class="token function">size</span><span class="token punctuation">(</span>zf<span class="token punctuation">,</span><span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	<span class="token keyword">end</span>
	tmp_sz <span class="token operator">=</span> <span class="token function">floor</span><span class="token punctuation">(</span><span class="token punctuation">(</span>target_sz <span class="token operator">*</span> <span class="token punctuation">(</span><span class="token number">1</span> <span class="token operator">+</span> padding<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token operator">*</span><span class="token function">search_size</span><span class="token punctuation">(</span>szid<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	current_size <span class="token operator">=</span> <span class="token function">tmp_sz</span><span class="token punctuation">(</span><span class="token number">2</span><span class="token punctuation">)</span><span class="token operator">/</span><span class="token function">window_sz</span><span class="token punctuation">(</span><span class="token number">2</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	pos <span class="token operator">=</span> pos <span class="token operator">+</span> current_size<span class="token operator">*</span>cell_size <span class="token operator">*</span> <span class="token punctuation">[</span>vert_delta <span class="token operator">-</span> <span class="token number">1</span><span class="token punctuation">,</span> horiz_delta <span class="token operator">-</span> <span class="token number">1</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
</code></pre>
<hr>
<h2 id="rpt-reliable-patch-trackers-robust-visual-tracking-by-exploiting-reliable-patchescvpr2015">RPT: Reliable Patch Trackers: Robust Visual Tracking by Exploiting Reliable Patches(CVPR2015)</h2>
<pre><code>Yang Li, Jianke Zhu, Steven C.H. Hoi
</code></pre>
<p><a href="https://github.com/ihpdep/rpt">Matlab</a></p>
<h2 id="fast-tracking-via-dense-spatio-temporal-context-leraning">Fast Tracking via Dense Spatio-Temporal Context Leraning</h2>
<p>Kaihua Zhang, Lei Zhang, Qingshan Liu, David Zhang, and Ming-Hsuan Yang<br>
European Conference on Computer Vision (ECCV 2014), pp. 127-141, Zurich, Switzerland, September, 2014.<br>
<a href="http://www4.comp.polyu.edu.hk/~cslzhang/STC/STC.htm">Matlab</a></p>
<h2 id="srdcf-learning-spatially-regularized-correlation-filters-for-visual-tracking-iccv2015">SRDCF: Learning Spatially Regularized Correlation Filters for Visual Tracking (ICCV2015)</h2>
<p>[Project] (<a href="http://www.cvl.isy.liu.se/research/objrec/visualtracking/regvistrack/index.html">http://www.cvl.isy.liu.se/research/objrec/visualtracking/regvistrack/index.html</a>)</p>
<hr>
<h2 id="acf-adaptive-color-attributes-for-real-time-visual-tracking">ACF: Adaptive Color Attributes for Real-Time Visual Tracking</h2>
<p>Martin Danelljan, Fahad Shahbaz Khan, Michael Felsberg and Joost van de Weijer.<br>
In Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition (CVPR), 2014 (Oral).<br>
<a href="http://www.cvl.isy.liu.se/research/objrec/visualtracking/colvistrack/ColorTracking_code.zip">Matlab</a></p>
<h2 id="lcf-long-term-correlation-trackingcvpr2015">LCF: Long-term Correlation Tracking(CVPR2015)</h2>
<p>Chao Ma, Xiaokang Yang, Chongyang Zhang, and Ming-Hsuan Yang,<br>
<a href="https://sites.google.com/site/chaoma99/cvpr15_tracking">Project</a></p>
<hr>
<hr class="footnotes-sep">
<section class="footnotes">
<ol class="footnotes-list">
<li id="fn1" class="footnote-item"><p>YiWu, Jongwoo Lim, and Ming-Hsuan Yang. Online object tracking: A benchmark. in CVPR, 2013. <a href="#fnref1" class="footnote-backref">↩</a></p>
</li>
</ol>
</section>