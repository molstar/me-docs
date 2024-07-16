#### Main Settings
<img src="../img/viewportsettings.png" align="left" width="300px"/>
<br>This panel allows fine-tuning of the viewport rendering effects and camera options:<br>
- **Animate**: Rock (shortcut `o`) or Spin (shortcut `i`) the camera around the current pivot (camera center) at a given speed and angle<br>
- **Camera**: Perspective or Orthographic camera projection. Hide/Show the Axes. Enable Stereo rendering<br>
- **Background**: Change the Background Color<br>
- **Occlusion**: Enable/Disable Ambient Occlusion<br>
- **Shadow**: Enable/Disable Shadow<br>
- **Outline**: Enable/Disable Outline<br>
- **DoF**: Enable/Disable Depth Of Field<br>
- **Fog**: Enable/Disable Fog<br>
- **Clipping**: Adjust camera front clipping plane<br>
- **Layout**: Enable/Disable the Left and Right panel visibility<br>

<br clear="left"/>

##### Ambient Occlusion
Ambient occlusion is a shading and rendering technique used to calculate how exposed each point in a scene is to ambient lighting. In molecular graphics, this technique enhances the perception of depth and shape of molecules. In Mol\*, the effect is achieved using the screen space ambient occlusion (SSAO) algorithm. The SSAO algorithm is implemented as a pixel shader, analyzing the scene depth buffer which is stored in a texture for which we can control the *Resolution Scale*. For every pixel on the screen, the pixel shader samples the depth values between the *Near* and *Far threshold* around the current pixel at a given *Radius* and tries to compute the amount of occlusion from each of the sampled points. The final occlusion factor can be adjusted using a *Bias* and is applied by mixing the given *Color*. This effect is not sufficient for large scenes with different objects of different scales. This is why we added the **Multi Scale** option, which can apply the SSAO effect for different levels of Radius and Bias.

SSAO                       |  Multiscale SSAO
:-------------------------:|:-------------------------:
![](./img/2PLVao1.png)  |  ![](./img/2PLVao2.png)
![](./img/mgao1.png)  |  ![](./img/mgao2.png)
![](./img/aosimple.png)  |  ![](./img/aomulti.png)

