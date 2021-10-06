# Configuring multi\-channel audio<a name="manage-audio"></a>

NICE DCV supports up to 7\.1 audio channels when using the NICE DCV native clients\. The web browser clients supports only stereo 2\.0 audio channels\.

NICE DCV supports the following multi\-channel audio configurations:
+ Stereo 2\.0 \(two channels\)
+ Quadriphonic 4\.0 \(four channels\)
+ Surround 5\.1 \(six channels\)
+ Surround 7\.1 \(eight channels\)—Windows NICE DCV servers only

![\[Supported audio configurations\]](http://docs.aws.amazon.com/dcv/latest/adminguide/images/audio.png)

If the client requests a lower number of audio channels than the number of channels provided by the server, the server downmixes the number of channels\. This is to match the number of channels requested by the client\. For example, assume that the client requests surround sound 5\.1 while the server supports up to surround sound 7\.1\. The server downmixes the audio to 5\.1\.

The server doesn't automatically downmix audio to match the audio output of the source application\. For example, assume that the source application provides surround sound 7\.1 whereas client supports only stereo 2\.0\. Only the front\-left and front\-right audio channels are streamed to the client\. The remaining channels are lost\. If this is true, to prevent the loss of audio channels configure the NICE DCV server to downmix the audio channels\.

**Topics**
+ [Configuring the audio channels on Windows NICE DCV servers](#win-audio)
+ [Configuring the audio channels on Linux NICE DCV servers](#linux-audio)

## Configuring the audio channels on Windows NICE DCV servers<a name="win-audio"></a>

Windows servers support surround sound 7\.1 \(eight audio channels\)\. The default configuration is stereo\. However, you can configure the server to use a different configuration\.

**Configuring the audio channels on Windows servers:**

1. Open the Sound Control Panel\. From the desktop’s taskbar, right\-click on the Speaker icon, and choose **Sounds**\.

1. Open the Playback tab and choose the NICE DCV speakers\.

1. Choose **Configure**\.

1. Choose your preferred channel configuration\.

1. Choose **OK**\.

## Configuring the audio channels on Linux NICE DCV servers<a name="linux-audio"></a>

Linux servers support stereo 2\.0 \(two audio channels\) by default and require some additional configuration to support multi\-channel audio\. 

You need to do the following:

1. Configure the PulseAudio sound server\.

1. Configure the NICE DCV server to use the PulseAudio device\.

1. Configure the number of channels to use\.

**To configure the PulseAudio sound server**

1. Open `/etc/pulse/default.pa` with your preferred text editor\. 

1. Add the following line to the end of the file\.

   ```
   load-module module-null-sink sink_name=dcv format=s16be channels=6 channel_map=front-left,front-right,rear-left,rear-right,front-center,lfe rate=48000 sink_properties="device.description='DCV Audio Speakers'"
   ```

1. Save and close the file\.

After you configured the PulseAudio sound server, you must configure the NICE DCV server to capture the audio from the PulseAudio sound server\.

**To configure the NICE DCV server to use the PulseAudio device**

1. Retrieve the name of the PulseAudio device using the following command\.

   ```
   $ C:\> pacmd list-sources
   ```

   The device name is listed in the `device.description` field\.

1. Open `/etc/dcv/dcv.conf` with your preferred text editor\.

1. Locate the `grab-device` parameter in the `[audio]` section\. Then, replace the existing value with the device name that you retrieved in the previous step\.

   If there's no `grab-device` parameter in the `[audio]` section, add it manually using the following format:

   ```
   [audio]
   grab-device="device_name"
   ```

1. Save and close the file\.

After you configured the NICE DCV server to capture the audio from the PulseAudio sound server, you can specify the number of channels to use\.

**To configure the number of channels to use**

1. Open `/etc/dcv/dcv.conf` with your preferred text editor\.

1. Locate the `source-channels` parameter in the `[audio]` section\. Then, replace the existing number of channels with one of the following: `2` for 2\.0, `4` for 4\.0, or `6` for 5\.1\.

   If there's no `source-channels` parameter in the `[audio]` section, add it manually using the following format:

   ```
   [audio]
   source-channels=channels
   ```

1. Save and close the file\.

1. [Stop](manage-stop.md) and [restart](manage-start.md) the NICE DCV server\.