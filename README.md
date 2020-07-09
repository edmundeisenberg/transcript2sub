Documentation for Robot History VTT tracker

FORMAT THIS LATER

(in email mention that click-scrolling elements aren't that hard)

## Premise

A JS-based applet that breaks a long-form transcript into word-groups and facilitates manual, speed-controlled time-stamping of subtitle tracks.  Resulting subtitle tracks may be saved as VTT (virtual text track) and used in HTML5 video elements. 

## Intended Use

This app was designed to provide shortcut-assisted manual time-stamping of subtitle tracks based on human-transcribed text.

## Page Layout

The page layout of transcript2sub is divided into three modules.  These are: video, transcript, and tracks.  Accordingly, the browser window is divided up into respective thirds containing said modules, as pictured here:

![Screen-shot of the applet](assets/applet_screen.png)



there is currently no mobile version of the applet.

## Content Registration

Before the UIUX becomes operable, the user must submit both a URL where the video is located and the full transcript body.  After this happens, 

<code>

$("#submit_mp4").click(function () {

	// load the video from link supplied	

	var video_url = document.getElementById("mp4_url").value;
	var video_html='<source src="' + video_url + '"/>';
	$("#active_video").html(video_html);

	// resize the player

	var video_width = $("#video_column").width();
	document.getElementById("active_video").style.width = ''+video_width-12;

	// hide the form and flag 

	document.getElementById("mp4_submission").style.display = "none";
	document.getElementById("url_flag").style.display = "none";
	video = $("#active_video")[0];
	video.playbackRate= .75;

	// check if both sources are supplied

	video_loaded = true;
	if(transcript_loaded){
	   runTracker();
	}
});

</code>

## UIUX



### Video

There are two functions of the video module. The first function is dedicated to 

### Transcript

### Tracks
There are three modules in the application corresponding to the video, the 

## Code
TRANSFER ANON FUNCTIONS INTO DEFINED FUNCTION 

AND: VTT MODULE SHOULD SCROLL AS IT ACCUMULATES
This is %

[all the code may be viewed by right clicking on the page and selecting (view source)]

Further Develoment