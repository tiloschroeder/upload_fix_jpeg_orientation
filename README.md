# Upload Fix JPEG Orientation

## Purpose

This extension fixes the orientation of pictures with EXIF headers. It works in frontend and backend with the Symphony Upload field and the extension [Field: Unique File Upload](https://github.com/michael-e/uniqueuploadfield).

__Note__: This extension requires a little hack (use at your own risk).

## Installation

1. Upload the 'upload_fix_jpeg_orientation' folder to your Symphony 'extensions' folder.
2. On the 'Extensions' page in the backend enable it by selecting the "Upload Fix JPEG Orientation", choose 'Enable' from the with-selected menu and click 'Apply'.
3. Add a delegate (the hack) as described below.

## The hack: Add a delegate

To work this extension, it needs a delegate in the upload function of Symphony ([What is a delegate?](https://www.getsymphony.com/learn/concepts/view/delegates/)).

1. Go to the folder ```symphony/lib/toolkit``` and open the file ```class.general.php```.
2. After ```line 1468``` insert the following line:
```php
Symphony::ExtensionManager()->notifyMembers('ManipulateTmpFile', class_exists('Administration', false) ? '/backend/' : '/frontend/', array('tmp' => $tmp_name,));
```

__Note__: If you upgrade Symphony to a newer version and forget to re-insert the delegate, __this extension will do nothing__.
