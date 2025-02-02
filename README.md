# geeup: Simple CLI for Earth Engine Uploads with Selenium Support
[![Twitter URL](https://img.shields.io/twitter/follow/samapriyaroy?style=social)](https://twitter.com/intent/follow?screen_name=samapriyaroy)

![](https://tokei.rs/b1/github/samapriya/geeup?category=code)
![](https://tokei.rs/b1/github/samapriya/geeup?category=files)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.5144379.svg)](https://doi.org/10.5281/zenodo.5144379)
[![PyPI version](https://badge.fury.io/py/geeup.svg)](https://badge.fury.io/py/geeup)
![PyPI - Downloads](https://img.shields.io/pypi/dm/geeup)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
![CI geeup](https://github.com/samapriya/geeup/workflows/CI%20geeup/badge.svg)

This tool came of the simple need to handle batch uploads of both image assets to collections but also thanks to the new table feature the possibility of batch uploading shapefiles into a folder. Though a lot of these tools including batch image uploader is part of my other project [geeadd](https://github.com/samapriya/gee_asset_manager_addon) which also includes additional features to add to the python CLI, this tool was designed to be minimal so as to allow the user to simply query their quota, upload images or tables and also to query ongoing tasks and delete assets. I am hoping this tool with a simple objective proves useful to a few users of Google Earth Engine.

-If you find this tool useful, star and cite it as below

```
Samapriya Roy. (2021). samapriya/geeup: geeup: Simple CLI for Earth Engine Uploads (0.5.1).
Zenodo. https://doi.org/10.5281/zenodo.5144379
```

## ReadMe Page: [https://samapriya.github.io/geeup/](https://samapriya.github.io/geeup/)

## Table of contents
* [Installation](#installation)
* [Windows Setup](#windows-setup)
* [GEE authenticate](#gee-authenticate)
* [Getting started](#getting-started)
* [geeup Simple CLI for Earth Engine Uploads](#geeup-simple-cli-for-earth-engine-uploads)
    * [geeup init](#geeup-init)
    * [geeup selsetup](#geeup-selsetup)
    * [geeup Quota](#geeup-quota)
    * [geeup Zipshape](#geeup-zipshape)
    * [geeup getmeta](#geeup-getmeta)
    * [geeup upload](#geeup-upload)
    * [geeup tabup](#geeup-tabup)
    * [geeup tasks](#geeup-tasks)
    * [geeup delete](#geeup-delete)

## Installation
This assumes that you have native python & pip installed in your system, you can test this by going to the terminal (or windows command prompt) and trying

```python``` and then ```pip list```

**geeup now only support Python v3.4 or higher from geeup version 0.3.3**


**This command line tool is dependent on functionality from GDAL**
For installing GDAL in Ubuntu
```
sudo add-apt-repository ppa:ubuntugis/ppa && sudo apt-get update
sudo apt-get install gdal-bin
sudo apt-get install python-gdal
```
## Windows Setup
Shapely and a few other libraries are notoriously difficult to install on windows machines so follow the steps mentioned here **before installing porder**. You can download and install shapely and other libraries from the [Unofficial Wheel files from here](https://www.lfd.uci.edu/~gohlke/pythonlibs) download depending on the python version you have. **Do this only once you have install GDAL**. I would recommend the steps mentioned above to get the GDAL properly installed. However I am including instructions to using a precompiled version of GDAL similar to the other libraries on windows. You can test to see if you have gdal by simply running

```gdalinfo```

in your command prompt. If you get a read out and not an error message you are good to go. If you don't have gdal try Option 1,2 or 3 in that order and that will install gdal along with the other libraries

#### Option 1:
Starting from geeup v0.3.4 onwards:

Simply run ```geeup -h``` after installation. This should go fetch the extra libraries you need and install them. Once installation is complete, the porder help page will show up. This should save you from the few steps below.

#### Option 2:
If this does not work or you get an unexpected error try the following commands. You can also use these commands if you simply want to update these libraries.

```
pipwin refresh
pipwin install gdal
```

#### Option 3
For Windows I also found this [guide](https://webcache.googleusercontent.com/search?q=cache:UZWc-pnCgwsJ:https://sandbox.idre.ucla.edu/sandbox/tutorials/installing-gdal-for-windows+&cd=4&hl=en&ct=clnk&gl=us) from UCLA

Also for Ubuntu Linux I saw that this is necessary before the install

```sudo apt install libcurl4-openssl-dev libssl-dev```

**This also needs earthengine cli to be [installed and authenticated on your system](https://developers.google.com/earth-engine/python_install_manual) and earthengine to be callable in your command line or terminal**

To install **geeup: Simple CLI for Earth Engine Uploads** you can install using two methods.

```pip install geeup```

or you can also try

```
git clone https://github.com/samapriya/geeup.git
cd geeup
python setup.py install
```
For Linux use sudo or try ```pip install geeup --user```.

I recommend installation within a virtual environment. Find more information on [creating virtual environments here](https://docs.python.org/3/library/venv.html).

## GEE authenticate

This tool assumes that you have a Google Earth Engine account. The earthengine command line tool needs to be authenticated using a Google account.

```
earthengine authenticate
```

or in a terminal you can also use

```
earthengine authenticate --quiet
```

## Getting started

As usual, to print help:

![geeup_main](https://user-images.githubusercontent.com/6677629/114294823-bb9e7d80-9a66-11eb-95fa-07f885622020.png)

To obtain help for specific functionality, simply call it with _help_ switch, e.g.: `geeup zipshape -h`. If you didn't install geeup, then you can run it just by going to *geeup* directory and running `python geeup.py [arguments go here]`

## geeup Simple CLI for Earth Engine Uploads
The tool is designed to handle batch uploading of images and tables(shapefiles). While there are image collection where you can batch upload imagery, for vector or shapefiles you have to batch upload them to a folder.

### geeup init
**This is a key step only if you are going to use selenium method to upload imagery instead of the cookies approach added since v0.4.6. All versions before 0.4.6 requires this step, since all upload function depends on it, so make sure you run this**. This downloads selenium driver and places to your local directory for windows and Linux subsystems. This is the first step to use selenium supported upload.

``` geeup init```

![geeup_init](https://user-images.githubusercontent.com/6677629/114273320-31f79d00-99df-11eb-8960-e4f887cf9b50.gif)

### geeup selsetup
Once in a while the geckodriver/selenium requires manual input before signing into the google earth engine, this tool will allow you to interact with the initialization of Google Earth Engine code editor window. It allows the user to specify the account they want to use, and should only be needed once.

```geeup selsetup```

![geeup_selsetup](https://user-images.githubusercontent.com/6677629/114273790-24431700-99e1-11eb-86b6-f7971377725c.gif)

### geeup Quota
Just a simple tool to print your earth engine quota quickly. Since Google Earth Engine also allows you to use Cloud Projects instead of the standard legacy folders, this tool now has the option to pass the project path (usually **projects/project-name/assets/**)

![geeup_quota](https://user-images.githubusercontent.com/6677629/114274802-c6fd9480-99e5-11eb-93e4-25d6367b88da.gif)

```
usage: geeup quota [-h] [--project PROJECT]

optional arguments:
  -h, --help         show this help message and exit

Optional named arguments:
  --project PROJECT  Project Name usually in format projects/project-
                     name/assets/

```

### geeup Zipshape
So here's how table upload in Google Earth Engine works, you can either upload the component files shp, shx, prj and dbf or you can zip these files together and upload it as a single file. The pros for this is that it reduces the overall size of the shapefile after zipping them along, this tool looks for the shp file and finds the subsidiary files and zips them ready for upload. It also helps when you have limited upload bandwidth. Cons you have to create a replicate structure of the file system, but it saves on bandwidth and auto-arranges your files so you don't have to look for each additional file.

![geeup_zipshape](https://user-images.githubusercontent.com/6677629/114293099-f8637800-9a58-11eb-9873-b36df8bb4245.gif)

```
usage: geeup zipshape [-h] --input INPUT --output OUTPUT

optional arguments:
  -h, --help       show this help message and exit

Required named arguments.:
  --input INPUT    Path to the input directory with all shape files
  --output OUTPUT  Destination folder Full path where shp, shx, prj and dbf
                   files if present in input will be zipped and stored
```

### geeup getmeta
This script generates a generalized metadata using information parsed from gdalinfo and metadata properties. For now it generates metadata with image name, x and y dimension of images and the number of bands.

![geeup_getmeta](https://user-images.githubusercontent.com/6677629/114294172-56488d80-9a62-11eb-8b18-540bf8e8a39a.gif)

```
usage: geeup getmeta [-h] --input INPUT --metadata METADATA

optional arguments:
  -h, --help       show this help message and exit

Required named arguments.:
  --input INPUT        Path to the input directory with all raster files
  --metadata METADATA  Full path to export metadata.csv file

```

### Setting up Cookies
This method was added since v0.4.6 and uses a third party chrome extension to simply code all cookies. The chrome extension is simply the first one I found and is no way related to the project and as such I do not extend any support or warranty for it.

The chrome extension I am using is called [Copy Cookies and you can find it here](https://chrome.google.com/webstore/detail/copy-cookies/jcbpglbplpblnagieibnemmkiamekcdg/related)

It does exactly one thing, copies cookies over and in this case we are copying over the cookies after logging into [code.earthengine.google](https://code.earthengine.google.com)

![cookie_copy](https://user-images.githubusercontent.com/6677629/114257576-8de20780-9986-11eb-86c5-4c85e35367c3.gif)


**Import things to Note**

* Open a brand new incognito or a browser window while you are copying cookies, if you have multiple GEE accounts open on the same browser the cookies being copied may create some read issues at GEE end.
* Clear cookies and make sure you are copying cookies from [code.earthengine.google](https://code.earthengine.google.com) in a fresh browser instance if upload fails with a ```Unable to read``` error.
* Make sure you save the cookie for the same account which you initiliazed using earthengine authenticate

To run cookie_setup and to parse and save cookie user

```
geeup cookie_setup
```

* For **Bash** the cannonical mode will allow you to only paste upto 4095 characters and as such geeup cookie_setup might seem to fail for this use the following steps

* Disable cannonical mode by typing ```stty -icanon``` in terminal
* Then run ```geeup cookie_setup```
* Once done reenable cannonical mode by typing ```stty icanon``` in terminal

*Since cookies generated here are post login, theoretically it should work on accounts even with two factor auth or university based Single Sign on GEE accounts but might need further testing*

### geeup upload
The script creates an Image Collection from GeoTIFFs in your local directory. By default, the image name in the collection is the same as the local directory name. The upload tool now allows the user to copy cookie list from your browser and bypass selenium based authentication. It saves the cookie temporarily and uses it automatically till it expires when it asks you for cookie list again. Just use the ```--method cookies``` argument.

```
usage: geeup upload [-h] --source SOURCE --dest DEST -m METADATA
                    [--nodata NODATA] [-u USER] [--method METHOD]

optional arguments:
  -h, --help            show this help message and exit

Required named arguments.:
  --source SOURCE       Path to the directory with images for upload.
  --dest DEST           Destination. Full path for upload to Google Earth
                        Engine, e.g. users/pinkiepie/myponycollection
  -m METADATA, --metadata METADATA
                        Path to CSV with metadata.
  -u USER, --user USER  Google account name (gmail address).
  --method METHOD       Choose method <cookies> to use cookies to authenticate

Optional named arguments:
  --nodata NODATA       The value to burn into the raster as NoData (missing
                        data)
```

### geeup tabup
This tool allows you to batch download tables/shapefiles/CSVs to a folder. It uses a modified version of the image upload and a wrapper around the earthengine upload cli to achieve this while creating folders if they don't exist and reporting on assets and checking on uploads. This only requires a source, destination and your ee authenticated email address. This tool also uses selenium to upload the tables. The table upload tool now allows the user to copy cookie list from your browser and bypass selenium based authentication. It saves the cookie temporarily and uses it automatically till it expires when it asks you for cookie list again. Just use the ```--method cookies``` argument.

```
usage: geeup tabup [-h] --source SOURCE --dest DEST [-u USER]
                   [--method METHOD] [--x X] [--y Y]

optional arguments:
  -h, --help            show this help message and exit

Required named arguments.:
  --source SOURCE       Path to the directory with zipped folder for upload.
  --dest DEST           Destination. Full path for upload to Google Earth
                        Engine, e.g. users/pinkiepie/myponycollection
  -u USER, --user USER  Google account name (gmail address).
  --method METHOD       Choose method <cookies> to use cookies to authenticate

Optional named arguments:
  --x X                 Column with longitude value
  --y Y                 Column with latitude value
```

### geeup tasks
This script counts all currently running, ready, completed, failed and canceled tasks along with failed tasks. This tool is linked to your google earth engine account with which you initialized the earth engine client. This takes no argument.

```
usage: geeup tasks [-h]

optional arguments:
  -h, --help  show this help message and exit
```

### geeup delete
The delete is recursive, meaning it will also delete all children assets: images, collections, and folders. Use with caution!

```
usage: geeup delete [-h] id

positional arguments:
  id          Full path to asset for deletion. Recursively removes all
              folders, collections and images.

optional arguments:
  -h, --help  show this help message and exit
```
# Changelog

### 0.5.1
- Now support both zipped shapefile as well as batch CSV upload
- General Improvements

### 0.5.0
- fixed typo in version check

### v0.4.9
- Improvements to redundancy in code
- Improvements to version check for tool
- General cleanup

### v0.4.8
- Fixed issue with epoch time conversion for 1970s and issue with second vs millisecond parsing

### v0.4.7
- Both table and image upload support using cookies and better error handling.
- Improved zipshape tool to avoid error handling
- Image upload to collection now support pyramiding policy
- Cookie setup tool now auto enables long string for Linux

### v0.4.6
- Now pass cookies for authentication and image and table uploaders.
- Added readme docs and feature to the tool
- Minor improvements to the overall tool.

### v0.4.5
- Replaced firefox_options with options for selenium 3.14 and higher related to [issue 24](https://github.com/samapriya/geeup/issues/24) for selsetup
- updated earthengine-api requirement to 0.1.238
- update tasks fetch from earthengine api

### v0.4.4
- Replaced firefox_options with options for selenium 3.14 and higher related to [issue 24](https://github.com/samapriya/geeup/issues/24)

### v0.4.3
- Updated quota tool to handle Google Cloud Projects in GEE

### v0.4.2
- Fixed issue with [geckodriver path](https://github.com/samapriya/geeup/issues/22) and better path parsing
- Added CI check for geckodriver

### v0.4.1
- Fixed selenium parser issue [Issue 19](https://github.com/samapriya/geeup/issues/19)
- Implemented Cloud API fix for table uploads
- Improved Cloud API fix for Imagery upload with improved manifest handling
- Improvement and code cleanup

### v0.4.0
- Updated earthengine API library requirements to 0.1.222
- Added version check tool for auto version check with PyPI

### v0.3.7
- Revisions to account for changes to API and client library 0.1.215
- Now checks vertex count for each shapefile and logs warning with those exceeding million vertices while zipping.
- Uses table manifest to perform table uploads designed to be more robust.
- Simpler recursive delete functionality.
- Overall General improvements.

### v0.3.5-v0.3.6
- Fixed downloader for pipwin for [release >= 0.4.8](https://github.com/lepisma/pipwin/pull/41)
- Improved overall package installation for windows
- Check pipwin import version to get release 0.4.9

### v0.3.4
- Supports python3 only since v0.3.4
- Added stackoverflow based auth fix for some users [Issue 13](https://github.com/samapriya/geeup/issues/13) and [Issue 16](https://github.com/samapriya/geeup/issues/16).
- General improvements.

### v0.3.3
- Added fix for handling no data in manifests while uploading.

### v0.3.2
- Fixed issue with selsetup.

### v0.3.1
- Fixed issue with raw_input and input for selsetup.
- Fixed selenium path for windows and other platforms.
- General improvements to ReadMe

### v0.3.0
- Fixed (issue 13)[https://github.com/samapriya/geeup/issues/13] non relative import.
- Fixed issues with package import.

### v0.2.9
- Fixed issues caused by --no-use_cloud_api in earthengine-api package

### v0.2.7
- Fix to handle case senstive platform type for all os Fix to [Issue 11](https://github.com/samapriya/geeup/issues/11)

### v0.2.6
- Fixed geckodriver path to handle macos Fix to [Issue 10](https://github.com/samapriya/geeup/issues/10)

### v0.2.5
- Now allows for downloading geckodriver for macos Fix to [Issue 10](https://github.com/samapriya/geeup/issues/10)
- Now includes a metadata tool to generate a generalized metadata for any raster to allow upload.
Fix to [Issue 7](https://github.com/samapriya/geeup/issues/7)
- Changed from geeup update to init to signify initialization
- Added selsetup this tool allows for setting up the gecko driver with your account incase there are issues uploading
- Better error handling for selenium driver download

### v0.2.4
- Made general improvements
- Better error handling for selenium driver download

### v0.2.2
- Can now handle generalized metadata (metadata is now required field)
- Fixed issues with table upload
- Overall code optimization and handle streaming upload

### v0.1.9
- Changes to handle PyDL installation for Py2 and Py3
- Removed Planet uploader to make tool more generalized

### v0.1.8
- Multipart encoder using requests toolbelt for streaming upload
- Changed manifest upload methodology to match changes in earthengine-api

### v0.1.6
- Fixed issue with [module locations](https://github.com/samapriya/geeup/issues/2)

### v0.1.5
- Fixed issue with gecko driver paths
- Fixed issue with null uploads using task, switched to ee CLI upload

### v0.1.4
- OS based geckdriver path fix
- General improvements

### v0.1.3
- fixed issues with extra arguments
- Upload issue resolved
- General dependency

### v0.1.1
- fixed dependency issues
- Upload post issues resolved
- Removed dependency on poster for now

### v0.0.9
- fixed attribution and dependecy issues
- Included poster to improve streaming uploads
- All uploads now use selenium

### v0.0.8
- fixed issues with unused imports

### v0.0.7
- fixed issues with manifest lib

### v0.0.6
- Detailed quota readout
- Uses selenium based uploader to upload images
- Avoids issues with python auth for upload

### v0.0.5
- Removed unnecessary library imports
- Minor improvements and updated readme

### v0.0.4
- Improved valid table name check before upload
- Improvements to earth engine quota tool for more accurate quota and human readable
