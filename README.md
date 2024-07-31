# Logix Designer Feature Requests
### (all checked up to V34, some checked to v36)

I need to preface these comments with the acknowledgement that Logix designer is by far the easiest to use PLC programming software that I have used, both from a technical and interface point of view. I’ve spent most of my working life using it. Kudos to the hardware and software teams that have got us to this point. Below is a list of feature requests that range from simple interface issues to more radical features that would require PLC firmware changes. If you're a dev that works on this software, there's some pretty low hanging fruit.

colin.love@hmps.com.au

# Pure Interface
## Trending

- Allow zoom-selection of x axis in isolated graphing mode
- Allow order of tags/pens to be rearranged
- Retain settings from the last created trend
  - x scale. (I’ve never used a trend with only a 2 second window, and probably never will)
  - y scale and options
  - Display milliseconds
  - Colour palette
- Make default colours for first trend pen and background a combination you can see easily
  - White background might make more sense so trend pen and legend text can be both seen
- Allow toggling of auto scale in Y axis from the trend window
  - This way you can run a trend in auto-scale and once some meaningful signals have arrived, lock the scale so that the scale can remain consistent for a longer period even after those signals have gone.
- Allow specifying X min/max when using x/y plot
- Allow zooming in on data as its being captured. This may already be possible, but I’ve never got it to work properly.
- Allow the ability to return focus to another window during creation of a new trend. If you have added 7 tags to a trend and you can’t quite remember what the last tag is that you want, you are forces to create the trend with what you have before you can go back and look at your ladder or tag list.
- Allow tags to be dragged and dropped from the ladder window into the trend window or onto a trend item in the controller explorer
- Allow DINT’s to be viewed as 32 separate bits within the trend view. This would allow you to trend 256 states without changing the way the PLC deals with trending. This would be an absolute game changer for diagnosing complex state-based transient issues.
- Adding a tag to a trend that is already running, should restart the trend. Presumably it needs to stop at least momentarily for PLC comms reasons, but an automatic restart after this period would be ideal.
- Allow right-click context menu from trend legend (particularly cross-reference)
- Show samples as dots when zoomed in far enough on X axis
  - This could serve to highlight missed data as well as show when sampling has inadequate frequency
- Add trends to project documentation stored in the PLC
- Allow logs to be saved without stopping the trend

## Cross reference

-	Show indirect addressing reference used in the ‘reference’ column.
-	When a mixture of direct references and aliases are used, there is no way to sort the references in base order, because the BaseTag field is empty for non-aliased references.
-	Keyboard shortcut for cross-reference visible when right clicking from ladder (I assumed for years that there wasn’t one)
-	Give focus to the cross-reference list when cross-reference window is opened rather than wait for first arrow press.
-	Add a shortcut to move to the next destructive reference of current tag.
-	The “Name” dropdown box would be more useful if it had a history of previously cross-referenced tags rather than (or as well as) a tag explorer. When going down the rabbit-hole of someone else’s code, it can be difficult to find your way back if you do more than 1 cross-reference to follow a chain of logic.
-	Differentiate (and/or filter) based on edited (or to be removed) rungs and/or auto-refresh
    -	When you want to change every reference of a particular tag, I go to the cross reference, but as soon as you edit one instance, the cross reference can become misleading in 2 ways.
        -	If the list is refreshed, Edited rungs show up whether they are the to-be-inserted or to-be-removed rungs.
        -	If the window is not refreshed, some instances point to the incorrect location due to the insertion of rungs during the editing process
        -	My current workaround is to not refresh and work on the instances starting from the last when sorted in location order.
        -	My suggestion: Black for regular rung, green for to-be-inserted, red for to-be-removed

## Indirect Addressing

-	Indirect addressing of a parent datatype breaks auto-complete of child objects (It works for Structure Text but not Ladder)
-	Indirect addressing index autocomplete

## Ladder

