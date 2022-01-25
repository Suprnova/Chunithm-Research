This is a list of general information that should be known regarding Chunithm's file format, as well as this collection of research. This includes a list of files of interest, the general overview of them, and links to additional documentation if available, as well as meta information about this research document.

# Meta

* This guide is **not** guaranteed to be up to date with the current version of Chunithm. This guide was written with Chunithm Paradise in mind. While I assume that almost all information here will continue to be relevant in later versions of Chunithm, I cannot guarantee that it will be 100% compatible with later releases, such as Paradise Lost and NEW. Additionally, AIR SLIDE notes and AIR CRUSH notes, which made their appearances in NEW, do not have charting documentation yet. This may change in the future.
* This is **not** a guide for creating custom songs in Chunithm "clones". This includes programs like SUSPlayer, Laverita, or Seaurchin. These games use different chart formats and have an entirely different, usually streamlined, way of implementing custom songs.
* Chunithm makes frequent use of ``.xml`` files. This document will, for the sake of simplicity, assume that you understand the basic format of ``.xml`` files.
* References to "music" and "song" will refer to the files in the ``music`` folder, which includes ``Music.xml``, as well as the chart files. References to ``audio`` will refer to the files in the ``cueFile`` folder.
* If anyone makes a tool to streamline any process outlined in this document, while credit to this document obviously isn't required (see [UNLICENSE](https://github.com/Suprnova123/Chunithm-Research/blob/main/UNLICENSE)), it would still be appreciated.

# How Songs End

When playing a song in Chunithm, the chart will "end" after the last note. This is where the animation for the progress bar at the top and the FULL COMBO/ALL JUSTICE graphic appear. However, the song will "end" after the audio file is finished playing. This is where any skills that occur at the end of a song (such as SUPPORT skills) will activate, and the results screen will appear shortly after.

# MASTER and WORLD'S END Difficulties

MASTER difficulties for songs are inaccessible unless one of two conditions are fulfilled:

* The player has passed the EXPERT difficulty of the song with an S rank or higher, OR

* The player is using a ticket that allows playing MASTER difficulty songs. (Noted as enabled in the ticket's ``Ticket.xml`` file under the ``<playMaster>`` field)

When creating custom songs, it is important to note this. Charters should always have a valid, completable chart for the EXPERT difficulty if they intend to have their chart have a MASTER difficulty. Otherwise, the chart should be set to one of the other 3 normal difficulties.

WORLD'S END difficulties for songs are inaccessible unless the player is using a ticket that allows playing WORLD'S END songs. (Noted as enabled in the ticket's ``Ticket.xml`` file under the ``<playWorldsEnd>`` field) When creating custom songs, it is inadvisable to create WORLD'S END charts. It is impossible for the player to access these charts unless they are connected to an AIME or Minime server, and purchase or cheat in a WORLD'S END ticket.

# Folders

Chunithm's method of receiving updates involves storing the new information in separate "AXXX" folders, found in ``root¥app¥data``. These folders will have varying numbers replacing the Xs depending on the update. Any references to "AXXX" in this document will refer to an unspecified ``A`` Folder. It is worth noting that, while songs usually have their complementary files (audio, jackets, rights) in the same ``A`` folder, it is possible that they are also in other folders. At the moment, it is assumed that newer AXXX folders will overwrite the older AXXX folders' data in terms of being in-game, although the older files will remain intact, however this is not confirmed. It is worth noting that Chunithm's updates will regularly remove certain songs that were prexisting, usually from rights expiring. It is also worth noting that the major updates for Chunithm that change branding and add new features (for example, Amazon to Crystal, or Crystal to Paradise) will not involve new AXXX files, instead condensing them all into the A000 folder. The .exe in ``root¥app¥bin`` may also be overwritten, among other binaries.

# File Types

This is a list of file types of interest that do not have a dedicated page for them, as well as the locations of them and links to additional info if necessary. This is **not** an extensive list, some files that are not of interest will not be included.

## Audio Files

Audio files for music are found in ``root¥app¥data¥AXXX¥cueFile¥cueFileXXXXXX``. The ID of the cueFile can be found in the XML ``<cueFileName>`` tag of the ``Music.xml`` file in the same folder as the chart files for the song of interest. More often than not, these files share the same ID as their corresponding music ID. These files are encoded in the proprietary [CRIWARE ADX2 audio format](https://en.wikipedia.org/wiki/ADX_(file_format)), in pairs of ``.awb`` and ``.acb`` files. These files can be played and converted by the [vgmstream](https://vgmstream.org/) library, specifically the component for [foobar2000](https://www.foobar2000.org/). Information on how to encode your own files into this format can be found in the [Customs](https://github.com/Suprnova123/Chunithm-Research/blob/main/Customs.md) document.

## Jacket Files

Jacket files, otherwise known as the images that are associated with the song, are found in the same folder as the chart files in a ``.dds`` (DirectDraw Surface) file format, which can be opened in software such as [GIMP](https://www.gimp.org/). Jacket files are always in a resolution of 300x300. To imitate the same file size as Chunithm's jackets, although not usually necessary, export any custom ``.dds`` jacket files with BC1 / DXT1 compression from GIMP's export settings.

## Rights Files

Rights files are the images that appear on the bottom left side of the song selection screen for specific songs. They are intended to be used as the file containing the text itself, as the image behind the text is its own separate texture that is reused for every rights file. Rights files are always formatted in a ``.dds`` (DirectDraw Surface) file format in a resolution of 512x48, and can be found in ``root¥app¥data¥AXXX¥rightsInfo¥rightsInfoXXXXXX``. To imitate the same file size as Chunithm's rights files, although not usually necessary, export any custom ``.dds`` rights files with BC1 / DXT1 compression from GIMP's export settings.

# Dummies

Dummy files are used for textures to serve as a template for how the game expects them to be formatted, mostly in terms of resolution. Note that the ``.png`` versions for these files are provided for convenience, all final versions should still be in a ``.dds`` format.

## Jacket Dummies

* [.dds](https://github.com/Suprnova123/Chunithm-Research/blob/main/_assets/jacket_dummy.dds)
* [.png](https://github.com/Suprnova123/Chunithm-Research/blob/main/_assets/jacket_dummy.png)

## Rights Dummies

* [.dds](https://github.com/Suprnova123/Chunithm-Research/blob/main/_assets/rights_dummy.dds)
* [.png](https://github.com/Suprnova123/Chunithm-Research/blob/main/_assets/rights_dummy.png)
