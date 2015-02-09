# Zippyshare-batch-download-PHP-cURL
A PHP script that uses cURL to download an array of Zippyshare links.
_____________________________________________________________________

Run GH_dl.php to start downloading... use the zippy_batch_dl function (at the end of the file) and feed it arguments. (example included, read at the end of features)
_____________________________________________________________________
Features:
- Accepts arrays of zippyshare links, grouped by associative array that contains DL folder names.
- Adapts to temporary download link number generating algorithm changes reasonably well. (other scripts require manualy specifying it, thus having to stop downloading)
- Names files by index, as they appear in the array, then by download link number, and then by file name.
- While downloading, the file name is modified to be *.part.file name.part - when finished it is renamed to remove both .part .
- When starting a new session, always deletes partially downloaded files and starts downloading them again.
- Can choose if you want to overwrite existing files.
- Checks if files already exist by searching the folder for index number and download link number. Skips already existing complete downloads (unless overwrite is on).
- Another check if file exists, after it fetches the file name from the zippyshare page. Skips already existing complete downloads (unless overwrite is on).
- Can specify various timeout, wait and delay times.
- Can specify from which folder/link to start, and where to end (can choose 'end' to go till the end).
- Can specify download folder.
- Has a pretty extensive log (not very well formatted).
- Has a lot of error detection.
- Example included. GH_dl.php is the main file. file_list.php, GH1_example.html and GH2_example.html are just to generate a bunch of working Zippyshare links/folders to feed GH_dl.php for testing purposes.


To-Do:
- add server index to the file name, between array index and url number
- add datetimes to each log entry
- check file size first (read from site, or to get exact size, curl to get file size from header of the temp dl link - but that requires an aditional curl (if you do it, make it not request body, only header, and add other curl options to make it simpler)) If you read file size from from site, it's here: <font style="line-height:18px; font-size: 13px; font-weight: bold;">Size:</font><font style="line-height:18px; font-size: 13px;">29.52 MB</font><br />
- re-download files if size doesn't match (give an optional argument for it, that overrides the overwrite argument)
- format log to make it actually easy to read
- check and note which PHP version and libraries this script uses (I'm running it on Windows 7 with: ApacheFriends XAMPP Version 5.6.3 which uses PHP 5.6.3 (VC11 X86 32bit thread safe) + PEAR, Apache 2.4.4, libraries: glob, curl...)
- add arbitrarily nested arrays of folder/links, along with support to specify download start/end folder/link indexes by having them nested like the folder/link array
- optimize code (eg. remove various preg matches if it can be done by quicker functions, maybe a faster approach than using the glob function, refactor some code...)
- increase the dl timeout according to the dl speed, only if script execution time isn't set to 0 (infinite)
- download resume
- support for running two or more of these scripts in parallel