-	Granular rung verification
    -	Highlight only the parts of a rung which do not verify
    -	Highlight invalid tags (within ladder params or within CPT/CMP equations)
-	Scroll bar should not snap to discrete rungs when dragged
-	When a branch from a pair of branches has been deleted, the most logical place for the selection to move to is the start of the remaining “branch” (although it is no longer a branch).
-	CMP/CPT
    -	CPT/CMP expression editor should expand to show the whole expression (or wrap the text)
    -	Auto-complete tags in CPT/CMP editor
    -	Better highlighting of tags on CPT/CMP editor. Currently a tag is only highlighted if it has a space before it, so “Tag1+Tag2*Tag3” doesn’t highlight all tags
    -	Respect all reserved words (currently “MOD” gets a red squiggly)
    -	Enter should close CPT/CMP expression editor (I know Ctrl+Enter does it already)
        -	OR allow newline characters to be retained to improve readability on large expressions
-	Rungs should be able to be dragged and dropped into a branch
-	Branches should be able to be dropped as new rungs
-	In some instances, the string editor window comes up on your left monitor even if Logix Designer is on your right monitor. It can also end up outside the bounds of your left monitor if you have different sized monitors
-	Duplicate label error prevents moving label during online edit
-	If too many tabs are open to see them all, make sure the one you’re on is one of the visible ones.
-	Allow 2 rows of tabs
-	Automatically adding an empty rung to an otherwise empty ladder when you open it is just annoying, especially when you’re online. It breaks the philosophy that you can explore a file without inadvertently modifying it.
-	Interrogate AOI InOut destructiveness so that cross-references aren’t automatically marked as descructive if the AOI the data is passed to doesn’t modify it.
-	Scale the blue arrows to match the zoom level
-	When editing a rung, don’t disable the insert rung button, just insert it at the next appropriate position
-	Allow pasting of code in text form that hasn’t come from Logix.
    -	Eg you can copy a rung from logix into notepad as: XIC(Tag1)OTE(Tag2);   
    -	By allowing the reverse process, standard code structures could be inserted without needing another instance of Logix running
-	Ladders don’t always render correctly when scrolling during dragging of an instruction or reference.
-	Allow dragging of output Booleans to bit instructions. (ie drag from a TON.DN bit to a subsequent XIC)

## Tags Window

-	Switching between Monitor and Edit shouldn’t collapse the data structure you’re within
-	When selecting “monitor tag” from context menu within a ladder, the tag window does not show the element within a data structure
-	Add a cross-reference column to the tag editor window with symbols differentiating whether a tag is used or a component within the tag is used:
    -	This tag is referenced directly
    -	A component within this tag is referenced (possibly by alias)
    -	This tag is accessed using an alias
-	When a tag is unable to be modified due to external reading/writing, allow automatic temporary modification (and restoration) of the read/write access of the tag (or base tag) with an appropriate warning

## Watch Window

-	Allow editing of tags
-	Allow right-click context menu (so you can cross reference)
-	Allow re-ordering of tags

## Safety

- Safety tags that are mapped to standard tags should be visually different when used in a safety task, rather than relying on a user's naming convention

# More than just interface
## Productivity

-	Allow Instructions to take expressions in place of numeric input values
-	A new instruction that functions as a Modulo operator that handles negative numbers and can output in a +/- range.
    -	i.e. something that could accomplish CPT ((Variable+Large_Integer*2*PI+PI) MOD (2*PI)) - PI to return a value Modulo’d to a range +/- PI
-	It would be helpful if Motor Data was retained within the Axis configuration even if it is disassociated from a servo controller in the I/O configuration. As it is, if you need to ugrade a controller to a higher current rating, you need to re-add the motor to the axis after you delete the controller and add the new one.
-	Axis Properties -> Parameter List -> Parameter Group dropdown refreshes sporadically when online making it difficult to select the correct group.
-	Add “Trend Rung” to the rung right click context menu to create a trend with the option to select up to 8 of the tags referenced within the instructions in the rung

