# Getting NICE DCV Session Screenshots<a name="managing-sessions-lifecycle-screenshot"></a>

You can use the `dcv get-screenshot` command to get a screenshot of a running session's desktop\. 

## Syntax<a name="syntax"></a>

```
dcv get-screenshot --max-width pixels --max-height pixels --format JPEG|PNG --primary --json --output /path_to/destination session_name
```

## Options<a name="syntax"></a>

**`--max-width`**  
Specifies the maximum width, in pixels, of the screenshot\. If you don't specify a width or a height, the screenshot uses the session's display resolution\. If you specify a height only, the width is automatically scaled to maintain the aspect ratio\.  
Type: Integer  
Required: No

**`--max-height`**  
Specifies the maximum height, in pixels, of the screenshot\. If you don't specify a width or height, the screenshot uses the session's display resolution\. If you specify a width only, the height is automatically scaled to maintain the aspect ratio\.  
Type: Integer  
Required: No

**`--format`**  
The file format of the screenshot\. Currently, only the `JPEG` and `PNG` formats are supported\. If you specify conflicting file types for the `--format` and `--output` options, the value specified for `--format` takes priority\. For example, if you specify `--format JPEG` and `--output myfile.png`, NICE DCV creates a JPEG image file\.  
Type: String  
Allowed values: `JPEG` \| `PNG`  
Required: No

**`--primary`**  
Indicates whether to get a screenshot of the primary display only\. To get a screenshot of the primary display only, specify `--primary`\. To get a screenshot of all displays, omit this option\. If you choose to get a screenshot of all of the displays, all of the displays are combined into a single screenshot\.  
Required: No

**`--json`, `-j`**  
Indicates whether to deliver the output in JSON format encoded in base64\. To get JSON output, specify `--json`\. Otherwise, omit it\.  
Required: No

**`--output`, `-o`**  
Specifies the destination path, file name, and file type for the screenshot\. For example, for Windows, specify `c:\directory\filename.format`, and for Linux, specify `/directory/filename.format`\. The format must be `.png` or `.jpeg`\. If you specify conflicting file types for the `--format` and `--output` options, the value specified for `--format` takes priority\. For example, if you specify `--format JPEG` and `--output myfile.png`, NICE DCV creates a JPEG image file\.  
Type: String  
Required: no

## Examples<a name="examples"></a>

**Example 1**  
The following example command gets a screenshot of a session named `my-session`\. The screenshot uses the resolution of the server\.

```
dcv get-screenshot --output myscreenshot.png my-session
```

**Example 2**  
The following example command gets a screenshot that is `200` pixels wide and `100` pixels high of a session named `my-session.` It saves the file in the current directory with the file name `myscreenshot.png`\.

```
dcv get-screenshot --max-width 200 --max-height 100 --output myscreenshot.png my-session
```

**Example 3**  
The following example command gets a screenshot of a session named `my-session`\. It gets a screenshot of the primary display only, saves the file in the current directory, and names it `myscreenshot.png`\.

```
dcv get-screenshot --primary --output myscreenshot.jpeg my-session
```

**Example 4**  
The following example command gets a screenshot of a session named `my-session`\. The command outputs the file encoded in base64 in JSON format\.

```
dcv get-screenshot --json --format png my-session
```