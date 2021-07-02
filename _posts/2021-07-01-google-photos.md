---
title: Exporting all photos from Google Photos
tags: [selfhosted, google, export, exif]
categories: [Self Hosted]
---

I want to move away from Google Photos, but I have *a lot* of photos in there. 
In this post, I'll explain what I did to get a nice folder with all my pictures in it.

I used Powershell on Windows 10.

## Step 0: Make a Google Photos export
To make an export of all the pictures in your Google Photos library, head over to Google Takeout and export them:

1. Go to [Google Takeout](https://takeout.google.com) and sign in
2. Deselect all services, then scroll down and select Google Photos
3. Wait for the export to be complete and then download it. 


## Step 1: Extract archives
Extract all the archives and merge the contents together

- `<downloadFoler>` is the directory where the archives are located. For me, this was `E:\Downloads`
- `<targetFolder>` is where you want the result. For me, this was `E:\`. The root of the archive contains a directory so the files ended up in `E:\Takeout`

```powershell
$files = (Get-ChildItem -Path <downloadFolder> -Filter "takeout-*").Fullname

foreach ($file in $files) {
    tar -xzf $file -C '<targetFolder>'
}
```

## Step 2: Apply metadata
Google provides the photo metadata (location, date) in a separate json file. I'd prefer to have everything inside the image file instead.

I got this command from [legault.me](https://legault.me/post/correctly-migrate-away-from-google-photos-to-icloud)

For this, I used `exiftool`. You can download it [here](https://exiftool.org) if you don't have it already.

First, move to the root directory of your Google Photos export. For me, this was `E:\Takeout\Google Photos`

You can remove the `-progress` argument to make it go faster, but I like seeing how far along it is.

```powershell
exiftool -r -d %s -tagsfromfile "%d/%F.json" `
  "-GPSAltitude<GeoDataAltitude" `
  "-GPSLatitude<GeoDataLatitude" `
  "-GPSLatitudeRef<GeoDataLatitude" `
  "-GPSLongitude<GeoDataLongitude" `
  "-GPSLongitudeRef<GeoDataLongitude" `
  "-Keywords<Tags" `
  "-Subject<Tags" `
  "-Caption-Abstract<Description" `
  "-ImageDescription<Description" `
  "-DateTimeOriginal<PhotoTakenTimeTimestamp" `
  "-FileCreateDate<PhotoTakenTimeTimestamp" `
  -ext "*" `
  --ext json `
  -overwrite_original -progress .
```

I also manually set the file creation date to ensure it matches the capture date.

## Step 3: Merge folders
Google duplicates all photos that are in an album by placing them both in a `photos from <year>` folder, as well as a folder with the album name. I want to use a different structure.

### 3.1: Everything in a single directory

- `<sourcePath>` is the Google Photos directory in the takeout archive. For me, this was `E:\Takeout\Google Photos`
- `<targetPath>` is the folder where you want to store everything. For me, this was `E:\Takeout_merged`

```powershell
$folders = (Get-ChildItem -Path "<sourcePath>" -exclude *.json).Fullname

foreach ($folder in $folders) {
    Copy-Item "$file\*" -Destination "<targetPath>"
}

```

### 3.2: Directories per year and month

I like a directory structure where pictures are sorted by year and month. 
First, create a directory for every year, with folders for each month. 

```
2020
  - 01
  - 02
  - 03
  - 04
  ...
2021
  - 01
  - 02
  - 03
  ...
```

You could write a script for this, but I just did it manually.

Then, run the following script to put all the pictures in the correct folders.

```powershell
$folders = (Get-ChildItem -Path "E:\Takeout\Google Photos\*" -Recurse -Attributes !Directory -exclude *.json).Fullname

foreach ($file in $folders) {
	$dateString = Get-ItemPropertyValue $file -Name "CreationTime"

	$year = ($dateString).ToString("yyyy")
	$month = ($dateString).ToString("MM")
	Copy-Item "$file" -Destination "D:\ordered_photos\$year\$month"
}
```

## Step 4: Delete metadata files

Now that all the metadata is back in its rightful place (i.e: the file itself), it's time to delete the json files. 
Move to the root folder where all your images are (either the folder with everything in one place, or the one with sub directories. Both work)

You can choose to keep the metadata files in place. Some software (such as Photoprism) can use it.

```powershell
Get-ChildItem *.json -Recurse | foreach {Remove-Item -Path $_.FullName }
```

## The end
That's it! Now all your pictures have the metadata where it belongs :)