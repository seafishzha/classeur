<h1 id="detection">Detection</h1>
<hr>
<h2 id="good-resource">Good Resource:</h2>
<h3 id="object-detection-resources">object detection resources:</h3>
<ul>
<li>detection lists:<br>
<a href="http://handong1587.github.io/deep_learning/2015/10/09/object-detection.html">http://handong1587.github.io/deep_learning/2015/10/09/object-detection.html</a></li>
<li>深度学习大讲堂：<br>
<a href="http://mp.weixin.qq.com/s?__biz=MzI1NTE4NTUwOQ==&amp;mid=2650325043&amp;idx=1&amp;sn=bd016d98a40e8cf7d53ee674f201b4a7#rd">http://mp.weixin.qq.com/s?__biz=MzI1NTE4NTUwOQ==&amp;mid=2650325043&amp;idx=1&amp;sn=bd016d98a40e8cf7d53ee674f201b4a7#rd</a></li>
</ul>
<hr>
<h2 id="detection-1">Detection</h2>
<h3 id="r-fcn-object-detection-via-region-based-fully-convolutional-networks">R-FCN: Object Detection via Region-based Fully Convolutional Networks</h3>
<p>homepage:<a href="http://kaiminghe.com/">http://kaiminghe.com/</a><br>
github:<a href="https://github.com/daijifeng001/r-fcn">https://github.com/daijifeng001/r-fcn</a></p>
<hr>
<h3 id="faster-r-cnn">faster R-CNN:</h3>
<ul>
<li></li>
<li>matlab code: <a href="https://github.com/ShaoqingRen/faster_rcnn">https://github.com/ShaoqingRen/faster_rcnn</a></li>
</ul>
<hr>
<h3 id="ssd-single-shot-multibox-detector">SSD: Single Shot MultiBox Detector</h3>
<p>homepage:<a href="http://www.cs.unc.edu/~wliu/">http://www.cs.unc.edu/~wliu/</a><br>
github: <a href="https://github.com/weiliu89/caffe/tree/ssd">https://github.com/weiliu89/caffe/tree/ssd</a><br>
blog:<a href="http://blog.csdn.net/cv_family_z/article/details/51907328">http://blog.csdn.net/cv_family_z/article/details/51907328</a></p>
<h4 id="contribution">1.contribution:</h4>
<ul>
<li>速度快: 58 fps</li>
<li>效果好: 75.1%</li>
</ul>
<h4 id="method">2. method:</h4>
<p><img src="http://img.blog.csdn.net/20160714093147693" alt=""><br>
VGG + Multi-scale feature maps</p>
<hr>
<h3 id="locnet-improving-localization-accuracy-for-object-detection">LocNet: Improving Localization Accuracy for Object Detection</h3>
<p>homepage:<a href="http://imagine.enpc.fr/~komodakn/">http://imagine.enpc.fr/~komodakn/</a><br>
github:<a href="https://github.com/gidariss/LocNet">https://github.com/gidariss/LocNet</a><br>
blog:<a href="http://blog.csdn.net/cv_family_z/article/details/52047262">http://blog.csdn.net/cv_family_z/article/details/52047262</a></p>
<blockquote>
<p>problem: 提升检测框与目标的吻合度，特别是当IOU比较大时</p>
</blockquote>
<p>method:<br>
<img src="http://img.blog.csdn.net/20160727164500329" alt=""><br>
检测方法步骤：<br>
1.给定候选框，分配置信度；<br>
2.给定候选框，放大得到搜索区域，迭代得到新的更接近目标的候选框，</p>
<blockquote>
<p>检测结果：结果主要是在IOU&gt;0.65时与bbox回归相比，与实际目标的吻合度更高，这个方法对于需要精确目标位置的应用应该有帮助，</p>
</blockquote>
<blockquote>
<p>后续工作： Attend Refine Repeat: Active Box Proposal Generation via In-Out Localization<br>
<a href="https://github.com/gidariss/AttractioNet">https://github.com/gidariss/AttractioNet</a></p>
</blockquote>
