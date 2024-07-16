#### Measurements Overview

Some tips & examples for doing measurements in #molstar at [Mol* Mesoscale Explorer](https://molstar.org/me/):

- Label, distance, angle, dihedral
- Orientation (box/axes from principal components)
- Plane (best fit)

![](./img/labelui.png)
![](./img/distance.png)
![](./img/labels.png)
![](./img/orientation.png)
![](./img/angle_plane.png)

#### Basic Measurements

![type:video](./videos/measure_ex.mp4)

View: [https://molstar.org/me/viewer/?url=mesoscope.scripps.edu/explorer/tours/measurements.molx&type=molx](https://molstar.org/me/viewer/?url=mesoscope.scripps.edu/explorer/tours/measurements.molx&type=molx)

#### Label Option
*Overview*

This panel allows users to configure text overlay settings for visual elements. It provides options for adjusting text properties, visibility, and styling.

<img src="./img/labeloptions.png" align="left" width="200px"/>
*Options* <br>
- **Select This**: Toggle to activate and configure the settings for the current selection.<br>
- **Opacity**: Adjust the opacity level of the text, with a range from fully transparent (0) to fully opaque (1).<br>
- **Quality**: Select the rendering quality of the text; options include 'Auto' for automatic adjustment based on display parameters.<br>
- **Text**: Field to enter the text content to be displayed. Note: if the label is a protein name, hovering over the label will highlight all instances of that protein in the viewport.<br>
- **Text Color**: Choose the color for the text.<br>
- **Text Size**: Slider to adjust the size of the text.<br>
- **Snapshot Key**: Assign a unique key for interactive behavior; clicking the label will load the snapshot with the corresponding key.<br>
- **Tooltip**: Enter a brief description or guidance that appears when users hover over the text element.<br>
*Advanced Options* <br>
- **Material Presets**: Apply predefined material properties to the text for consistent styling.<br>
- **Clip**: Enable or disable clipping of the text to its bounding box.<br>
- **Instance Granularity**: Control whether text properties are applied on a per-instance basis.<br>
- **Font Family**: Choose from various font families such as Sans Serif for text rendering.<br>
- **Font Quality**: Select the quality of the font rendering, such as 'high' for better clarity.<br>
- **Font Style and Variant**: Adjust the style and variant of the font, including options like Normal or Italic.<br>
- **Font Weight**: Set the weight of the font from light to bold.<br>
- **Size Factor**: Scale the text size relative to its original dimensions.<br>
- **Border Width and Color**: Customize the border around the text for visibility and aesthetics.<br>
- **Offset X, Y, Z**: Fine-tune the position of the text overlay in three-dimensional space.<br>
- **Background**: Enable a background layer for the text for enhanced readability.<br>
- **Background Opacity**: Adjust the opacity of the background.<br>
- **Tether**: Enable a line tethering the text to a specific point in the UI.<br>
- **Tether Length and Base Width**: Configure the appearance and dimensions of the tether.<br>
- **Attachment Point**: Set the attachment point for the text within its container, such as 'middle-center'.<br>
- **Scale By Radius**: Option to scale the text size dynamically based on the radius of the bounding sphere.<br>
*Visualization*<br>
- **Visuals**: Manage related visual elements.<br>
- **Culling & LOD**: Configure the level of detail and culling options to optimize performance.<br>
*Usage*<br>
This panel is crucial for users needing precise control over text displays in their projects, allowing for detailed customization and styling to suit various use cases. The intuitive layout ensures that both novice and advanced users can efficiently apply and modify text settings.

<br clear="left"/>
