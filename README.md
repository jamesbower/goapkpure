# goapkpure

A Go module to download APKs from [APKPure](https://apkpure.com/).

## Installation
For package import
```go
$ go get -u github.com/adamyordan/goapkpure/cmd/goapkpure
```

To run the CLI program
```go
$ go get -u github.com/adamyordan/goapkpure/cmd/goapkpure
```

## CLI Usage

See available command flags
```bash
$ goapkpure -help
Usage of /Users/user/go/bin/goapkpure:
  -download
    	Download APK from direct link. By default download latest version. Use -version to specify version ID
  -output string
    	Download file output. (default: <packagename>.apk)
  -package string
    	Package name
  -version int
    	Get direct link for a version index
  -versions
    	List all available versions
```

List available versions of a package

```bash
$ goapkpure -versions -package com.whatsapp
  0 | version=2.19.360 (453123) | updateOn=2019-12-10 | tags=APK        | size=26.4 MB  | arch=arm64-v8a        | downloadUrl=https://apkpure.com/whatsapp-messenger/com.whatsapp/download/453123-APK?from=popup%2Fversion
  1 | version=2.19.360 (453122) | updateOn=2019-12-10 | tags=APK        | size=26.4 MB  | arch=x86              | downloadUrl=https://apkpure.com/whatsapp-messenger/com.whatsapp/download/453122-APK?from=popup%2Fversion
  2 | version=2.19.360 (453121) | updateOn=2019-12-10 | tags=APK        | size=26.4 MB  | arch=armeabi-v7a      | downloadUrl=https://apkpure.com/whatsapp-messenger/com.whatsapp/download/453121-APK?from=popup%2Fversion
  3 | version=2.19.352 (453112) | updateOn=2019-12-04 | tags=APK        | size=26.4 MB  | arch=arm64-v8a        | downloadUrl=https://apkpure.com/whatsapp-messenger/com.whatsapp/download/453112-APK?from=popup%2Fversion
  4 | version=2.19.352 (453110) | updateOn=2019-12-05 | tags=APK        | size=26.4 MB  | arch=armeabi-v7a      | downloadUrl=https://apkpure.com/whatsapp-messenger/com.whatsapp/download/453110-APK?from=popup%2Fversion  
  ...
```

Download specific version of a package.
For example, download the version number 2 of the whatsapp available versions list,
and output the file to /tmp/whatsapp.apk
```bash
$ goapkpure -version 2 -download -output /tmp/whatsapp.apk -package com.whatsapp
2019/12/11 19:30:28 Downloading from https://download.apkpure.com/b/apk/Y29tLndoYXRzYXBwXzQ1MzEyMV9lYzJkZjRk?_fn=V2hhdHNBcHAgTWVzc2VuZ2VyX3YyLjE5LjM2MF9hcGtwdXJlLmNvbS5hcGs&k=0e55154b1b7eb21d6d8a1989a7af86e45df37654&as=f39a574c3c0e8bdcbf7e05823c5b91445df0d3cc&_p=Y29tLndoYXRzYXBw&c=1%7CCOMMUNICATION%7CZGV2PVdoYXRzQXBwJTIwSW5jLiZ0PWFwayZzPTI3MzU1OTE3JnZuPTIuMTkuMzYwJnZjPTQ1MzEyMQ&hot=1
2019/12/11 19:30:30 Downloaded 0/27355917 (0.00%)
2019/12/11 19:30:35 Downloaded 949780/27355917 (3.47%)
2019/12/11 19:30:40 Downloaded 2604564/27355917 (9.52%)
2019/12/11 19:30:45 Downloaded 4242964/27355917 (15.51%)
2019/12/11 19:30:50 Downloaded 6077972/27355917 (22.22%)
2019/12/11 19:30:55 Downloaded 7732756/27355917 (28.27%)
2019/12/11 19:31:00 Downloaded 18759188/27355917 (68.57%)
2019/12/11 19:31:05 Download completed in 37.101594676s
```

## Import from a Go Project

```bash
package main

import (
    "fmt"
    "github.com/adamyordan/goapkpure"
)

func main()  {
    downloadLink, _ := goapkpure.GetLatestDownloadLink("com.whatsapp")
    goapkpure.DownloadFile(downloadLink, "whatsapp.apk")

    versions, _ := goapkpure.GetVersions("com.whatsapp")
    fmt.Println(versions[0].Signature)
}
```

The version item struct
```go
type VerItem struct {
    Version string
    DownloadUrl string
    Size string
    Tags []string
    Title string
    UpdateOn string
    Signature string
    Sha1 string
    AndroidVer string
    Architectures []string
    ScreenDPI string
}
```
