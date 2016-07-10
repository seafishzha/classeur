<h1 id="caffe-使用">Caffe 使用</h1>
<h2 id="ubuntu">Ubuntu</h2>
<h3 id="ubuntu-安装-caffe">ubuntu 安装 caffe</h3>
<p><a href="http://coldmooon.github.io/2015/08/03/caffe_install/">从零安装caffe（ubuntu4.04）</a></p>
<p>注意事项：</p>
<ol>
<li>GPU使用</li>
<li>matlab 路径</li>
<li>python 路径</li>
<li>Make 的使用 <code>make all -j8``make test -j8</code></li>
<li>g++降级：
<ul>
<li>下载gcc/g++ 4.7.x<br>
<code>$ sudo apt-get install -y gcc-4.7</code><br>
<code>$ sudo apt-get install -y g++-4.7</code><br>
`- 链接gcc/g++实现降级</li>
</ul>
</li>
</ol>
<pre><code>	$ cd /usr/bin
	$ sudo rm gcc
	$ sudo ln -s gcc-4.7 gcc
	$ sudo rm g++
	$ sudo ln -s g++-4.7 g++
	``


-----------------------
### MatCaffe 使用
6. 下载库：在[github](https://github.com/BVLC/caffe)对应的`model`中链接
7. read image: 
</code></pre>
<p>im = imred(‘caffe/examples/images/cap.jpg’);<br>
[scores, maxlabel] = classification_demo(im, 0);</p>
<pre><code>workspace 
</code></pre>
<p>Elapsed time is 0.015581 seconds<br>
Elapsed time is 1.274006 seconds</p>
<pre><code>
------------------------
&gt;`classification_demo`

-------------------
8. data:
	- matlab: height * width *chanels(RGB)
	- caffe: [width * height * channels(BGR)*images]
	- code:
	
```matlab
	
	im_data = im(:, :, [3, 2, 1]);  % permute channels from RGB to BGR
	im_data = permute(im_data, [2, 1, 3]);  % flip width and height
	im_data = single(im_data);  % convert from uint8 to single

	%% resize + oversample
	im_data = imresize(im_data, [IMAGE_DIM IMAGE_DIM], 'bilinear');  % resize im_data
	im_data = im_data - mean_data;  % subtract mean_data (already in W x H x C, BGR)
	% oversample (4 corners, center, and their x-axis flips)
	crops_data = zeros(CROPPED_DIM, CROPPED_DIM, 3, 10, 'single');
	indices = [0 IMAGE_DIM-CROPPED_DIM] + 1;
	n = 1;
	for i = indices
	  for j = indices
	    crops_data(:, :, :, n) = im_data(i:i+CROPPED_DIM-1, j:j+CROPPED_DIM-1, :);
	    crops_data(:, :, :, n+5) = crops_data(end:-1:1, :, :, n);
	    n = n + 1;
	  end
	end
	center = floor(indices(2) / 2) + 1;
	crops_data(:,:,:,5) = ...
	  im_data(center:center+CROPPED_DIM-1,center:center+CROPPED_DIM-1,:);
	crops_data(:,:,:,10) = crops_data(end:-1:1, :, :, 5);
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
