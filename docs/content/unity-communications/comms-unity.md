# Real-time Spatial Audio and Communications with Unity

Enhance your games with realtime Spatial Audio and Communications. This Unity package acts as a client to the Dolby.io Real-time Spatial Audio and Communications Service. 

## Dolby.io Virtual World plugin for Unity

With the Dolby.io Virtual World plugin for Unity, you can easily integrate Dolby.io Spatial Audio, powered by Dolby Atmos technology into your virtual world applications.

### Prerequisites
- Apple MacOS x64 or Microsoft Windows 10+ x64.
- A Dolby.io account. If you do not have an account, you can [sign up](https://dolby.io/signup) for a free account.
- The [client access token](https://docs.dolby.io/communications-apis/docs/overview-developer-tools#client-access-token) copied from the Dolby.io dashboard. To create the token, log into the [Dolby.io dashboard](https://dashboard.dolby.io/), create an application, and navigate to the API keys section.
- Install [git-lfs](https://git-lfs.com/) command line tool on your computer.

### How to install
You can install the plugin from the Unity Package Manager.

- Open the Package Manager from the Unity Editor and click the ➕ icon in the upper left corner.
- Select **Add package from git URL..**, enter the URL below
    ```
    https://github.com/DolbyIO/comms-sdk-unity.git
    ```

> ⓘ On MacOS, it is necessary to unquarantine SDK libraries. Otherwise, quarantine attributes prevent their usage. The simplest way to unquarantine the SDK library is to strip the quarantine attributes recursively for all the files in the package. Follow these steps:
>1. Open **Terminal**.
>2. Navigate to your project root folder, run this command: `xattr -d -r com.apple.quarantine Library/PackageCache/dolbyio.comms.unity*`.

### Apple Silicon
If you are using Unity from an Apple Silicon Mac (e.g., M1), please be aware that currently the SDK is only distributed as x64 binary for Mac. You need to configure the Unity project under `File` > `Build Settings` and select `Intel 64bits` to make it work. 




#### Next Steps:

* [Getting Started](https://api-references.dolby.io/comms-sdk-dotnet/documentation/unity/getting-started/installation.html)

* [Initalization](https://api-references.dolby.io/comms-sdk-dotnet/documentation/unity/getting-started/initialization.html)
  
* [Remote participants](https://api-references.dolby.io/comms-sdk-dotnet/documentation/unity/getting-started/remote-participants.html)
* [Shared Scenes](https://api-references.dolby.io/comms-sdk-dotnet/documentation/unity/getting-started/shared-scene.html)
* [Individual Scene](https://api-references.dolby.io/comms-sdk-dotnet/documentation/unity/getting-started/individual-scene.html)

  
* [Dolby.io .net SDK](https://github.com/DolbyIO/comms-sdk-dotnet)
