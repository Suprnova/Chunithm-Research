Getting Chunithm to recognise and add your custom song into the song selection screen is an unintuitive process, so this explains the basics on how to properly add customs.

# Formatting Files

Because of the nature of the game, Chunithm is very specific on what kinds of files it expects and what kind of specifications these files have. If these specifications are incorrect, Chunithm will simply refuse to show the song on the song selection screen, without showing a clear reason why. You can find a quick overview of the kinds of files that Chunithm expects to see on the [General Information](https://github.com/Suprnova123/Chunithm-Research/blob/main/General.md#file-types) page.

## Images

The two types of image files that you'll likely be dealing with are Jackets and Rights. Jacket files are the "cover art" for the song, visible on the song selection screen, during gameplay, on the results screen, and elsewhere. Rights files are the rights information that appears at the bottom left of the screen when selecting the associated song. Information on the formats for these files can be found in the [General Information](https://github.com/Suprnova123/Chunithm-Research/blob/main/General.md#file-types) page.

## Audio

Audio is the most difficult file to get right. It's encoded in a proprietary audio format by CRIWARE called ADX2, and as such is hard to replicate. Fortunately, there are tools that can both decode and encode these files. This section will focus primarily on encoding custom files into this format. For information on decoding and extracting these files, see [General Information](https://github.com/Suprnova123/Chunithm-Research/blob/main/General.md#audio-files).

### Necessary Programs

* [SonicAudioTools](https://github.com/blueskythlikesclouds/SonicAudioTools)
* [VGAudio](https://github.com/Thealexbarney/VGAudio)
* [HXD](https://mh-nexus.de/en/hxd/)
* [Audacity](https://www.audacityteam.org/) (optional, useful for adjusting volume, trimming, finding preview positions, and converting audio files to ``.wav``s.)

### Extraction

In order to make custom ADX2 songs, we first have to extract an existing one. It's recommended to backup the files you're extracting, as you'll be replacing them for the purposes of this method, and you'll want to replace the files again afterwards to prevent your game from having overwritten songs. To start, navigate to ``root¥app¥data¥AXXX¥cueFile`` and select any ``cueFileXXXXXX`` folder. In a separate File Explorer window, open the SonicAudioTools folder. Drag the ``.acb`` file from the cueFile folder into ``AcbEditor.exe``. A new folder will be created in the cueFile folder. In this folder, there will be a ``.hca`` file. We don't have to do anything with this ``.hca`` file for now, we will be overwriting it instead.

### Preparing the File

First, you'll want to get the audio file that you want and putting it into Audacity or your audio editor of choice. The two things you'll want to do for now is to adjust the volume so that it has an average level of -16dB. This can be seen in Audacity with the Contrast option under Analyze. Next, you'll want to trim the song to the desired length. Songs in Chunithm usually range from 2 to 3 minutes, and you'll want to trim your song down to be around that range. If your song is longer than 3 minutes, you might want to shorten it by removing some parts in the middle of the song, such a second verse and chorus. Make sure it sounds natural! Afterwards, export the file as a 16-bit .wav file.

### Encoding

Open VGAudio and find the exported ``.wav`` file that you just made. Use the program to convert it into ``.hca``. It might be labeled as simply "HCA" or "CRI HCA". Place your new ``.hca`` file in the folder that you extracted the first ``.hca`` file, then overwrite the existing file with the same name. Drag the parent folder that contains the ``.hca`` file and drop it onto ``AcbEditor.exe``. If everything was done correctly, you'll have overwritten the ``.acb`` and ``.awb`` files with your own custom files.

### Final Touches

Rename your new ``.acb`` and ``.awb`` files with the ID of your custom song. If you haven't created the custom Music.xml file yet, just create your own unique ID. Finally, open the ``.acb`` file in HxD. Use ``CTRL + F`` and search for "music". Find any fields that contain the previous ID of the original ``.acb`` file, and replace them with the new ID. Save the ``.acb`` file, and put the file pair in a safe place. This will be used in a future step.

# Putting It All Together

This section will focus on the files and directories that you'll have to create and edit.

## New Folders

### Adding the CueFile

In the ``root¥app¥data¥AXXX¥cueFile`` directory, create a new folder and name it ``cueFile00XXXX``, replacing ``XXXX`` with the ID given to the custom ``.acb`` and ``.awb`` files. Drag and drop your custom ``.acb`` and ``.awb`` files into this folder. Create a new file and call it ``CueFile.xml``. Copy and paste the contents of a ``CueFile.xml`` file from another folder into this new file. Replace the ``<dataName>``, ``<name><id>``, ``<name><str>``, ``<acbFile><path>``, and ``<awbFile><path>`` tag values with the appropriate values, usually by replacing the IDs with the correct ones.

### Adding the Music

In the ``root¥app¥data¥AXXX¥music`` directory, create a new folder and name it ``musicXXXX``, replacing ``XXXX`` with the custom ID. Create a new file here called ``Music.xml``, and copy and paste the contents of an existing ``Music.xml`` file into this file. Follow the specifications explained on the [Music](https://github.com/Suprnova123/Chunithm-Research/blob/main/Music.md) document to configure this file. You'll also need the ``.c2s`` files in this directory. You can copy and paste existing ``.c2s`` files with no edits into this directory if you just want the song to appear on the song selection screen.

### Adding the RightsInfo (optional)

This section is optional unless you want to add your own custom RightsInfo image. In the ``root¥app¥data¥AXXX¥rightsInfo`` directory, create a new folder and name it ``rightsInfoXXXXXX``, replacing ``XXXXXX`` with a unique ID, which can be separate from your custom song's ID. Move your custom Rights file into this folder and name it ``CHU_UI_Rights_XXXX.dds``. Create a file called ``RightsInfo.xml`` and copy and paste the contents of an existing ``RightsInfo.xml`` file into the new file. Replace ``<rightsText>`` with a general overview of what your rights image says, ``<name><id>`` with the same ID as the parent folder, excluding any preceding 0s, ``<name><str>`` with what your custom rights image says, and ``<image><path>`` with the file name of the ``.dds`` file that you added earlier.

## Edited Files

### Editing MusicSort

The ``MusicSort.xml`` file, found in the ``root¥app¥data¥AXXX¥music`` directory, lists the order of every song in the song selection menu. This is independent from the genre that the song is under, although is still formatted with the genres in mind. To add your song, simply create a new ``<StringID>`` tag with the ``<id>`` and ``<str>`` tags being replaced with the song's custom ID and the name of the song respectively.