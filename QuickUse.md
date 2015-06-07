# Integrating #
[Checkout](http://code.google.com/p/android-file-folder-picker/source/checkout) or ([download and unzip](http://android-file-folder-picker.googlecode.com/files/FilePickerLibrary.zip)) this project to your machine and import this project into the same _eclipse_ **workspace** as that of your _Android Application project_.
Now right click on your Application Project, click **Properties** > **Android**  and add the FilePicker Project as a **Library** to your application Project

Now add the following activity tag to your Application Project Manifest's application tag.
```
<activity android:name="com.coderplus.filepicker.FilePickerActivity"/>
```
Now import the **FilePickerActivity** into your Application Project's **Activity** ( The one from which you would want to trigger the FilePicker )
```
 import com.coderplus.filepicker.FilePickerActivity;
```
# Invoking the File/Folder Picker #

Use the following code to invoke the file picker from your **Activity**
```
//Some random integer used to identify the intent so that the data returned back can be identified
static int REQUEST_PICK_FILE = 777;
```
```
Intent intent = new Intent(this, FilePickerActivity.class);
startActivityForResult(intent, REQUEST_PICK_FILE);
```

FilePicker will return a list containing files/directories which were selected.You can grab the list using the following code:
```
@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
	if(resultCode == RESULT_OK) {
		switch(requestCode) {
		case REQUEST_PICK_FILE:
		if(data.hasExtra(FilePickerActivity.EXTRA_FILE_PATH)) {
			// Get the file path
			@SuppressWarnings("unchecked")
			List<File> files = (List<File>)data.getSerializableExtra(FilePickerActivity.EXTRA_FILE_PATH);			
                        //Print the File/Folder  names		
			for(File file:files){
                          if(file.isDirectory())
			   System.out.prinln("Directory : "+file.getAbsolutePath());
			 else
			   System.out.prinln("Directory : "+file.getAbsolutePath());
                          }					
			}
		}
	}
}
```

# Default Configuration #
By default, this is how the picker will behave
  * Picks both **Files** and **Directories**. Long Press to pick a directory
  * Picks a single item
  * Hidden Files/Folders can't be picked
  * Initial Directory displayed in the picker is /
  * No File filtering which means that any kind of file can be picked

# Altering the Picker Configuration #
The picker configuration can be altered by sending extra fields to the FilePicker via intent data.
These are the available fields.
  * Pick Multiple items
```
intent.putExtra(FilePickerActivity.EXTRA_SELECT_MULTIPLE, true);
```
  * Pick Directories only
```
intent.putExtra(FilePickerActivity.EXTRA_SELECT_DIRECTORIES_ONLY, true);
```
  * Pick Files only
```
intent.putExtra(FilePickerActivity.EXTRA_SELECT_FILES_ONLY, true);
```
  * Set Picker's initial directory
```
//Set the initial directory to sdcard.
intent.putExtra(FilePickerActivity.EXTRA_FILE_PATH, Environment.getExternalStorageDirectory().getAbsolutePath());
```
  * Set File Filters. If you want to pick just _.jpg_ or _.png_ files, you can use this.
```
ArrayList<String> extensions = new ArrayList<String>();
extensions.add(".jpg");
extensions.add(".png");
intent.putExtra(FilePickerActivity.EXTRA_ACCEPTED_FILE_EXTENSIONS, extensions);
```

# Changing the File/Folder Icons #
> There are 7 icons used in the File Picker.
  * folder.png
  * file.png
  * file\_audio.png
  * file\_video.png
  * file\_image.png
  * file\_compressed.png
  * file\_plain\_text.png
These icons are present in different sizes in the drawable folders. You can replace them to change the file/folder icons.