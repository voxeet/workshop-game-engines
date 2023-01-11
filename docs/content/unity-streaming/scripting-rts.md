# Instantiating RTS within a script

This is the preferred method, as it allows users to control when to publish, unpublish, control video parameters and dynamically switch video and audio sources, which leads to more freedom. Assuming you have a parent script,

let us first import the required namespace:

### Importing the namespace
`using Dolby.Millicast;`

# Millicast Publisher (or McPublisher)
Then, you can create a publisher like so: 
### Creating a publisher
`McPublisher publisher = gameObject.AddComponent<McPublisher>();`
which you can then set the Credentials and optionally PublisherOptions for:
Setting Credentials and Publisher Options

```
Credentials credentials = ...;
publisher.credentials = credentials;
 
PublisherOptions publisherOptions = ...;
publisher.options = publisherOptions;
```
After that, we will need to add the video sources to publish, assuming you have a camera and audio source created before hand:
### Setting the publisher video and audio sources
```
Camera camera = ...;
AudioSource audioSource = ...;
 
publisher.SetVideoSource(camera);
publisher.SetAudioSource(audioSource);
 
// You can optionally add a RawImage to render the camera feed locally, as well
// as AudioSource to render the local audio source. You can multiple of both.
RawImage renderTexture = ...;
AudioSource renderAudioSource ...;
publisher.AddRenderImage(renderTexture);
publisher.AddRenderAudioSource(renderAudioSource);
```
Finally, we can publish:
### Publishing
`publisher.Publish();`
And to unpublish: 
### Unpublishing
`publisher.Unpublish();`
The publisher also supports some useful callbacks that can be set to receive information of when we are actually publishing, when a connection error occurs, and when the viewer count changes as well as : 
### Useful callbacks
```
publisher.OnPublishing += (publisher) =>
{
  Debug.Log($"We are publishing!");
};
publisher.OnConnectionError += (publisher, errorMessage) =>
{
  Debug.Log($"Error publishing: {errorMessage}");
};
publisher.OnViewerCount += (publisher, count) =>
{
  Debug.Log($"Viewer count is currently: {count}");
};
```
For example, you can use the **OnPublishing**  callback to start subscribing via the Millicast Subscriber (or McSubscriber) which we will get to in the next section. 

# Millicast Subscriber (or McSubscriber)
The Millicast subscriber has a very similar API to the publisher, in terms of setting credentials and options, so we will skip those for the time being, and for more information, you can access the documentation. 

The only thing to note, is that the subscriber only requires the stream name and the account ID for credentials, and a subscribing token only when the stream you are viewing is a secure viewer stream. 

The subscriber requires **RawImage** objects to render the incoming video stream on, as well as **AudioSource** to render the incoming audio stream.


We can add those similar to how we added the local renderers in the publisher section, as follows:

### Adding video and audio renderers to the subscriber
```
McSubscriber subscriber = ...;
 
RawImage renderImage = ...;
AudioSource renderAudioSource;
 
subscriber.AddRenderImage(renderImage);
subscriber.AddRenderAudioSource(renderAudioSource);
```
We can add however many of those we want to the subscriber, and they will all receive the render the same stream. To subscribe: 

### Subscribe
`subscriber.Subscribe();`

And to unsubscribe: 
### Unsubscribe
`subscriber.UnSubscribe();`

Similarly, the subscriber contains a set of callbacks to set to know when you are subscribing, when a connection error occurs and when the viewer count changes:

### Useful subscriber callbacks
```
subscriber.OnSubscribing += (subscriber) =>
{
  Debug.Log($"We are subscribing!");
};
subscriber.OnConnectionError += (subscriber, errorMessage) =>
{
  // This could happen if no source is publishing for example.
  Debug.Log($"Error subscribing: {errorMessage}");
};
subscriber.OnViewerCount += (subscriber, count) =>
{
  Debug.Log($"Viewer count is currently: {count}");
};
```
Now that the basic features are done, Let us understand how to perform video configuration for publishing.

### Next Section:
[Publisher Video Configuration](content/unity-streaming/video-config-rts.md)