##### Shadow
The shadow in Mol\* is a screen space effect like the SSAO. Our implementation is greatly inspired by [Panos Karabelas](https://panoskarabelas.com/posts/screen_space_shadows/), who detailed the basic idea as follows: We start by moving from the pixel to the light. We move in steps; in each step, we compare the depth of our ray against the depth that the camera perceives. If our ray depth is larger (further away) from the camera’s, then we assume that the pixel is in shadow.

![](https://panoskarabelas.com/media/post_sss_idea.png) 
<img src="../img/shadow.png" align="left" width="300px"/>
<br>
The following options are exposed:<br>
- **Steps**: How many pixels are sampled along the path between the pixel and the light distance<br>
- **Bias**: Strength of the shadow<br>
- **Max distance**: The maximum distance to cover in the direction of light<br>
- **Tolerance**: Depth difference threshold<br>

*Note that the light settings are accessible in the advanced viewport settings->Renderer->Light->Inclination|Azimuth|Color|Intensity.*

<br clear="left"/>
Here is an example showing a rendering with shadow only, 64 steps, 0.81 bias, and a distance of 256.

![](./img/onlyshadow.png)

##### Outline
<img src="../img/shadow.png" align="left" width="300px"/>
The outline effect draws a colored line at abrupt changes of normal and depth. This gives a contouring effect for which we can adjust its Scale (thickness), Threshold (sensitivity), and Color.

<br clear="left"/>

Threshold 0.1 Black contour |  Threshold 0.6 Yellow contour
:-------------------------:|:-------------------------:
![](./img/outline1.png)  |  ![](./img/outline2.png)

##### Depth Of Field
The depth of field is the distance between the nearest and the furthest objects that are in acceptably sharp focus in an image captured with a camera. To fake this visual effect, we implemented a simplified [screen space algorithm](https://catlikecoding.com/unity/tutorials/advanced-rendering/depth-of-field/) that evaluates the distance of the pixel from the sharp point of focus, which is either the scene bounding box center or the camera pivot point. The distance test can be done in a sphere or against a plane.

<img src="../img/dof.png" align="left" width="300px"/>
- **Blur size**: Controls the number of pixels of the blurring box<br>
- **Blur spread**: Controls the scale of the blurring box<br>
- **In Focus**: Used in planar mode to define the distance from the plane passing through the Center<br>
- **Ppm**: The size of the area in focus (plane thickness or sphere radius)<br>
- **Center**: The center of the focused area, either the scene center or the current camera target (default)<br>
- **Mode**: How the focus distance is computed. In planar mode: <br>`focus = (abs(distance_to_center_Z) - InFocus) / PPM;`<br> and in spherical mode: <br>`focus = distance_to_center / PPM;`<br>

<br clear="left"/>

Planar DOF |  Spherical DOF
:-------------------------:|:-------------------------:
![](./img/dof1.png)  |  ![](./img/dof2.png)

##### Fog
<img src="../img/fog.png" align="left" width="300px"/>
Also called depth cue, it helps to emphasize what is in the foreground and background of the image with respect to the camera by adding a progressive fog of a given intensity based on the depth value.  
<br clear="left"/>

#### Advanced Settings
<img src="../img/advancedcontrol.png" align="left" width="300px"/>
<br>
This panel provides advanced settings for fine-tuning the rendering and performance of the viewer:<br>
- **Multi Sample**<br>
&nbsp;&nbsp;&nbsp;&nbsp;- **Mode**: Toggle between different multi-sampling modes. On, Off, Temporal.<br>
&nbsp;&nbsp;&nbsp;&nbsp;- **Sample Level**: Adjust the level of multi-sampling. Higher levels provide better quality at the cost of performance. Take level^2 samples.<br>
&nbsp;&nbsp;&nbsp;&nbsp;- **Reduce Flicker**: Enable or disable flicker reduction in "temporal" mode.<br>
- **Hi Z** Hierarchical Z-buffer occlusion culling. Only available for WebGL2.<br>
&nbsp;&nbsp;&nbsp;&nbsp;- **Enabled**: Toggle Hi Z on or off. This improves rendering performance by using a hierarchical Z-buffer.<br>
&nbsp;&nbsp;&nbsp;&nbsp;- **Max Frame Lag**: Adjust the maximum frame lag. This sets the upper limit on how many frames the Hi Z buffer can lag behind the current frame.<br>
&nbsp;&nbsp;&nbsp;&nbsp;- **Min Level**: Adjust the minimum level for Hi Z. This sets the lower bound for the depth levels considered by Hi Z.<br>
- **Sharpening** Contrast Adaptive Sharpening<br>
&nbsp;&nbsp;&nbsp;&nbsp;- **Enabled**: Toggle sharpening on or off. This improves the visual clarity by enhancing edges.<br>
&nbsp;&nbsp;&nbsp;&nbsp;- **Pixel Scale**: Adjust the pixel scaling factor. This controls the intensity of the sharpening effect.<br>
- **Transparency**<br>
&nbsp;&nbsp;&nbsp;&nbsp;- **Mode**: Choose the transparency mode. Options include Blended, Weighted and Depth Peeling.<br>

<br clear="left"/>

#### Moving in 3D
References to the mouse and key behaviors in the viewer:

- **Rotate**: Drag using the left mouse button
- **Rotate around z-axis (roll)**: Drag using the left mouse button + control key + shift key
- **Pan**: Drag using the right mouse button or left mouse button + control key
- **Focus**: Drag using three fingers
- **Focus and zoom**: Drag using the wheel/middle mouse button
- **Zoom**: Scroll using the wheel/middle mouse button
- **Clip**: Scroll using the wheel/middle mouse button + shift key
- **Move forward, back, left, right, up, down**: Press w, s, a, d, r, f
- **Roll left, right**: Press q, e
- **Pitch up, down**: Press arrow up + shift key, arrow down + shift key
- **Yaw left, right**: Press arrow left + shift key, arrow right + shift key
- **Boost move**: Press left shift key
- **Enable pointer lock**: Press space + control key

#### Mouse and Key Controls
References to the mouse and key controls in the viewer:

- **Spin Animation**: Press i
- **Rock Animation**: Press o
- **Toggle Fly Mode**: Press space + shift key
- **Reset View**: Press t
- **Camera center**: Click element using left mouse button
- **Camera center and focus**: Click element using right mouse button
- **Click**: Click element using left mouse button
- **Toggle select**: Click element using left mouse button + shift key or left mouse button + control key
- **Highlight**: Hover over element using mouse hover + shift key or mouse hover + control key
