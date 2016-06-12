# polarr8

Requirements: jQuery, node, and fs
Make sure the javascriptFile sets the localstorage version.

How it works: A named javascript module to give context. appVersion.checkVersion will pull the current version of the application from the localstorage, 
which is placed via the javascript file. The use of an ajax call will bring allow the app to check for a version from a specified api endpoint.
If the call is unsuccessful, due to a lack of internet, then we will recal the ajax method after 2.5 minutes. On success the ajax call will compare the loaded version
with the version specified on the endpoint. If these versions are not equal we will need to download a new javascript file. The downloaded
javascript file will need to be renamed, moved, and replace the currenty javascript file in the applications bundler. The next time the user
opens the application the bundler with new javascript file will be located and will be loaded with the new version.

Caveats: Timing does play a role, we will need to set localstorage before checking the versions. We will want to check the version early in the application
to ensure the file is replaced before the application crashes. The version on the remote site has to be kept up to date. If that version isn't updated
then every user who has the application will download a new javascript file. I doubt Apple will allow javascript to download and replace a file in the
application bundle and this will only work for the JS file. 

Implementation: 
1)With only javascript involved it maybe better to have the javascript file on a server that is served and cached to each user.
We would update the cache with a new javascript file, if the cached one is out of date.
2)Use objective C to hotpatch the code. Javascript, CSS, HTML files, and assets in your application can be manipulated. Download and replace the entire bundle
when the application is currently in use like meteor.
3)Keep asset files in the documents folder and override them based on which files are out of date through objective c. 
