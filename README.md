# Svelte Image Zoom Plugin

The Svelte Image Zoom Plugin is a lightweight and customizable plugin that provides zoom functionality for images in Svelte applications. It allows users to hover over an image and view a zoomed-in version in a separate box, enhancing the user experience and providing a closer look at image details.

## Features

- Smooth zoom functionality on mouse hover
- Customizable zoom box size and selector dimensions
- Support for both local and remote images
- Easy integration with Svelte applications

## Props

The `ImageZoom` component accepts the following props:

| **Prop**           | **Type**   | **Default Value** | **Description**                                                                                        |
|----------------|--------|---------------|----------------------------------------------------------------------------------------------------|
| imageStyle     | Object | {}            | Custom CSS styles for the image element.                                                           |
| containerStyle | Object | {}            | Custom CSS styles for the container element.                                                       |
| url            | String | null          | The path or URL of the image to be displayed.                                                      |
| zoomImgUrl     | String | null          | An alternative image URL to use for zoomed view (optional, if not provided, the url prop is used). |
| viewerWidth    | Number | 200           | The width of the zoom viewer in pixels.                                                            |
| viewerHeight   | Number | 400           | The height of the zoom viewer in pixels.                                                           |
| selectorWidth  | Number | 30            | The width of the zoom selector box in pixels.                                                      |
| selectorHeight | Number | 30            | The height of the zoom selector box in pixels.                                                     |

## Styling
The `ImageZoom` component can be customized using CSS styles. Here are the CSS classes and their default styles:

- `.zoom-box`: The container element that wraps the image and the zoom components.
- `.zoom-box > img`: The image element.
- `.viewer-box`: The zoom viewer box element.
- `.viewer-box img`: The zoomed-in image element inside the viewer box.
- `.zoom-selector`: The zoom selector box element.

## Example

```svelte
<script>
  import ImageZoom from "image-zoom-simple";
</script>

<main>
  <ImageZoom
    imageStyle={{ width: '200px' }}
    viewerHeight={250}
    url="https://images.unsplash.com/photo-1686077304557-d13e1b91ac06?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=2864&q=80"
  />
  <ImageZoom
    imageStyle={{ width: '200px' }}
    viewerHeight={200}
    url="https://images.unsplash.com/photo-1674574124349-0928f4b2bce3?ixlib=rb-4.0.3&ixid=M3wxMjA3fDF8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1471&q=80"
  />
</main>
```

You can override these styles in your application's CSS to achieve the desired visual appearance.