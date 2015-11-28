<h1 id="kernelized-supervised-context-hashing">Kernelized Supervised Context Hashing</h1>
<p><strong>摘要要说明的几个问题:</strong></p>
<ol>
<li>要解决的问题是什么?</li>
<li>我们观察到的现象是什么?</li>
<li>idea是什么:用一句简单精炼的话来的描述</li>
<li>我们的采用的方法是什么:具体步骤,如何实现?</li>
<li>通过<em>对比实验</em>来<strong>验证</strong>我们这个方法的优越性, <strong>佐证</strong>提出的理论和方法的正确性.</li>
</ol>
<hr>
<p><strong>Abstract:</strong></p>
<p>Most existing supervised hashing methods formulate hashing learning based on the Hamming affinity calculated by inner product of binary codes, which assume that all hashing bits are irrelevant.</p>
<blockquote>
<p><strong>修改：</strong><br>
Most existing supervised hashing methods learn the affinity-preserving binary codes to represent the high-dimensional data. However, each hashing code is assumed as independent and irrelevant with other codes.</p>
</blockquote>
<p>Typically, there may be exist context correlations among hashing bits.Here we propose a kernelized supervised context hashing (KSCH) method, which exploits the context information among hashing codes to reduce the quantization error.</p>
<blockquote>
<p><strong>修改：</strong><br>
In practice, we find that  there  exists context association among hashing bits. According to the above observation,  the hashing codes interrelation is exploited to reduce the quantization error, which is called kernelized supervised context hashing (KSCH)  in this paper.</p>
</blockquote>
<p>In our approach, we first employ the kernel formulation to tackle the practical data which is mostly linear inseparable, and then utilize different distributions to approximately extract the context information. Finally, a gradient descent method iteratively learns hashing codes and redefined the Hamming affinity to derive desired hashing codes which integrate the context information.</p>
<blockquote>
<p><strong>修改：</strong><br>
In this work, the kernel formulation is employed to tackle the high-dimensional data which is mostly linear inseparable firstly; and then three different distributions are utilized to describe the binary codes  context;  finally, the  hashing codes can be approximated by gradient descent method iteratively.  Therefore, the correlation between the hash codes is integrated to redefined the  <strong>metric measurement</strong> to hold the data affinity in the raw space.</p>
</blockquote>
<p>We evaluate our method on two image benchmarks and experimental results show that it achieves better performance than several other state-of-the-art methods.</p>
<blockquote>
<p>写的太简单了，在那些数据库上，和那些方法方法进行了对比，性能提升多少（具体数字）。或者在特定的维数上有大的提升。</p>
</blockquote>
<hr>
<p>问题：</p>
<ol>
<li>论文的三个关键的创新点：
<ul>
<li>上下文</li>
<li>kernel</li>
<li>模型优化</li>
</ul>
</li>
</ol>
<blockquote>
<p>摘要没有围绕这三点来写，而仅仅只是围绕上下文在说，而且上下文信息只是利用高斯分布对原始的hash codes做加权。<br>
建议从提出的问题, 到观察的现象,到问题的求解都要围绕着三个问题说到.</p>
</blockquote>
<ol start="2">
<li>Hamming affinity 的意思我不是很明白？我觉得主要是最后一个 测度度量（metric measure）的问题。</li>
<li>主动的语句有些多；</li>
<li>副词应该放在句子最后；</li>
</ol>