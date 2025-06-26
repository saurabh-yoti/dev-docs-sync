---
type: page
title: Face capture
listed: true
slug: face-capture-module
description: 
index_title: Face capture
hidden: 
keywords: 
tags: 
---

If you have integrated Age estimation and anti-spoofing API, you can add our face capture module to enhance your results. When deployed in a web application, Yoti optionally provides a JavaScript face capture module that uses the webcam to capture an image of the user which can be sent to the Yoti services backend for processing.

{% badge type="warning" text="Help" /%} If you need assistance please email: [clientsupport@yoti.com](mailto:clientsupport@yoti.com).

There is one step to follow to integrate the face capture module:

1. Install the package
2. Integrate the package.

This service has **high** image quality requirements. 

{% badge type="info" text="Hint" /%} Yoti face capture supports native and web integrations.

---

## Requirements

The image requirements to use our services are:

{% table widths="179" %}
| Condition | Requirement | 
| ---- | ---- | 
| Image resolution | The image must be 720pp(1280x720 pixels) or 1080pp (1920x1080 pixels) | 
| Image format | PNG or JPEG(95 to 100 quality).\n\n\n\nPlease avoid image format conversion to avoid degrade image quality | 
| Single face image | We don't support multiple faces images. | 
| Ratio Face to Image | 35% to 80% of Face Box over the image size\n\nNote: A centred overlay will help you to send better images. It will avoid the users stay to close to the camera avoiding face distortions or too far from the camera where the face will be too small for the model analysis. | 
| Face cropping | Based on Client Face detector adding padding | 
| Face position | Face should be centred in the image | 
| Image size | Min height/width 300 pixels\n\n\n\nMax height/width 2000 pixels | 
{% /table %}

The best trade-off between users' experience and model performance is applying a ratio between the size of the Bounding Box Face and the image size.

---

## Integration guide

Install the package and dependencies.

{% code %}
{% tab language="javascript" %}
npm i @getyoti/react-face-capture

import FaceCapture from "@getyoti/react-face-capture"
import "@getyoti/react-face-capture/index.css"
{% /tab %}
{% /code %}

The package depends on the following peer dependencies:

{% code %}
{% tab language="javascript" %}
"react": "16.12.0",
"react-dom": "16.12.0"
{% /tab %}
{% /code %}

Assets are not included in the javascript bundle. To have the components to work correctly, you will need to copy library assets from `@getyoti/react-face-capture/assets` folder into your assets folder.

For instance, in webpack you can use the plugin `copy-webpack-plugin` in the following way:

{% code %}
{% tab language="javascript" %}
new CopyPlugin([
  {
    from: path.resolve(__dirname, './node_modules/@getyoti/react-face-capture/assets'),
    to: path.resolve(__dirname, './assets')
  }
]),
{% /tab %}
{% /code %}

{% table %}
| Property | Type | Default | Description | Mandatory | 
| ---- | ---- | ---- | ---- | ---- | 
| captureMethod | String `manual/auto` | manual | The way you capture the photo, either with the button of auto-capture. | ❌ | 
| onSuccess | Function({ image }) |  | Callback which will be called once the result (capture) is complete. | ✅ | 
| onError | Function |  | Callback which will be called when there is an error. See Appendix for the list of error codes we currently support. | ❌ | 
| showOverlay | Boolean | true | Use a face overlay | ❌ | 
| widthMinConstraint | Number | 1024 | Video min width constraint passed to `getUserMedia` |  | 
| widthIdealConstraint | Number | 1280 | Video ideal width constraint passed to `getUserMedia` | ❌ | 
| format | String | jpeg | Image format | ❌ | 
| CustomButton | Function | simplebutton | Custom UI of the button. It uses `onClick` and `disabled` as props | ❌ | 
| countdownMode | String `auto/never/always` | never | Note: `auto` means it will be hidden on mobile and shown on desktop | ❌ | 
| imageType | String `original/cropped` | orginal | Cropped image to improve performance on processing from the API | ❌ | 
| isDebug | Boolean | false | If `true`, display useful information | ❌ | 
| qualityType | String `high/medium/low` | high | The quality of the image taken for jpeg format only. High (1) - Medium (0.96) - Low (0.90) | ❌ | 
| language | - `en`: English\n- `es`: Spanish (Spain)\n- `es-419`: Spanish (Latin America)\n- `it`: Italian\n- `de`: German\n- `fr`: French | en | The language code to set the language of the feedback messages | ❌ | 
{% /table %}

---

## Example code

{% code %}
{% tab language="javascript" %}
import FaceCapture from '@getyoti/react-face-capture';
import '@getyoti/react-face-capture/index.css';

export function App() {
  const onSuccess = ({ image }) => console.log('Length = ', image.length);
  const onError = (error) => console.log('Error =', error);

  return <FaceCapture onSuccess={onSuccess} onError={onError} />;
}
{% /tab %}
{% /code %}

Full web example:

- [Web example.](https://github.com/getyoti/web-fcm-demo/)

Yoti also has native integration examples:

- [Android example](https://github.com/getyoti/yoti-face-capture-android)
- [iOS example](https://github.com/getyoti/yoti-face-capture-ios)

---

## Error codes

{% table %}
| Error Code | Description | 
| ---- | ---- | 
| NO_CAMERA | No camera detected on the user’s device | 
| GENERIC_CAMERA_ERROR | Other camera error. The reasons can be [various](https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/getUserMedia), and inconsistent across browsers. The complete error is logged in the user’s browser console. | 
| UNSUPPORTED_BROWSER | The user’s browser is not supported, because the API needed for camera interaction is missing. `Note: Older Non-Safari browsers on iOS also fall into this category.` | 
| NO_CAMERA_PERMISSION | The user rejected the camera permission | 
| OVERCONSTRAINED | The camera constraints are not compatible with any camera device. `Note: One recovery option is to lower the widthMinConstraint value.` | 
| FACE_DETECTION_INIT_ERROR | The face detection has failed to initialise. This usually means that the required model assets are missing from the host application. | 
| INTERNAL_ERROR | Internal error. This can be due to a programming error, or the user using an old unsupported browser. | 
{% /table %}