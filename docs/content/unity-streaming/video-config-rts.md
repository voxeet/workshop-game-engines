# Publisher Video Configuration

### Overview
This article aims to explain the various video configuration APIs available to the Unity SDK publisher. The article will be split into the following topics
* Creating video streams with a given resolution.
* Selecting the video codec.
* Adjusting video stream parameters.
* Creating video streams with a given resolution

The publisher API allows us to capture a video camera feed with a chosen resolution via the SetVideoSource API's second parameter as follows: 
### Custom resolution
```
McPublisher publisher = ...;
Camera cam = ...;
 
publisher.SetVideoSource(cam, new StreamSize { height = 1920, width = 1080 });
```

By default, the stream size is set to 1280 x 720  i.e. 720p. 

?> Note: In certain cases, for example with H264 codecs, not all stream resolutions are supported, however, there is an API to query that, which we will discuss in the following section. 

### Selecting video codec
The publisher also allows us to choose the video codec we want to encode with. There are four codecs we can choose from: 
* VP8
* VP9
* H264
* AV1
* 
?> In case of VP8, VP9 and AV1 codecs, their implementation is software based in contrast to H264 which is hardware based on all platforms. Therefore, it is preferable to use H264 whenever you can, however that comes with some limitations with regards to resolutions supported which will be discussed later. 

The default codec used is VP8, however, to change the selected codec, we should first query the supported codecs on the platform we are on: 
### Querying the supported codecs
```
// First query the available codecs
var codecs = Capabilities.GetAvailableVideoCodecs();
```

After that, we search for the codec we want to select, in this case H264: 

### Searching the list of supported codecs
```
if (Array.BinarySearch(codecs, 0, codecs.Length, VideoCodec.H264) >= 0) {
    publisher.options.videoCodec = VideoCodec.H264;
}
```

As we can see, we can use the options field within the publisher to select the codec.

?> You can find more information about the **VideoCodec** enum in the documentation. 

As stated earlier there is an API that we can use to query the maximum allowed resolution for a specific codec. Software codecs generally do not have any maximum resolution constraints theoretically, however for H264, there are due to the underlying hardware implementation. 

The following API Capabilities.GetMaximumSupportedResolution allows to query that information: 
### Query the maximum supported resolution for a codec
`Capabilities.SupportedResolutions maxResolution = Capabilities.GetMaximumSupportedResolution(VideoCodec.H264);`

** Capabilities.SupportedResolutions** is an enum that contains the common resolutions, some of those values are:
* SupportedResolutions.ANY 
* SupportedResolutions.RES_720p

We can use that value to tell us what the maximum resolution we can use in setting the video source via **SetVideoSource** when that codec is used. For example, if the maximum supported resolution was 1080p then we can do the following:

### Setting the video source with resolution after querying
`publisher.SetVideoSource(camera, new StreamSize { width = 1920, height = 1080 });`

?> Note: You can change the video codec only when unpublished. If you are publishing, changing the video codec will have no effect, and you will have to un-publish first before changing it. However, changing the video source can be done while publishing (for example, in order to change the capture resolution.)

### Adjusting the video stream parameters 
This is an advanced configuration that allows us to fine tune our video stream more. There are 4 video parameters we can adjust with the publisher API: 
* The maximum encoding bitrate.
* The minimum encoding bitrate.
* The maximum FPS.
* The resolution scale-down factor.

All of these configurations can be adjusted even while publishing via the publisher's SetVideoConfig API: 

### Custom video configuration

```
VideoConfig config = new VideoConfig {
    minBitrate = 1000, // in kbps
    maxBitrate = 6000,
    maxFramerate = 60,
    resolutionDownScaling = 2.0
};
 
publisher.SetVideoConfig(config);
```


Not all values have to be set at once. Here is a quick explanation for each of those fields: 

* **minBitrate:**  The minimum bitrate of encoding. This will depend on the network bandwidth available. If set too high, it might result in choppy streams. 
* **maxBitrate:** The maximum bitrate of encoding. This is set to 2.5 mbps by default. This has to be higher than minBitrate.
* **maxFramerate:** The maximum video frame-rate. Can be used to cap the frame-rate to reduce bandwidth used. 
* **resolutionDownScaling:** a factor greater than 1.0 to reduce the resolution by. This can be used to reduce the resolution to save bandwidth while publishing. For example, for an original resolution of 1280 x 720, setting the factor to 2.0 will halve the resolution to 640 x 360. 
