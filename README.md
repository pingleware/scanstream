# ScanStream
A native Mac app to interface between scanners and JSON clients.

## API

ScanStream provides a HTTP+JSON interface on `localhost`. By default it runs on port 8080, but this can be changed as follows:

    defaults write com.counsyl.ScanStream SSServerPort -int 54321

To reset:

    defaults delete com.counsyl.ScanStream SSServerPort

### Interface details by example

    GET /ping
    {"ready": true}

    GET /scan
    {"error": "<error message>"}

    GET /scan
    {"files": ["temp_file_id_1", "temp_file_id_2", ...]}

    GET /download/temp_file_id_1
    {"data": "<base64-encoded data>", "type": "image/jpeg"}

Files are returned in the order they were scanned (to the extent that the OS X
ICScannerDevice API does so — this is not in fact documented).

## Building

TL;DR: run `make`.

The project manages one dependency using [CocoaPods](http://cocoapods.org/), namely [RoutingHTTPServer](http://cocoadocs.org/docsets/RoutingHTTPServer/). To update to the latest release of it, run `pod update`. This is not necessary if you are building for the first time.

`ScanStream.xcworkspace` is the main workspace file which contains both the ScanStream and CocoaPods projects. Building the ScanStream scheme (likely the default when you open the workspace) will build everything.

### Versioning

For ease of debugging, ScanStream displays its build version
(`CFBundleVersion`) and marketing version (`CFBundleShortVersionString`) in the
main window's title bar.

To increment the build version, run `agvtool bump`. To set a new marketing
version, run `agvtool new-marketing-version 1.2.3`.