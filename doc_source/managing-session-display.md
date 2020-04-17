# Managing the NICE DCV Session Display Layout<a name="managing-session-display"></a>

You can set the display layout for a running NICE DCV session\. The display layout specifies the default configuration that is used when clients connect to the session\. However, clients can manually override the layout using the NICE DCV client settings or the native operating system display settings\. You can prevent clients from changing the display layout by setting the `enable-client-resize` configuration parameter to false\. For more information, see [`display` Parameters](config-param-ref.md#display)\.

If the host server's hardware and software configuration does not support the specified resolution or the number of screens, the NICE DCV server does not apply the specified display layout\.

**Topics**
+ [Specifying the Display Layout](#dislay-set)
+ [Viewing the Display Layout](#dislay-view)

## Specifying the Display Layout<a name="dislay-set"></a>

**To configure the display layout for a running NICE DCV session**  
Use the `dcv set-display-layout` command and specify the session for which to set the display layout and the display layout descriptor\.

```
dcv set-display-layout --session session-id display-layout-descriptor
```

The display layout descriptor specifies the number of displays and the resolution and position offset for each display\. The description must be specified in the following format:

```
widthxheight+|-x-position-offset+|-y-position-offset
```

If you specify more than one screen, separate the screen descriptors by a comma\. The screen position offsets specify the position of the top\-left corner of the screen relative to screen 1\. If you do not specify a position offset for a screen, it defaults to x=0 and y=0\.

**Important**  
If you're specifying more than one screen, ensure that you properly set the position offset for each screen to avoid screen overlaps\.

For example, the following display layout descriptor specifies two screens:
+ Screen 1: 1920x1080 resolution offset to x=0, y=0
+ Screen 2: 800x600 resolution offset to x=1920, y=0 so that it appears to the right of screen 1\.

![\[Screen layout with two screens.\]](http://docs.aws.amazon.com/dcv/latest/adminguide/images/eg2.png)

```
1920x1080+0+0,800x600+1920+0
```

The following display layout descriptor specifies three screens\. 
+ Screen 1: 1920x1080 resolution offset to x=0, y=0
+ Screen 2: 1920x1080 resolution offset to x=1920, y=0 so that it appears to the right of screen 1\.
+ Screen 3: 1024x768 resolution offset to x=\-1024, y=0 so that it appears to the left of screen 1\.

![\[Screen layout with three screens.\]](http://docs.aws.amazon.com/dcv/latest/adminguide/images/eg1.png)

```
1920x1080+0+0,1920x1080+1920+0,1024x768-1024+0
```

## Viewing the Display Layout<a name="dislay-view"></a>

**To view the display layout for a session**  
Use the `dcv describe-session` command and review the `display layout` element in the output\. For more information, see [Viewing NICE DCV Sessions](managing-sessions-lifecycle-view.md)\.