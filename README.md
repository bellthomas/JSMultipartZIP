#JSMultipartZIP
Downloads remote content via AJAX and compiles it into ZIP archives using JSZip and JSZipUtils.

If the content exceeds the defined maximum size for an archive, the content will be split over a number of parts.

##Dependencies
- None (JSZip, JSZipUtils and Filesaver.js included in file)

##Usage
###Initialise an Instance of JSMultipartZIP
Initialise an instance of JSMultipartZIP using the following code;
```javascript
// Parts will be called 'Package-xxxxxxxx.zip' and be a maximum of 500MB.
var downloader = new JSMultipartZIP("Package-", 0.5);
```
The first parameter is a string, and represents the prefix to add on to the generated ZIP files.

The second parameter is an number representing the maximum size of a part in GB. Check out the [Supported Browsers section in the README of Filesaver.js](https://github.com/eligrey/FileSaver.js/, Filesaver.js Supported Browsers)

###Add URLs to be Downloaded and Archived
Add a single URL:
```javascript
// Adds http://www.examplesite.com/image.jpg to the queue of files to be archived.
downloader.addURL("image.jpg", "http://www.examplesite.com/");
```

Add multiple URLs:
```javascript
// Adds http://www.examplesite.com/image1.jpg and http://www.examplesite.com/image2.jpg to the queue of files to be zipped.
var urls = [
    "image1.jpg",
    "image2.jpg"
];

downloader.addURLs(urls, "http://www.examplesite.com/");
```

###Run the Archiver
```javascript
downloader.run();
```

###Print All URLs in the Queue
```javascript
downloader.printURLs();
```

###Event Handlers
JSMultipartZIP offers hooks in the execution of the archiver so custom code can be run.
```javascript
// Runs when the instance's completion percentage increases.
downloader.percentageChangeCallback(function(percentage) {
    jQuery("#downloader .progress-bar").css("width", percentage + "%").text(percentage + "%");
});

// Returns messages about the success or failure to retrieve URLs. Fires once per URL.
downloader.logCallback(function(msg) {
    jQuery("#downloader #output-log").prepend("<p>" + msg + "</p>");
});

// Runs when the archiver has finished.
downloader.onCompleteCallback(function() {
    jQuery("#downloader .progress-bar")
        .removeClass("progress-bar-primary")
        .addClass("progress-bar-success")
        .text("Done")
        .css("width", "100%");
});

// Runs if, and only if, none of the URLs requested could be retrieved.
downloader.noFilesRetrieved(function() {
    jQuery("#main-container").prepend('<p>Nothing downloaded because none of the requested files could be found.</p>');
});
```
