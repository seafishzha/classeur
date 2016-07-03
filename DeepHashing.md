<h1 id="deep-hashing">Deep Hashing</h1>
<h2 id="kevin-ke-yun-lin">Kevin (Ke-Yun) Lin</h2>
<p>Homepage：<a href="https://sites.google.com/site/kevinlin311tw/">https://sites.google.com/site/kevinlin311tw/</a><br>
github：<a href="https://github.com/kevinlin311tw">https://github.com/kevinlin311tw</a></p>
<h3 id="learning-compact-binary-descriptors-with-unsupervised-deep-neural-networks">Learning Compact Binary Descriptors with Unsupervised Deep Neural Networks</h3>
<p><img src="https://sites.google.com/site/kevinlin311tw/_/rsrc/1459070870264/me/cvpr16.png?height=158&amp;width=200" alt=""></p>
<p><img src="http://handong1587.github.io/assets/image_retrieval/DeepBit.jpg" alt=""></p>
<h4 id="introduction">Introduction</h4>
<p>We propose a new <strong>unsupervised deep learning</strong> approach to learn compact binary descriptor.<br>
We enforce three criterions on binary codes which are learned at the top layer of our network:</p>
<ol>
<li>minimal loss quantization;</li>
<li>evenly distributed codes;</li>
<li>rotation invariant bits.<br>
Then, we learn the parameters of the networks with a <strong>back-propagation</strong> technique.<br>
Experimental results on three different visual analysis tasks including image matching, image retrieval, and object recognition demonstrate the effectiveness of the proposed approach.</li>
</ol>
<p>点评：利用无监督学习，首先在vgg16模型基础上学习量化损失和均匀分布，对Vgg16模型参数调优，然后在学习旋转不变的patch， 进一步调优。</p>
<p>The details can be found in the following <a href="http://www.iis.sinica.edu.tw/~kevinlin311.tw/cvpr16-deepbit.pdf">CVPR 2016 paper</a></p>
<h4 id="codes">codes</h4>
<p>github: <a href="https://github.com/kevinlin311tw/cvpr16-deepbit">https://github.com/kevinlin311tw/cvpr16-deepbit</a></p>
<ol>
<li>MATLAB (tested with 2015a on 64-bit Ubuntu)</li>
<li>Caffe’s prerequisites</li>
</ol>
<blockquote>
<p>Learning Compact Binary Descriptors with Unsupervised Deep Neural Networks<br>
Kevin Lin, Jiwen Lu, Chu-Song Chen and Jie Zhou<br>
IEEE Conference on Computer Vision and Pattern Recognition (CVPR), 2016</p>
</blockquote>
<h3 id="deep-learning-of-binary-hash-codes-for-fast-image-retrieval">Deep Learning of Binary Hash Codes for Fast Image Retrieval</h3>
<blockquote>
<p>Deep Learning of Binary Hash Codes for Fast Image Retrieval<br>
K. Lin, H.-F. Yang, J.-H. Hsiao, C.-S. Chen<br>
CVPR Workshop (CVPRW) on Deep Learning in Computer Vision, DeepVision 2015, June 2015.<br>
Rapid Clothing Retrieval via Deep Learning of Binary Codes and Hierarchical Search<br>
K. Lin, H.-F. Yang, K.-H. Liu, J.-H. Hsiao, C.-S. Chen<br>
ACM International Conference on Multimedia Retrieval, ICMR 2015, June 2015.</p>
</blockquote>
<p><img src="https://sites.google.com/site/kevinlin311tw/_/rsrc/1459071308576/me/cvprw15.jpg?height=150&amp;width=200" alt=""></p>
<h4 id="introduction-1">Introduction</h4>
<p>We present a simple yet effective deep learning framework to create the hash-like binary codes for fast image retrieval. We add a <strong>latent-attribute layer</strong> in the deep CNN to simultaneously learn domain specific image representations and a set of hash-like functions. Our method does not rely on pairwised similarities of data and is highly scalable to the dataset size.</p>
<p>the paper is in <a href="http://www.iis.sinica.edu.tw/~kevinlin311.tw/cvprw15.pdf">CVPRW 2015 paper</a> and the <a href="http://www.csie.ntu.edu.tw/~r01944012/deepworkshop-slide.pdf">slides</a></p>
<p>点评：在<code>F7</code>和<code>F8</code>之间增加隐含层<code>H</code>，</p>
<h4 id="code">Code</h4>
<p>github： <a href="https://github.com/kevinlin311tw/caffe-cvprw15">https://github.com/kevinlin311tw/caffe-cvprw15</a></p>
<ol>
<li>MATLAB (tested with 2012b on 64-bit Linux)</li>
<li>Caffe’s prerequisites</li>
</ol>
<h2 id="yan-pan">Yan Pan</h2>
<p>homepage：<a href="http://ss.sysu.edu.cn/~py/">http://ss.sysu.edu.cn/~py/</a></p>
<h3 id="supervised-hashing-for-image-retrieval-via-image-representation-learning">Supervised Hashing for Image Retrieval via Image Representation Learning</h3>
<blockquote>
<p>Supervised Hashing for Image Retrieval via Image Representation Learning<br>
Rongkai Xia (third-year master student), Yan Pan*, Hanjiang Lai, Cong Liu, and Shuicheng Yan<br>
In Proceedings of AAAI Conference on Artificial Intelligence (AAAI), 2014</p>
</blockquote>
<p>paper: <a href="http://ss.sysu.edu.cn/~py/papers/AAAI-CNNH.pdf">http://ss.sysu.edu.cn/~py/papers/AAAI-CNNH.pdf</a><br>
PPT: <a href="http://ss.sysu.edu.cn/~py/CNNH-slides.pdf">http://ss.sysu.edu.cn/~py/CNNH-slides.pdf</a></p>
<p><img src="http://www.36dsj.com/wp-content/uploads/2016/06/1871.jpg" alt=""></p>
<h4 id="method">Method:</h4>
<ul>
<li>step1: 通过对相似度矩阵（矩阵中的每个元素指示对应的两个样本是否相似）进行分解，得到样本的二值编码</li>
<li>step2: 利用CNN对得到的二值编码进行拟合;
<ul>
<li>多标签预测问题 — 交叉熵损失</li>
<li>分类的损失函数  — softmax</li>
</ul>
</li>
</ul>
<blockquote>
<p>conclusion: 尽管实验中CNNH相比传统的基于手工设计特征的方法取得了显著的性能提升，但是这个方法仍然不是<strong>端到端</strong>的方法，学到的图像表示不能反作用于二值编码的更新，因此并不能完全发挥出深度学习的能力。</p>
</blockquote>
<h3 id="simultaneous-feature-learning-and-hash-coding-with-deep-neural-networks">Simultaneous Feature Learning and Hash Coding with Deep Neural Networks</h3>
<blockquote>
<p>Simultaneous Feature Learning and Hash Coding with Deep Neural Networks<br>
Hanjiang Lai, Yan Pan*, Ye Liu, and Shuicheng Yan<br>
In Proceedings of IEEE International Conference on Pattern Recognition and Computer Vision (CVPR), 2015</p>
</blockquote>
<p>paper: <a href="http://arxiv.org/abs/1504.03410">http://arxiv.org/abs/1504.03410</a></p>
<p><img src="http://www.36dsj.com/wp-content/uploads/2016/06/1881.jpg" alt=""></p>
<p>Method:</p>
<ol>
<li>网络使用三张图像构成的三元组进行训练。</li>
<li>损失函数:Hamming空间中，相似样本间的距离小于不相似样本间的距离</li>
<li>网络结构
<ul>
<li>为了减小二值码不同bit之间的冗余性，作者提出使用部分连接层代替全连接层，每个部分负责学习一个bit，各部分之间无连接;</li>
<li>为了避免二值码学习中的离散取值约束，像大多数哈希方法一样，作者使用sigmoid激活函数将离散约束松弛为范围约束（{0,1}→(0,1)），同时为了保持学到的特征空间和Hamming空间相似，引入了分段量化函数;</li>
</ul>
</li>
</ol>
<h2 id="liang-lin">liang lin</h2>
<p>homepage : <a href="http://ss.sysu.edu.cn/~ll/">http://ss.sysu.edu.cn/~ll/</a></p>
<h3 id="bit-scalable-deep-hashing">Bit-Scalable Deep Hashing</h3>
<blockquote>
<p>Ruimao Zhang, Liang Lin, Rui Zhang, Wangmeng Zuo, Lei Zhang. Bit-Scalable Deep Hashing with Regularized Similarity Learning for Image Retrieval and Person Re-identification. TIP 2015.</p>
</blockquote>
<p>Project: <a href="http://vision.sysu.edu.cn/projects/deephashing/">http://vision.sysu.edu.cn/projects/deephashing/</a><br>
Code :<a href="https://github.com/ruixuejianfei/BitScalableDeepHash/">https://github.com/ruixuejianfei/BitScalableDeepHash/</a></p>
<p><img src="http://vision.sysu.edu.cn/vision_sysu/wp-content/uploads/2015/08/framework-1024x594.jpg" alt=""></p>
<h4 id="introduction-2">Introduction</h4>
<ol>
<li>基于三元组的损失</li>
<li>使用图像对（image pair）之间的相似性作为正则项</li>
<li>网络学习: 加权Hamming距离</li>
</ol>
<h2 id="wujun-li">wujun li</h2>
<p>homepage : <a href="http://cs.nju.edu.cn/lwj/">http://cs.nju.edu.cn/lwj/</a><br>
Learning to Hash: <a href="http://cs.nju.edu.cn/lwj/L2H.html">http://cs.nju.edu.cn/lwj/L2H.html</a></p>
<h3 id="feature-learning-based-deep-supervised-hashing-with-pairwise-labels">Feature Learning based Deep Supervised Hashing with Pairwise Labels</h3>
<blockquote>
<p>Feature Learning based Deep Supervised Hashing with Pairwise Labels.<br>
Wu-Jun Li, Sheng Wang*, Wang-Cheng Kang*.<br>
To Appear in Proceedings of the 25th International Joint Conference on Artificial Intelligence (IJCAI), 2016.</p>
</blockquote>
<p>Paper: <a href="http://cs.nju.edu.cn/lwj/paper/IJCAI16_DPSH.pdf">http://cs.nju.edu.cn/lwj/paper/IJCAI16_DPSH.pdf</a><br>
Code： VGG convnetmat</p>
<h4 id="introduction-3">Introduction:</h4>
<p>simultaneous feature learning and hash code learning for applications with pairwise labels.</p>
