# About
After much colobaration with users on Mobile Read on this thread https://www.mobileread.com/forums/showthread.php?t=355521, we all found a way to customize the PocketBook desktop, app icons, app name and app drawer layout. Big thanks to the following users:
EastEriq
neil_swann80
nhedgehog

This was tested(on my end) with a PocketBook Era on SW Version 6.8(Latest). Another user on the thread had SW Version 5.2 with a PocketBook touch HD which appeared to work differently then what I needed to do

The prupose of this repo is to summarize these finding into an easy to follow guide.

This doesn't require root, just the ability to understand File System and JSON.
This guide assumes you have KOReader installed already to edit it's icon

IT IS VERY IMPORTANT TO BACK UP ANY FILES EDITED.

## Changing app names
Many of the custom apps installed to a Pocketbook appear as @AppName(Koreader, PbDbFix, etc.) We can control how these appear
1. Plug in your PocketBook to your PC or SSH/FTP
2. If you plugged into PC, navigate to ROOT/system/language. If SSH, cd /mnt/ext1/system/language
3. Once in the the system/language folder, create a file with your specific language accronym. For English, create en.txt
4. Enter the following
   English
   @koreader=KOReader
5. Save the file, unplug or reboot your PocketBook to view the changes.
--Notes--
This can be done for ANY custom app. Please see the attached en.txt file in this repo

## Removing icons from views
I have alot of apps I don't use on my PocketBook. While I don't want to uninstall them just in case, I do want to hide them from view
1. Plug in your PocketBook to your PC or SSH/FTP
2. If you plugged into PC, navigate to ROOT/system/config/desktop. If SSH, cd /mnt/ext1/system/config/desktop
3. Open the view.json file
4. Remove a "AppName" entry from one of the groups. This will hide the application from view.
5. Save the file, unplug or reboot your Pocketbook to view the changes
--Notes--
It's important to follow the JSON syntax. If you aren't confident in your changes you can copy the file contents into a JSON Validator. I use https://jsonlint.com/
If the JSON syntax is wrong, no big deal! Your device will still start but you may see an error popup
The only icons I have in view are Dictionary, Library, Settings and my custom apps. Please see the attached view.json file in this repo. Ignore the U_KOReader bits for now

## Adding custom app icons images
This will be different depending on FW version and maybe device. The icons have some specifics properties
-Icon has to be .bmp file format
-Icon has to be 8 bit
-You can check the bit of the image by right-clicking the file and going to properties
-The size of the image we have tested has a max of: Vertical:128px, Horizontal:106px
-Play with the size until you feel it fits for you
1. Plug in your PocketBook to your PC or SSH/FTP
2. If you plugged into PC, navigate to ROOT/applications/. If SSH, cd /mnt/ext1/applications/
3. create a new folder in /applications/ called icons
4. Copy the two files from the attached desktop_app_koreader.zip into the applications/icons/ folder
--Notes--
You can rename these file if you wish
One file is for the static image, the other file that ends in _f is for when you click this icon
### Changing the App Icon
1. Confirm that you have the two KOReader bmp image files in \system\resources\Line
2. Once confirmed, navigate to /system/config/desktop/
3. Open the view.json file
4. Add the following text between the applications and _comment key
		"U_koreader": {
			"path": "/mnt/ext1/applications/koreader.app",
			"title": "KOReader",
			"icon": "/mnt/ext1/applications/icons/desktop_app_koreader.bmp",
			"focused_icon": "/mnt/ext1/applications/icons/desktop_app_koreader_f.bmp"
		},
5. Add the following entry in one of the groups(I used the @General group)
   "U_koreader"
6. Save the file, unplug or reboot your Pocketbook to view the changes
   --Notes--
   The JSON keys can be explained as:
     path - Location to the KOReader app on your file system
     title - The title of the app. Needs to match how it's displayed on your Home screen or from the Changing app names step
     icon - location of the static icon you want to use on your file system
     focused_icon - location of the "tapped" icon you want to use on your file system
   The U_ part in U_koreader is mandatory
   After the U_ is HAS TO match the name of the app in ROOT/applications
   This can be done for any custom app
   For an example please see the attached view.json file in this repo.

# Other changes I have 
## Adding sync ability in PocketBook Library view with KOReader book progress
Please go to https://github.com/ckilb/koreader-pocketbook-sync. This user greatly increased the usability of my scrpit
## Meta data not appearing correctly in PocketBook Library view
Please go to https://git.rustysoft.de/martin/PbDbFixer

Thanks again for everyones help in this adventure :)


    
