# Managing the NICE DCV Session Display Layout<a name="managing-session-display"></a>

You can set the display layout for a running NICE DCV session\. The display layout specifies the default configuration that is used when clients connect to the session\. However, clients can manually override the layout using the NICE DCV client settings or the native operating system display settings\. 

If the host server's hardware and software configuration does not support the specified resolution or the number of screens, the NICE DCV server does not apply the specified display layout\.

**Topics**
+ [Restricting the Display Layout](#display-restrict)
+ [Specifying the Display Layout](#dislay-set)
+ [Viewing the Display Layout](#dislay-view)

## Restricting the Display Layout<a name="display-restrict"></a>

You can configure the NICE DCV server to prevent clients from requesting display layouts that are outside of a specified range\. To restrict display layout changes, configure the following NICE DCV server parameters\.
+ [`enable-client-resize`](config-param-ref.md#paramref.display.enable-client-resize)—To prevent clients from changing the display layout, set this parameter to `false`\.
+ [`min-head-resolution`](config-param-ref.md#paramref.display.min-head-resolution) and [`max-head-resolution`](config-param-ref.md#paramref.display.max-head-resolution)—Specifies the minimum and maximum allowed resolutions respectively\.
+ [`web-client-max-head-resolution`](config-param-ref.md#paramref.display.web-client-max-head-resolution)—Specifies the maximum allowed resolution for web browser clients\. The `max-head-resolution` limitation is applied on top of `web-client-max-head-resolution` limitation\.
+ [`max-num-heads`](config-param-ref.md#paramref.display.max-num-heads)—Specifies the maximum number of displays\.
+ `max-layout-area`— Specifies the maximum number of pixels allowed for the screen area\. Requests in which the total screen area expressed in pixels exceeds the specified value are ignored\.

For more information about these parameters, see [`display` Parameters](config-param-ref.md#display) in the Parameter Reference\.

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