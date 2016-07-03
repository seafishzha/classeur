<h1 id="distortion--stitching">Distortion + Stitching</h1>
<h2 id="distortion">Distortion</h2>
<h3 id="theory-from-opencv">1.  <a href="http://docs.opencv.org/master/d4/d94/tutorial_camera_calibration.html">Theory from OpenCV</a></h3>
<p>For the distortion OpenCV takes into account the radial and tangential factors. For the radial factor one uses the following formula:<br>
<script type="math/tex; mode=display" id="MathJax-Element-307">
x_{distorted} = x( 1 + k_1 r^2 + k_2 r^4 + k_3 r^6) \\ y_{distorted} = y( 1 + k_1 r^2 + k_2 r^4 + k_3 r^6)
</script></p>
<p>So for an undistorted pixel point at<script type="math/tex" id="MathJax-Element-134">(x,y)</script>coordinates, its position on the distorted image will be <script type="math/tex" id="MathJax-Element-135">(x_{distorted},y_{distorted})</script>. The presence of the radial distortion manifests in form of the “barrel” or “fish-eye” effect.</p>
<p>Tangential distortion occurs because the image taking lenses are not perfectly parallel to the imaging plane. It can be represented via the formulas:<br>
\[x_{distorted} = x + [ 2p_1xy + p_2(r^2+2x^2)] \\ y_{distorted} = y + [ p_1(r^2+ 2y^2)+ 2p_2xy]\]</p>
<p>So we have five distortion parameters which in OpenCV are presented as one row matrix with 5 columns:<br>
\[distortion\_coefficients=(k_1 \hspace{10pt} k_2 \hspace{10pt} p_1 \hspace{10pt} p_2 \hspace{10pt} k_3)\]</p>
<p>now for the unit conversion we use the following formula:<br>
<script type="math/tex; mode=display" id="MathJax-Element-142">
\left [ \begin{matrix} x \\ y \\ w \end{matrix} \right ] = \left [ \begin{matrix} f_x & 0 & c_x \\ 0 & f_y & c_y \\ 0 & 0 & 1 \end{matrix} \right ] \left [ \begin{matrix} X \\ Y \\ Z \end{matrix} \right ]
</script></p>
<p>Here the presence of <script type="math/tex" id="MathJax-Element-233">w</script> is explained by the use of homography coordinate system (and <script type="math/tex" id="MathJax-Element-234">w=Z</script>). The unknown parameters are <script type="math/tex" id="MathJax-Element-235">f_x</script> and <script type="math/tex" id="MathJax-Element-236">f_y</script> (camera focal lengths) and <script type="math/tex" id="MathJax-Element-237">(c_x,c_y)</script> which are the optical centers expressed in pixels coordinates. If for both axes a common focal length is used with a given a aspect ratio (usually 1), then <script type="math/tex" id="MathJax-Element-238">f_y=f_x∗a</script> and in the upper formula we will have a single focal length <script type="math/tex" id="MathJax-Element-239">f</script>. The matrix containing these four parameters is referred to as the camera matrix. While the distortion coefficients are the same regardless of the camera resolutions used, these should be scaled along with the current resolution from the calibrated resolution.</p>
<p>更多理论课参考wiki： <a href="https://en.wikipedia.org/wiki/Camera_resectioning">Camera resectioning</a></p>
<h3 id="implementation">2.  Implementation</h3>
<p>Blog: <a href="http://www.theeminentcodfish.com/gopro-calibration/">GoPro Lens Distortion Removal</a></p>
<h4 id="step-1--collecting-calibration-images">Step 1:  Collecting calibration images</h4>
<p><code>bool ImageCollect(int n_boards)</code><br>
‘n_boards:’ 表示实际收集图像的个数。</p>
<h4 id="step-2-calibration">Step 2: Calibration</h4>
<p><code>int runCalibrationAndSave(const int n_boards, const int board_w = 9, const int board_h = 6, float squareSize = 20)</code><br>
<code>board_w, board_h</code> 矫正板内角点的的个数<br>
<code>squareSize</code>矫正板一个方块对应的实际长度（单位是mm）<br>
结果存储为一个<code>.xml</code>文件<br>
主要为：<br>
<code>camera_matrix:</code></p>
<p>学到相机矩阵为：<br>
<script type="math/tex; mode=display" id="MathJax-Element-140">
\left[ \begin{matrix} 537.65& 0. &340.11 \\
0.&   537.89 &236.94 \\
  0 & 0 & 1 
  \end{matrix} \right]
</script></p>
<p><code>distortion_coefficients</code><br>
<script type="math/tex; mode=display" id="MathJax-Element-297">[-0.2776, 0.0539, 0.0212, -0.0039,  0.0486]</script></p>
<h4 id="step-3-undistorting">Step 3: Undistorting</h4>
<p><code>int undistortImages_test()</code></p>
<ol>
<li>生产映射矩阵<code>xmap</code>和<code>ymap</code>:<br>
<code>Mat map1, map2; initUndistortRectifyMap(cameraMatrix, distCoeffs, Mat(), 	getOptimalNewCameraMatrix(cameraMatrix, distCoeffs, imageSize, 1, imageSize, 0), 	imageSize,CV_16SC2, map1, map2);</code></li>
<li>图像矫正：图像插值实现。<br>
<code>remap(image, rimg, map1, map2, INTER_LINEAR);</code></li>
</ol>
<h4 id="testing：">testing：</h4>
<p>机器：thinkpad 笔记本：CPU（ i7-3520M） 2.9G， RAM： 8G）<br>
环境： vs2013 + OpenCV3.0<br>
对于**<code>640*480</code>**的图像矫正所需时间： \(&lt;1.5ms\)</p>
