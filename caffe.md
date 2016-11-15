<h1 id="caffe--安装与使用">Caffe  安装与使用</h1>
<ol>
<li>虚拟机Ubuntu14.04： CPU without GPU</li>
</ol>
<hr>
<p><a href="http://suanfazu.com/t/caffe/13577">Caffe上手教程:</a></p>
<p><a href="http://suanfazu.com/t/ubuntu-14-04-caffe/447">在Ubuntu 14.04上安装Caffe:</a></p>
<ol>
<li>安装依赖</li>
</ol>
<pre><code>sudo apt-get install libatlas-base-dev
sudo apt-get install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libboost-all-dev libhdf5-serial-dev
sudo apt-get install libgflags-dev libgoogle-glog-dev liblmdb-dev protobuf-compiler
</code></pre>
<ol start="2">
<li>安装Caffe</li>
</ol>
<pre><code>git clone https://github.com/BVLC/caffe.git
cd caffe
cp Makefile.config.example Makefile.config
</code></pre>
<ol start="3">
<li>选择只用CPU（不用GPU）计算</li>
</ol>
<pre><code>vi Makefile.config
# Adjust Makefile.config (for example, if using Anaconda Python)
# uncomment CPU_ONLY := 1
</code></pre>
<p>注意事项：<br>
- GPU使用<br>
- matlab 路径<br>
- python 路径</p>
<ol start="4">
<li>最后编译</li>
</ol>
<pre><code>make all
make matcaffe
make pycaffe
</code></pre>
<p>pycaffe 出错，找不见caffe：原因是系统中安装了两个python：</p>
<pre><code>pip install protobuf
aconda2/bin/pip protobuf
</code></pre>
<ol start="5">
<li>测试（可选）</li>
</ol>
<pre><code>make test
make runtest
</code></pre>
<p>error:``</p>
<ol start="6">
<li>使用Caffe: 跑MNIST试试</li>
</ol>
<pre><code>cd caffe
sh data/mnist/get_mnist.sh
sh examples/mnist/create_mnist.sh
vi examples/mnist/lenet_solver.prototxt
# 修改 solver_mode 为 CPU
./examples/mnist/train_lenet.sh
</code></pre>
<hr>
<ol start="2">
<li>Ubuntu14.04  with GPU</li>
</ol>
<hr>
<p><a href="http://caffe.berkeleyvision.org/install_apt.html">官方网站：</a></p>
<p><a href="http://coldmooon.github.io/2015/08/03/caffe_install/">从零安装caffe（ubuntu4.04）</a></p>
<hr>
<h3 id="matcaffe-使用">MatCaffe 使用</h3>
<ol start="6">
<li>下载库：在<a href="https://github.com/BVLC/caffe">github</a>对应的<code>model</code>中链接</li>
<li>read image:</li>
</ol>
<pre><code>im = imred('caffe/examples/images/cap.jpg');
[scores, maxlabel] = classification_demo(im, 0);
</code></pre>
<p>workspace</p>
<pre><code>Elapsed time is 0.015581 seconds
Elapsed time is 1.274006 seconds
</code></pre>
<hr>
<blockquote>
<p><code>classification_demo</code></p>
</blockquote>
<hr>
<ol start="8">
<li>data:
<ul>
<li>matlab: height * width *chanels(RGB)</li>
<li>caffe: [width * height * channels(BGR)*images]</li>
<li>code:</li>
</ul>
</li>
</ol>
<pre class=" language-matlab"><code class="prism  language-matlab">	
	im_data <span class="token operator">=</span> <span class="token function">im</span><span class="token punctuation">(</span><span class="token operator">:</span><span class="token punctuation">,</span> <span class="token operator">:</span><span class="token punctuation">,</span> <span class="token punctuation">[</span><span class="token number">3</span><span class="token punctuation">,</span> <span class="token number">2</span><span class="token punctuation">,</span> <span class="token number">1</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  <span class="token comment" spellcheck="true">% permute channels from RGB to BGR</span>
	im_data <span class="token operator">=</span> <span class="token function">permute</span><span class="token punctuation">(</span>im_data<span class="token punctuation">,</span> <span class="token punctuation">[</span><span class="token number">2</span><span class="token punctuation">,</span> <span class="token number">1</span><span class="token punctuation">,</span> <span class="token number">3</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  <span class="token comment" spellcheck="true">% flip width and height</span>
	im_data <span class="token operator">=</span> <span class="token function">single</span><span class="token punctuation">(</span>im_data<span class="token punctuation">)</span><span class="token punctuation">;</span>  <span class="token comment" spellcheck="true">% convert from uint8 to single</span>

	<span class="token comment" spellcheck="true">%% resize + oversample</span>
	im_data <span class="token operator">=</span> <span class="token function">imresize</span><span class="token punctuation">(</span>im_data<span class="token punctuation">,</span> <span class="token punctuation">[</span>IMAGE_DIM IMAGE_DIM<span class="token punctuation">]</span><span class="token punctuation">,</span> <span class="token string">'bilinear'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>  <span class="token comment" spellcheck="true">% resize im_data</span>
	im_data <span class="token operator">=</span> im_data <span class="token operator">-</span> mean_data<span class="token punctuation">;</span>  <span class="token comment" spellcheck="true">% subtract mean_data (already in W x H x C, BGR)</span>
	<span class="token comment" spellcheck="true">% oversample (4 corners, center, and their x-axis flips)</span>
	crops_data <span class="token operator">=</span> <span class="token function">zeros</span><span class="token punctuation">(</span>CROPPED_DIM<span class="token punctuation">,</span> CROPPED_DIM<span class="token punctuation">,</span> <span class="token number">3</span><span class="token punctuation">,</span> <span class="token number">10</span><span class="token punctuation">,</span> <span class="token string">'single'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	indices <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token number">0</span> IMAGE_DIM<span class="token operator">-</span>CROPPED_DIM<span class="token punctuation">]</span> <span class="token operator">+</span> <span class="token number">1</span><span class="token punctuation">;</span>
	n <span class="token operator">=</span> <span class="token number">1</span><span class="token punctuation">;</span>
	<span class="token keyword">for</span> <span class="token number">i</span> <span class="token operator">=</span> indices
	  <span class="token keyword">for</span> <span class="token number">j</span> <span class="token operator">=</span> indices
	    <span class="token function">crops_data</span><span class="token punctuation">(</span><span class="token operator">:</span><span class="token punctuation">,</span> <span class="token operator">:</span><span class="token punctuation">,</span> <span class="token operator">:</span><span class="token punctuation">,</span> n<span class="token punctuation">)</span> <span class="token operator">=</span> <span class="token function">im_data</span><span class="token punctuation">(</span><span class="token number">i</span><span class="token operator">:</span><span class="token number">i</span><span class="token operator">+</span>CROPPED_DIM<span class="token number">-1</span><span class="token punctuation">,</span> <span class="token number">j</span><span class="token operator">:</span><span class="token number">j</span><span class="token operator">+</span>CROPPED_DIM<span class="token number">-1</span><span class="token punctuation">,</span> <span class="token operator">:</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	    <span class="token function">crops_data</span><span class="token punctuation">(</span><span class="token operator">:</span><span class="token punctuation">,</span> <span class="token operator">:</span><span class="token punctuation">,</span> <span class="token operator">:</span><span class="token punctuation">,</span> n<span class="token operator">+</span><span class="token number">5</span><span class="token punctuation">)</span> <span class="token operator">=</span> <span class="token function">crops_data</span><span class="token punctuation">(</span><span class="token keyword">end</span><span class="token operator">:</span><span class="token operator">-</span><span class="token number">1</span><span class="token operator">:</span><span class="token number">1</span><span class="token punctuation">,</span> <span class="token operator">:</span><span class="token punctuation">,</span> <span class="token operator">:</span><span class="token punctuation">,</span> n<span class="token punctuation">)</span><span class="token punctuation">;</span>
	    n <span class="token operator">=</span> n <span class="token operator">+</span> <span class="token number">1</span><span class="token punctuation">;</span>
	  <span class="token keyword">end</span>
	<span class="token keyword">end</span>
	center <span class="token operator">=</span> <span class="token function">floor</span><span class="token punctuation">(</span><span class="token function">indices</span><span class="token punctuation">(</span><span class="token number">2</span><span class="token punctuation">)</span> <span class="token operator">/</span> <span class="token number">2</span><span class="token punctuation">)</span> <span class="token operator">+</span> <span class="token number">1</span><span class="token punctuation">;</span>
	<span class="token function">crops_data</span><span class="token punctuation">(</span><span class="token operator">:</span><span class="token punctuation">,</span><span class="token operator">:</span><span class="token punctuation">,</span><span class="token operator">:</span><span class="token punctuation">,</span><span class="token number">5</span><span class="token punctuation">)</span> <span class="token operator">=</span> <span class="token punctuation">...</span>
	  <span class="token function">im_data</span><span class="token punctuation">(</span>center<span class="token operator">:</span>center<span class="token operator">+</span>CROPPED_DIM<span class="token number">-1</span><span class="token punctuation">,</span>center<span class="token operator">:</span>center<span class="token operator">+</span>CROPPED_DIM<span class="token number">-1</span><span class="token punctuation">,</span><span class="token operator">:</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	<span class="token function">crops_data</span><span class="token punctuation">(</span><span class="token operator">:</span><span class="token punctuation">,</span><span class="token operator">:</span><span class="token punctuation">,</span><span class="token operator">:</span><span class="token punctuation">,</span><span class="token number">10</span><span class="token punctuation">)</span> <span class="token operator">=</span> <span class="token function">crops_data</span><span class="token punctuation">(</span><span class="token keyword">end</span><span class="token operator">:</span><span class="token operator">-</span><span class="token number">1</span><span class="token operator">:</span><span class="token number">1</span><span class="token punctuation">,</span> <span class="token operator">:</span><span class="token punctuation">,</span> <span class="token operator">:</span><span class="token punctuation">,</span> <span class="token number">5</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<ol start="10">
<li>network:
<ul>
<li>structure: <code>/models/bvlc_reference_caffenet/deploy.prototxt</code></li>
<li>parameters: <code>/models/bvlc_reference_caffenet/bvlc_reference_caffenet.caffemodel</code></li>
</ul>
<blockquote>
<p><code>% Initialize a network</code><br>
	<code>net = caffe.Net(net_model, net_weights, phase);</code></p>
</blockquote>
</li>
<li>prediction:<pre><code>scores = net.forward(input_data);
scores = scores{1};
scores = mean(scores, 2);  % take average scores over 10 crops
[~, maxlabel] = max(scores);
</code></pre>
</li>
<li>release network:<code>caffe.reset_all();</code></li>
</ol>
<hr>
<h3 id="pycaffe-使用">pycaffe 使用</h3>
<p><a href="http://blog.csdn.net/a_31415926/article/details/50532665">在windows下编译caffe的python接口</a><br>
总之，经过下面这三个过程，github包下面的python\caffe文件夹已经齐全了。</p>
<ol>
<li>
<p><code>extract_proto.bat</code>生成<code>python\caffe</code>下面的<code>caffe.proto</code>文件和<code>proto</code>文件夹。</p>
</li>
<li>
<p>VS2013编译pycaffe项目，同样也是在python\caffe这个文件夹下生成_caffe.pyd。</p>
</li>
<li>
<p><code>Pip</code>安装<code>google</code>的<code>protobuf</code>包(具体命令<code>pip install protobuf</code>)</p>
</li>
</ol>
<p>我们将这个caffe文件夹移到C:\Anaconda2\Lib\site-packages\下面，这个时候import caffe应该没有错误了。可以用示例代码跑跑看<br>
q: TypeError: <strong>init</strong>() got an unexpected keyword argument 'syntax’<br>
a: comment ./caffe-fast-rcnn/python/caffe/proto/caffe_pb2.py , all "systax = proto " line, fix it.Ha ha</p>
<h2 id="windows">Windows</h2>
<h3 id="如何快糙好猛地在windows下编译caffe并使用其matlab和python接口"><a href="http://blog.csdn.net/happynear/article/details/45372231"> 如何快糙好猛地在Windows下编译CAFFE并使用其matlab和python接口</a></h3>
<ol>
<li>准备
<ul>
<li>源码：<a href="https://www.github.com/happynear/caffe-windows">https://www.github.com/happynear/caffe-windows</a></li>
<li>百度云:<a href="http://pan.baidu.com/s/1bSzvKa">http://pan.baidu.com/s/1bSzvKa</a></li>
<li>cuda： 7.5</li>
<li>MKL</li>
</ul>
</li>
<li>编译<br>
　　编译非常简单，分为以下几步：<br>
　　1、双击./src/caffe/proto/extract_proto.bat批处理文件来生成caffe.pb.h和caffe.pb.cc两个c++文件，和caffe_pb2.py这个Python使用的文件。<br>
　　2、打开./buildVS2013/MainBuilder.sln，打开之后切换编译模式至Release X64模式。如果打开之后显示加载失败，可能你的CUDA版本和我的不一致，我的是CUDA 7.5版，这时就要用记事本打开./buildVS2013目录下各个文件夹内的.vcxproj文件，搜索CUDA 7.5，把这个7.5换成你自己的CUDA版本，就可以正常打开了。<br>
　　另外，如果你的显卡比较老或者没有显卡，请使用./build_cpu_only/MainBuilder.sln。<br>
　　3、点上边工具栏中的绿色三角编译吧。编译大概需要半小时左右，请耐心等待。<br>
	4、 修改<code>matcaffe</code>和<code>pycaffe</code>工程的<code>include</code>and <code>lib</code>目录<br>
	编译需要</li>
</ol>
<p>3.测试</p>
<p>到 <a href="http://pan.baidu.com/s/1mgl9ndu">http://pan.baidu.com/s/1mgl9ndu</a> 下载已经转换好的MNIST的leveldb数据文件，解压至./examples/mnist文件夹中，然后运行根目录下的run_mnist.bat即可开始训练，训练日志会保存在./log文件夹中，以INFO开头，txt格式的日志文件中。</p>
<p>ps：如果你编译成功的话，不要忘了给我的github工程点个star！</p>
<ol start="4">
<li><a href="https://github.com/BVLC/caffe/tree/windows">window-caffe</a></li>
</ol>
<hr>
<p>nuget下载出错</p>
