# jspsych-single-stim plugin

This plugin displays an image or HTML-formatted content and allows the subject to respond by pressing a button on the screen. The stimulus can be displayed until a response is given, or for a pre-determined amount of time. The trial can be ended automatically if the subject has failed to respond within a fixed length of time.

Because this plugin can display any HTML content, it is quite versatile. It can be used for any situation in which the response generated by the subject is a single button press.

## Parameters

This table lists the parameters associated with this plugin. Parameters with a default value of *undefined* must be specified. Other parameters can be left unspecified if the default value is acceptable.

Parameter | Type | Default Value | Description
----------|------|---------------|------------
stimuli | array | *undefined* | Each element of the array is a stimulus. A stimulus can be either a path to an image file or a string containing valid HTML markup. Each stimulus will be presented in its own trial, and thus the length of this array determines the total number of trials.
is_html | boolean | false | If the elements of the `stimuli` array are strings containing HTML content, then this parameter must be set to true.
choices | array | [ ] | This array contains the labels for the buttons.
button_html | string or array | `'<button class="jspsych-btn">%choice%</button>'` | A template of HTML for generating the button elements. You can override this to create customized buttons of various kinds. The string `%choice%` will be changed to the corresponding element of the `choices` array. You may also specify an array of strings, if you need different HTML to render for each button. If you do specify an array, the `choices` array and this array must have the same length. The HTML from position 0 in the `button_html` array will be used to create the button for element 0 in the `choices` array, and so on.
prompt | string | "" | This string can contain HTML markup. Any content here will be displayed below the stimulus. The intention is that it can be used to provide a reminder about the action the subject is supposed to take (e.g. which key to press).
timing_stim | numeric | -1 | How long to show the stimulus for in milliseconds. If the value is -1, then the stimulus will be shown until the subject makes a response.
timing_response | numeric | -1 | How long to wait for the subject to make a response before ending the trial in milliseconds. If the subject fails to make a response before this timer is reached, the the subject's response will be recorded as -1 for the trial and the trial will end. If the value of this parameter is -1, then the trial will wait for a response indefinitely.
response_ends_trial | boolean | true | If true, then the trial will end whenever the subject makes a response (assuming they make their response before the cutoff specified by the `timing_response` parameter). If false, then the trial will continue until the value for `timing_response` is reached. You can use this parameter to force the subject to view a stimulus for a fixed amount of time, even if they respond before the time is complete.

## Data Generated

In addition to the [default data collected by all plugins](overview#datacollectedbyplugins), this plugin collects the following data for each trial.

Name | Type | Value
-----|------|------
stimulus | string | Either the path to the image file or the string containing the HTML formatted content that the subject saw on this trial.
button_pressed | numeric | Indicates which button the subject pressed. The first button in the `choices` array is 0, the second is 1, and so on.
rt | numeric | The response time in milliseconds for the subject to make a response. The time is measured from when the stimulus first appears on the screen until the subject's response.

## Examples

#### Displaying image until subject gives a response

```javascript
var trial = {
	type: 'button-response',
	stimuli: ['img/happy_face_1.jpg'],
	choices: ['Happy', 'Sad'],
	prompt: "<p class='center-content'>What emotion is this person showing?</p>"
};
```