# Things that are awful when using a slow network connection (like a cellular modem or VPN)

-	Motion Group in controller explorer takes ages to refresh if visible
-	IO configuration in controller explorer takes ages to refresh if visible
-	The above 2 are compounded by the fact that uploading automatically expands everything in controller organiser
-	Auto-hide controller organiser seems to poll each visible device/axis at each frame of its opening animation
-	Who Active shouldn’t immediately try to connect to the previously selected device
    -	Or even better would be if attempted communications happened in a separate thread, so the GUI was still responsive
-	There is no distinction in the trend window between lost data and unchanging data

# Bugs

-	Float a window, give that window focus, move the window over main window, lose connection. Now, the “lost connection prompt” can’t be acknowledged because it is covered by the floated window which doesn’t respond because the prompt requires acknowledgement.
-	Run a trend while zoomed in, then zoom out and data doesn’t display
-	(unreproducible) sometimes I get phantom tags that have been created while online, but don’t appear in the tag editor and can’t be selected for trends etc, but are definitely there. Going offline/online brings them back.

# Features that require significant changes

-	Save/Open human readable L5X/L5K without import/export. That would allow compare/merge of 3+ files using standard tools.
-	Data-less AOI’s that take inputs, outputs and inouts but require no retentive internal state tags. There are many small instructions that could be created to tidy up my code, but having to create instance tags for them all makes it less appealing
-	Allow STRING data type as input or output (not just INOUT) to AOI
    -	That would allow AOI data types to contain an editable name for the item that the AOI is controlling
-	Allow STRING constants within all ladder instructions that take string tags (I mostly just want CONCAT)
-	Allow more than 8 tags in a trend. If the bandwidth can cope with 8 DINTS, it can cope with lots of BOOL’s if they’re pre-packaged at the PLC end.
    -	Allow multiple separate trends to be displayed on the same time axis. This could achieve the appearance of allowing more than 8 tags in a trend AND allowing trends to be appended on-the-fly.
-	Allow adding tags to a trend while it’s running
-	Allow a large buffer for trending in the PLC so that Trends can be collected without a PC connected
-	Online editing of AOI’s. At the very least, allow edits that don’t add/remove from the data structure.
-	Allow EnableOut to be made true from the EnableInFalse Ladder of an AOI (This is obviously contentious, but could lead to some elegant simplifications in some code)
-	A “Tree” style cross-reference tool that shows all tags that have the ability to modify the value of a specific tag within a specified depth range.
    -	Show all tags that exist (and in what instructions) in logic preceding a destructive reference to the specified tag
    -	Repeat for each of those tags and show a count at each branch.
-	A dynamic cross-reference screen that automatically updates when rungs are edited online, clearly indicating which references are in iiiiii and rrrrr rungs. This would make it easier to find and change all references to a particular tag.
-	A means of using a virtual axis OR a real axis as a parameter for an AOI (similar to how motion commands can use either)(also similar to how an AOI can take a REAL in a DINT input and vice versa). This would allow easier simulation of machines
-	OTL and OTU instructions needn’t be processed for Logic-In-False. Many times I have faulted a PLC due to invalid indirect addressing in logic that shouldn’t have been processed.

# Features in Logix Designer Adjacent Software

##	Compare Tool

-	More intelligent matching of rungs
    -	When the tool detects a “deleted” rung and an “inserted” rung which contain most of the same instructions, treat it as a “modified” rung OR
    -	Allow deleted and inserted rungs to line up side by side for easier analysis
-	Allow launching of compare tool from “Offline changes have been made to this project” window
-	Allow selection of an online PLC as one part of a compare
-	Allow smooth scrolling rather than snapping to rungs when dragging the scrollbar
-	Allow zooming out
-	Scroll both sides of a compare in tag window
