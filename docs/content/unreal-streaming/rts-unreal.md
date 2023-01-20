# Real-time Streaming with Unreal Engine

### Requirements 
* Windows or Linux
* UE4.27 UE5.0.3 UE5.1.0

### Publisher Plugin
This plugin enable to **publish game audio and video content to Millicast**. You can configure your credentials and configure your game logic using unreal object, capture and publish from virtual camera.
[Installing the Millicast Publisher plugin for Unreal engine](https://docs.dolby.io/streaming-apis/docs/publisher-plugin)
* Audio: Opus (Software Encoding).
* Video: VP8  (simulcast available, software encoding), VP9 (software encoding), H264 (simulcast not available, hardware encoding).

### Player Plugin
This plugin enable to **play real time stream from Millicast in your Unreal Engine game**. You can configure your credentials and configure your game logic using unreal object and then render the video in a texture2D.
[Installing the Millicast Player plugin for Unreal Engine](https://docs.dolby.io/streaming-apis/docs/player-plugin)
* Audio: Opus (Software Encoding).
* Video: VP8  (software decoding), VP9 (software decoding).

--- 
## Installing the Plugins
1. Create a template project in UE, then exit the editor. Make sure to use the **C++ Class**, not the Blueprint Class when creating the game template.
2. Exit out of the game and navigate to root of the project folder ```C:\Users\User\Unreal Engine\My_streaming_Project```. From the root of the project create a folder ```Plugins```.
3. Clone the ```MillicastPublisher``` plugin from the GitHub repo : ```git clone https://github.com/millicast/millicast-publisher-unreal-engine-plugin.git MillicastPublisher``` or clone the ```MillicastPlayer``` plugin from the GitHub repo : ```git clone https://github.com/millicast/millicast-player-unreal-engine-plugin.git MillicastPlayer```
4. Open the game again and confirm that the plugin correctly installed by navigating to ```Edit```>```Plugins```> Search for Millicast and you should see ```MillicastPublisher``` or ```MillicastPlayer```

####Troubleshooting Installation  
- The game must be created with a C++ template.
- You must have the correct version of Visual Studio installed to match your Unreal Engine version.
- You must have the correct version of the plugin installed, plugins are not backwards compatible.
- If prompted to rebuild MillicastPublisher, say yes.
- Some users may encounter an error asking them to build from source. To do this go to the directory of your game, right-click on the ```.uproject``` file and select ```Generate Visual Studio project files```. 
- If the issues with installation persist open an issue [here](https://github.com/millicast/millicast-publisher-unreal-engine-plugin/issues) for Publisher or [here](https://github.com/millicast/millicast-player-unreal-engine-plugin/issues) for Player.
---
## Building with the Publisher Plugin
[Documentation here](https://docs.dolby.io/streaming-apis/docs/publisher-plugin)
1. Enable the plugin by navigating to ```Edit```>```Plugins```> Search for Millicast and you should see ```MillicastPublisher```.
2. The MillicastPublisherSource object allow you to configure your Dolby.io Real-time Streaming credentials and manage the video and audio sources you want to publish to Millicast. To add a ```MillicastPublisherSource```, add a new asset by clicking ```"Add/Import"```, and you will see the object in the ```"Media"``` category.
3. Inside the ```MillicastPublisherSource``` object add your Dolby.io streaming token ```Stream name``` and ```Publishing token```. For a guide on creating tokens click [here](https://docs.dolby.io/streaming-apis/docs/managing-your-tokens).
4. For slate window capture (whole game view) and audio capture from submix (in-game audio) leave audio and video to none.
5. Next we will configure the blueprint for the publish logic. Click ```+Add``` then ```Blueprint class``` and then select  ```Actor``` and drag and drop the blue print onto your level.
6. Open the blueprint and switch from ```viewport``` to ```event graph```. On the components panel click ```+ Add``` and add the ```MillicastPublisherComponent```.
7. In the properties of your newly added component set ```Millicast Publisher Source``` to the ```MillicastPublisherSource``` we created and added credentials to earlier. Set the codec to a valid codec such as VP8.
8. Drag the component onto the event graph. We need to cconfigure the event graph as per this design [here](https://files.readme.io/003320e-blueprint.png). For an in-depth explanation of the event graph read [here](https://docs.dolby.io/streaming-apis/docs/publisher-plugin#blueprint).
9. Once configured the game is ready to play. Test it out. To find the stream of your game navigate to ```https://viewer.millicast.com?streamId=<YOUR_ACCOUNT_ID>/<YOUR_STREAM_NAME>```

####Troubleshooting
- Codec choice is very important, currently we only support: Audio: Opus (Software Encoding).
Video: VP8 (simulcast available, software encoding), VP9 (software encoding), H264 (simulcast not available, hardware encoding).
- Make sure your credentials are valid, you can test this from the Dolby.io dashboard by broadcasting a stream and testing it out.
- If the issues with installation persist open an issue [here](https://github.com/millicast/millicast-publisher-unreal-engine-plugin/issues).

---

## Building with the Player Plugin
