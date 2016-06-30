<h1 id="object-proposals">Object Proposals</h1>
<h2 id="survey">survey</h2>
<ol>
<li><a href="https://filebox.ece.vt.edu/~aroma/web/object-proposals.html#code_dataset">Object-Proposal Evaluation Protocol is ‘Gameable’.</a><br>
Neelima Chavali, Harsh Agrawal, Aroma Mahendru, Dhruv Batra @[CVPR2016]<br>
评估框架：Matlab code [github:] (<a href="https://github.com/batra-mlp-lab/object-proposals">https://github.com/batra-mlp-lab/object-proposals</a>)</li>
<li>What makes for effective detection proposals?,J. Hosang, R. Benenson, Piotr Dollár, B. Schiele,  BMVC2014, PAMI2015<br>
Matlab Code: <a href="https://github.com/hosang/detection-proposals">github</a></li>
</ol>
<h2 id="selective-search-for-object-recognition">Selective Search for Object Recognition</h2>
<p><a href="http://koen.me/research/selectivesearch/">project:</a><br>
<a href="https://github.com/Itseez/opencv_contrib/tree/master/modules/ximgproc">OpenCV:</a><br>
<a href="https://github.com/belltailjp/selective_search_py">Python:</a></p>
<blockquote>
<p>Selective Search for Object Recognition    uijlings_ijcv2013_draft.pdf<br>
Jasper R. R. Uijlings, Koen E. A. van de Sande, Theo Gevers, Arnold W. M. Smeulders<br>
International Journal of Computer Vision, Volume 104 (2), page 154-171, 2013</p>
</blockquote>
<blockquote>
<p>Segmentation As Selective Search for Object Recognition    vandesande_iccv2011.pdf<br>
Koen E. A. van de Sande, Jasper R. R. Uijlings, Theo Gevers, Arnold W. M. Smeulders<br>
IEEE International Conference on Computer Vision, 2011</p>
</blockquote>
<h3 id="中文博客：">中文博客：</h3>
<ol>
<li><a href="http://blog.csdn.net/surgewong/article/details/39316931">Surge</a></li>
<li><a href="http://zhangliliang.com/2014/07/17/paper-note-selective-search/">在路上:</a></li>
</ol>
<hr>
<h3 id="核心思想">核心思想</h3>
<p>由图像分割合并构成可能存在目标的区域，然后利用SVM学习分类器，对目标定位。</p>
<ol start="3">
<li>候选区域：
<ul>
<li>图像分割：Efficient Graph-Based Image Segmentation</li>
<li>区域合并：多样化策略
<ul>
<li>颜色空间</li>
<li>相似度度量</li>
</ul>
</li>
</ul>
</li>
</ol>
<p><img src="http://img.blog.csdn.net/20140917092806522?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvc3VyZ2V3b25n/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast" alt=""></p>
<ol start="4">
<li>物体识别：
<ul>
<li>特征提取：HOG（Histograms of oriented gradients）和 bag-of-words</li>
<li>分类器训练：SVM</li>
</ul>
</li>
</ol>
<h2 id="bing">Bing</h2>
<p><a href="https://github.com/bittnt/Objectness/tree/master/Src">github:</a><br>
This is the 1000 FPS BING objectness linux version library for efficient objectness proposal estimator,We would appreciate if you could cite and refer to the papers below.</p>
<blockquote>
<p>@inproceedings{BingObj2014,<br>
title={{BING}: Binarized Normed Gradients for Objectness Estimation at 300fps},<br>
author={Ming-Ming Cheng and Ziming Zhang and Wen-Yan Lin and Philip H. S. Torr},<br>
booktitle={IEEE CVPR},<br>
year={2014},<br>
}<br>
@inproceedings{depthobjectproposals_GCPR2015,<br>
author = {Shuai Zheng and Victor Adrian Prisacariu and Melinos Averkiou and Ming-Ming Cheng and Niloy J. Mitra and Jamie Shotton and Philip H. S. Torr and Carsten Rother},<br>
title = {Object Proposal Estimation in Depth Images using Compact 3D Shape Manifolds},<br>
booktitle = {German Conference on Pattern Recognition (GCPR)},<br>
year = {2015}<br>
}</p>
</blockquote>
<p>Third party resources.</p>
<p>If you have made a version running on other platforms (Software at other platforms, e.g. Mac, Linux, vs2010, makefile projects) and want to share it with others, please send me an email containing the url and I will add a link here. Notice, these third party versions may or may not contain updates and bug fix, which I provided in the next section of this webpage for easier updates.</p>
<p><a href="https://github.com/bittnt/Objectness#objectness">Linux version</a> of this work provided by Shuai Zheng from the University of Oxford.<br>
<a href="https://bitbucket.org/robotvault/bingfeatures/overview">Linux version</a> of this work provided by Dr. Ankur Handa from the University of Cambridge.<br>
<a href="https://github.com/fpuja/opencv_contrib/tree/saliencyModuleDevelop/modules/saliency">OpenCV version (doc)</a> of this work by Francesco Puja et al.<br>
<a href="https://github.com/tfzhou/BINGObjectness">Matlab version</a> of this work by Tianfei Zhou from Beijing Institute of Technology<br>
<a href="https://github.com/nhlijiaming/BINGObjectness">Matlab version</a> (work with 64 bit Win7 &amp; visual studio 2012) provided by Jiaming Li from University of Electronic Science and Technology of China(UESTC).</p>
<p><a href="https://github.com/tolga-b/BINGpp">Bing++</a>:  利用edge信息提高bounding box的精度。</p>
<h2 id="edgebox">EdgeBox</h2>
<h3 id="edge-boxes-locating-object-proposals-from-edges">1. <a href="https://github.com/pdollar/edges">Edge Boxes: Locating Object Proposals from Edges</a></h3>
<p>Very fast edge detector (up to <strong>60 fps</strong> depending on parameter settings) that achieves excellent accuracy. Can serve as input to any vision algorithm requiring high quality <strong>edge maps</strong>. Toolbox also includes the <strong>Edge Boxes object proposal</strong> generation method and fast superpixel code.</p>
<blockquote>
<p>@inproceedings{DollarICCV13edges,<br>
author    = {Piotr Doll’ar and C. Lawrence Zitnick},<br>
title     = {Structured Forests for Fast Edge Detection},<br>
booktitle = {ICCV},<br>
year      = {2013},<br>
}</p>
</blockquote>
<p>@article{DollarARXIV14edges,<br>
author    = {Piotr Doll’ar and C. Lawrence Zitnick},<br>
title     = {Fast Edge Detection Using Structured Forests},<br>
journal   = {ArXiv},<br>
year      = {2014},<br>
}</p>
<p>@inproceedings{ZitnickECCV14edgeBoxes,<br>
author    = {C. Lawrence Zitnick and Piotr Doll’ar},<br>
title     = {Edge Boxes: Locating Object Proposals from Edges},<br>
booktitle = {ECCV},<br>
year      = {2014},<br>
}</p>
<h2 id="detection-with-object-proposals">Detection with object proposals</h2>
<h3 id="cnn-object-proposal-models-for-salient-object-detection">1. CNN Object Proposal Models for Salient Object Detection</h3>
<p>CNN models for the following CVPR’16 paper:</p>
<blockquote>
<p>Unconstrained Salient Object Detection via Proposal Subset Optimization<br>
J. Zhang, S. Sclaroff, Z. Lin, X. Shen, B. Price and R. Mech.<br>
CVPR, 2016.</p>
</blockquote>
<p>[PDF:] (<a href="http://cs-people.bu.edu/jmzhang/SOD/CVPR16SOD_camera_ready.pdf">http://cs-people.bu.edu/jmzhang/SOD/CVPR16SOD_camera_ready.pdf</a>)<a href="http://cs-people.bu.edu/jmzhang/sod.html">Webpage:</a><br>
<a href="https://github.com/jimmie33/SOD">github:</a></p>
<p>The following models are finetuned on the <a href="http://cs-people.bu.edu/jmzhang/sos.html">Salient Object Subitizing dataset</a> (~5000 images) with bounding box annotations:</p>
<p><a href="https://gist.github.com/jimmie33/509111f8a00a9ece2c3d5dde6a750129">VGG16</a>: This model is used in the paper.<br>
<a href="https://gist.github.com/jimmie33/339fd0a938ed026692267a60b44c0c58">GoogleNet:</a> This model is smaller, faster and slightly better than the VGG16 model.<br>
It is recommended that you download the full system here, which will automatically download all the needed models and data.</p>
<h3 id="faster-r-cnn-towards-real-time-object-detection-with-region-proposal-networks">2. <a href="(https://github.com/ShaoqingRen/faster_rcnn)">Faster R-CNN: Towards Real-Time Object Detection with Region Proposal Networks</a></h3>
<p><strong>Faster R-CNN</strong> is an object detection framework based on deep convolutional networks, which includes a <strong>Region Proposal Network (RPN)</strong> and an <strong>Object Detection Network.</strong> Both networks are trained for <strong>sharing convolutional layers</strong> for fast testing.</p>
<p>Faster R-CNN was initially described in an <a href="http://arxiv.org/abs/1506.01497">arXiv tech report.</a></p>
<p>This repo contains a MATLAB re-implementation of Fast R-CNN. Details about Fast R-CNN are in: <a href="https://github.com/rbgirshick/fast-rcnn">rbgirshick/fast-rcnn.</a></p>
<p>This code has been tested on Windows 7/8 64-bit, Windows Server 2012 R2, and Linux, and on MATLAB 2014a.</p>
<blockquote>
<p>@article{ren15fasterrcnn,<br>
Author = {Shaoqing Ren, Kaiming He, Ross Girshick, Jian Sun},<br>
Title = {{Faster R-CNN}: Towards Real-Time Object Detection with Region Proposal Networks},<br>
Journal = {arXiv preprint arXiv:1506.01497},<br>
Year = {2015}<br>
}</p>
</blockquote>
<h2 id="tracking-with-object-proposals">Tracking with object proposals</h2>
<ol>
<li><a href="http://arxiv.org/abs/1501.00909">Adaptive Objectness for Object Tracking</a><br>
IDEA：利用bing特征online训练SVM分类器，对目标进行跟踪。<br>
疑问：bing特征本来是用来学习目标与非目标的轮廓，表征能力较弱，直接用来跟踪的话，很难区分目标和背景。</li>
<li>Beyond Local Search: Tracking Objects Everywhere with Instance-Specific Proposals<br>
<a href="https://arxiv.org/abs/1605.01839">arxiv: PDF</a>
<blockquote>
<p>G. Zhu, F. Porikli, and H. Li, “Beyond local search: Tracking objects everywhere with Instance-specic proposals,” in IEEE Conference on Computer Vision and Pattern Recognition (CVPR), 2016.</p>
</blockquote>
</li>
</ol>
<p><img src="https://static.wixstatic.com/media/482d38_9492cc3ff82c48d29c9f41abd0472e6d.jpg/v1/fill/w_247,h_101,al_c,q_80,usm_0.66_1.00_0.01/482d38_9492cc3ff82c48d29c9f41abd0472e6d.jpg" alt=""><br>
Method：<br>
	- 利用EdgeBox或者BING在整副图像上，提取可能是目标的区域；<br>
	- 利用2640-D的直方图作为特征，利用Structure SVM进行分类。</p>
<ol start="3">
<li>Robust visual tracking with deep convolutional neural network based object proposals on PETS</li>
</ol>
<blockquote>
<p>G. Zhu, F. Porikli, and H. Li, “Robust visual tracking with deep convolutional neural network based object proposals on PETS,” in IEEE Conference on Computer Vision and Pattern Recognition Workshop (CVPRW), 2016.<br>
<a href="http://120.52.73.10/www.cv-foundation.org/openaccess/content_cvpr_2016_workshops/w20/papers/Zhu_Robust_Visual_Tracking_CVPR_2016_paper.pdf">Paper:</a><br>
<img src="https://static.wixstatic.com/media/482d38_a6691fc90ee84b6ea75de13953d2190e.jpg/v1/fill/w_247,h_106,al_c,q_80,usm_0.66_1.00_0.01/482d38_a6691fc90ee84b6ea75de13953d2190e.jpg" alt=""></p>
</blockquote>
<p>Method:<br>
利用Faster R-CNN中的 RPN网络获得object proposals， 然后在进行跟踪。</p>
