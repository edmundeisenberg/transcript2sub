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

Video Registration:
<code>

	$("#submit_mp4").click(function () {
	
		// load the video from link supplied	
		var video_url = document.getElementById("mp4_url").value;
		var video_html='<source src="' + video_url + '"/>';
		$("#active_video").html(video_html);

		// resize the player
		var video_width = $("#video_column").width();
		document.getElementById("active_video").style.width = ''+video_width-12;

		// hide the submission form and request flag 
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

Transcript Registration:

This function specifically accounts for the HTML formatting of OHR interview transcripts as found here: *** FIND***  

The word-grouping algorithm is roughly the following:
*1.* The transcript is broken up into phrases, determined by various punctuation marks, using `<p>` tags as delimiting characters.
*2.* Each phrase is word-counted and, if fewer than 24 words, joined with the consecutive phrase.  This process continues until the 24 word threshold is exceeded, completing a word-group.
*3.* Each word group is embedded within a distinct `<p>` element.  This will allow for onclick events during the [titling process](#UIUX).

<code>

	$("#submit_transcript").click(function () {
		var transcript_text=document.getElementById("transcript_entry").value;
			// hide submission elements
		document.getElementById("transcript_submission").style.display = "none";
		document.getElementById("transcript_flag").style.display = "none";

			// create holder for parsed transcript
		var parsed_transcript=transcript_text;
		
			// break transcript into punctuated phrases, for more readable word groups later
		parsed_transcript = parsed_transcript.split('?').join('?</p><p>');
		parsed_transcript = parsed_transcript.split('!').join('!</p><p>');
		parsed_transcript = parsed_transcript.split(".").join(".</p><p>");
		parsed_transcript = parsed_transcript.split(",").join(",</p><p>");
		parsed_transcript = parsed_transcript.split("–").join("–</p><p>");

		var phrases = parsed_transcript.split("</p><p>");
		word_chunks=[];

		var id_count = 0;
		var id_tag="";

			// basically creates blocks of MINIMUM 24 words each
		for(i=0;i<phrases.length;i++){
				// make sure not to cut off any special characters
			if(phrases[i].length>2 && phrases[i].charAt(0) != "\""){
			  word_chunk = phrases[i];
				// check if meets minimum word count is met or adds more words to chunk
			  while (word_chunk.split(" ").length<=24){
				i++;
					// add the next phrase
				word_chunk+=" "+phrases[i]
				phrases.push("");
			  }
		  
			  tagged_chunk='</p><p>'+word_chunk;
			  word_chunks.push(tagged_chunk);
			  id_count++;
			}else{
			  last_index = word_chunks.length-1;
			  word_chunks[last_index]+=phrases[i];
			}
		}
	
			// join all work chunks
		render_transcript=word_chunks.join("");
	
			// and add them to DOM
		$("#transcript_renderer").html('<p>' + render_transcript+'</p>');
	
			// check if both sources are supplied
		transcript_loaded = true;
		if (video_loaded){
			runTracker();
		}
	})

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
