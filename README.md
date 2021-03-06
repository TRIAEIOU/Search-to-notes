# Search to notes
Search to notes is an Anki addon (https://ankiweb.net/shared/info/1034341786) to rapidly generate notes from an image web search (Anki forum thread: https://forums.ankiweb.net/t/search-to-notes-support-thread/16286).

**CREDIT TO DEEPAN (HTTPS://GITHUB.COM/DEEPANPRABHU) FOR INSPIRATION FOR THE DDG API IMPLEMENTATION (HTTPS://GITHUB.COM/DEEPANPRABHU/DUCKDUCKGO-IMAGES-API)**

Search to notes (S2N) is designed to rapidly generate notes from a list of terms, such as a list of anatomy names (for all of us that tend to get lists with 400 Latin names that are on the next exam).
1. Paste/load the list
2. Specify the search query template and run the query
3. Select which images to use for each term
4. Specify note details and generate notes

## 1. Paste/load list
Edit the search terms manually, in the Enter/paste window or load them from a text file (each line will be interpreted as a search term). The terms will be parsed and “split” on tab character and the sum as well as part available in the query template (see below). Remarks:
- Ctrl+return will close (accept) the Enter/Paste window, escape will cancel.
- When new terms are loaded (even if they are the same as the old ones) all downloaded files are removed (of course everything that has already been generated to notes is retained inside Anki).
<img src="https://github.com/TRIAEIOU/Search-to-notes/blob/main/Screenshots/1.jpeg" height="400">

## 2. Specify search query template and run the query
The template will be applied to each term using the following substitution:
- %0 – will be replaced with the complete term
- %1 – will be replaced by the first part of the term (everything up to the first tab character, i.e. if there are no tab characters it will be the same as %0)
- %2 – will be replaced by the second part of the term (everything between the first and second tab character), etc.
- Any %<digit> that doesn’t have a corresponding part in the term (i.e. %3 in the template when a term only has one tab character) is deleted.
The search syntax is as follows:
- cats dogs => cats or dogs in results
- "cats and dogs" => Exact term "cats and dogs" in results
- cats -dogs => Fewer dogs in results
- cats +dogs => More dogs in results
- site:wikipedia.org => Only results from wikipedia.org
- intitle:anki => Only results with page title including "anki"
- maxn:10 => Only first 10 results (all if omitted)
Remarks:
- I think all med students know of sites that have a lot of useful anatomy images with specific parts highlighted, I will refrain from spelling it out lest they change their site to make things like this more difficult.
- It is likely useful to set nmax – the image search and downloading is slow and the relevance gets lower rather rapidly.
- When pressing “Search” a dialog will present the terms and their respective search query to allow the user to inspect and abort if there was some mistake in the template.

## 3. Select which images to use for each term
Select (so that they are highlighted) the relevant images for each term (S2N remembers which images are selected for each term as you swap between them). Remarks:
- All actions can be made with the mouse (selecting term, selecting/deselecting images).
- Keyboard shortcuts for moving down and up in the list of terms (default ‘S’ and ‘W’ respectively) even when out of focus reduces the need for mouse movement to allow rapid iteration through the terms.
- Movement between the image thumbnails can be done with the arrow keys, space bar will select/deselect.
- A zoom view is available by right click/return on a thumbnail. Escape, return, right and left click closes the zoom window (it can also be left open).
- The size of the images in the thumbnail view can be set in the config.
<img src="https://github.com/TRIAEIOU/Search-to-notes/blob/main/Screenshots/2.png" height="400">

## 4. Specify note generation details
Select deck, note type, and in which field the terms and images go respectively (e.g. term on front, images on back or vice versa). Remarks:
- The max size of the images can be set in the config file (images that are larger are scaled down to the max retaining proportions).
- For basic style notes one note of the specified type per term will be generated to the selected deck, term and images inserted in the specified fields.
- For cloze style notes one note of the specified type will be generated and each term/image inserted as a cloze, either with the term as prompt and the image(s) inside the cloze or vice versa. With the term as prompt the clozes will be inserted with a line break between each “pair”. With the image(s) as prompt the clozes will be inserted as a table (table attributes adjustable in the config, i.e. you can insert style=”color: red;” or add a CSS class etc.) to be able to see which images and cloze belong together.
- Once generated a dialog will list any terms that did not get any notes/clozes (because no images were found in the search or no images were selected) to allow copying those to run another query on or create those notes some other way.
<img src="https://github.com/TRIAEIOU/Search-to-notes/blob/main/Screenshots/3.png" height="400">

## Remarks
The results returned by the DDG API are somewhat mediocre, anyone that is up for it can plug in another search engine (requirements in the source, but basically provide a search function that returns a list of matches as well as functions that return tooltip and legend strings).
We will see what explodes with 2.1.50 and the move to Qt 6.

## Changelog
- 2022-01-01: Prepare code for Anki Qt5 to Qt6 transition. Added local error logging.
- 2022-05-18: Bug fixes
