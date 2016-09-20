#JSMultipartZIP
Downloads remote content via AJAX and compiles it into ZIP archives using JSZip and JSZipUtils.

If the content exceeds the defined maximum size for an archive, the content will be split over a number of parts.

##Dependencies
- None (JSZip, JSZipUtils and Filesaver.js included in file)

##Usage
Initialise an instance of JSMultipartZIP using the following code;
```javascript
// Parts will be called 'Package-xxxxxxxx.zip' and be a maximum of 500MB.
var downloader = new JSMultipartZIP("Package-", 0.5);
```
The first parameter is a string, and represents the prefix to add on to the generated ZIP files.
The second parameter is an number representing the maximum size of a part in GB. Check out the [Supported Browsers section in the README of Filesaver.js](https://github.com/eligrey/FileSaver.js/, Filesaver.js Supported Browsers)
