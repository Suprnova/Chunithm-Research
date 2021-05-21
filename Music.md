This is a general documentation of the ``Music.xml`` file present in every music folder under the path ``root¥app¥data¥AXXX¥music¥musicXXXX¥Music.xml``. 

# Overview

``Music.xml`` is a singular file that is in the same folder as the charts for a specific song. This file is essentially the metadata of the song, and provides the game with nearly all information about the song excluding the chart itself. Note that this documentation will not include the structure of the entire XML file, only the meanings of it. To create your own ``Music.xml`` file, use a preexisting one as a template, then use the specifications listed here.

The ``Music.xml`` files in this game make frequent use of a stock array layout, shown below:

```xml
<id></id>
<str></str>
<data />
```

Any references to a "stock array" will mean that there is this array format within the value, with the ``<id>`` and ``<str>`` tags having their values specified. ``<data />`` will never contain any values, and will always be formatted as such.

# Tags

## dataName

The ``<dataname>`` tag will have a single value named after the parent folder, usually ``musicXXXX``.

## formatVersion

The ``<formatVersion>`` tag will always have a value of ``10000``.

## resourceVersion

The ``<resourceVersion>`` tag always contains a stock array with an ``<id>`` value of ``0`` and a ``<str>`` value of ``10000``.

## netOpenName

The ``<netOpenName>`` tag contains a stock array with unknown values. A possible explanation is that these values signify the update that the song was originally added to the game from.

## disableFlag

The ``<disableFlag>`` tag has a value of either ``false`` or ``true``. Enabling the disableFlag will make it so that the song does not appear on the song selection screen.

## exType

The ``<exType>`` tag has a value of an integer between 0 and 2. With a value of ``0``, the song becomes a normal song that can be selected from the song selection screen. With a value of ``1``, the song becomes a tutorial song. With a value of ``2``, the song becomes a WORLD'S END song.

## name

The ``<name>`` tag contains a stock array with an ``<id>`` value equal to the last 4 digits of the parent folder's name, removing any preceeding 0s, and a ``<str>`` value containing the name of the song as it will appear in-game.

## rightsInfoName

The ``<rightsInfoName>`` tag contains a stock array with an ``<id>`` value equal to the corresponding ``rightsInfo`` file in the ``root¥app¥data¥AXXX¥rightsInfo¥rightsInfoXXXXXX`` folder, removing any preceeding 0s, and a ``<str>`` value containing the name of the rights holder as it appears in the ``RightsInfo.xml`` file's ``name`` tag (not how it appears in-game). If the song does not need a rights disclaimer, then the ``<id>`` has a value of ``-1`` and the ``<str>`` has a value of ``Invalid``.

## sortName

The ``<sortName>`` tag contains the name of the song in a format that can be sorted alphabetically. All Latin characters become capitalized, and all punctuation and spaces are removed. For titles in Japanese, all hiragana and kanji are converted into their katakana counterpart.

## artistName

The ``<artistName>`` tag contains a stock array with an ``<id>`` value equal to the ID of the artist, and a ``<str>`` value of the name of the artist as it will appear in-game. If the artist was not previously used in a song, it should be given the same ID as the song. If an artist was previously used, it should be given the same ID as the artist ID used in those previous songs.

## genreName

The ``<genreName>`` tag contains a ``<list>`` tag, which contains a ``<StringID>`` tag, which contains a stock array, with an ``<id>`` value equal to the ID of the genre in question according to the ``GenreSort.xml`` file found in ``root¥app¥data¥AXXX¥music``, and a ``<str>`` value equal to the name of the genre as it appears in the ``GenreSort.xml`` file.

## worksName

The ``<worksName>`` tag contains a stock array, with an ``<id>`` value equal to the ID of the work that the song originates from, and a ``<str>`` value equal to the name of the work in question. This follows the same specifications as ``<artistName>``. If the song does not need a rights disclaimer, then the ``<id>`` has a value of ``-1`` and the ``<str>`` has a value of ``Invalid``.

## jaketFile

The ``<jaketFile>`` tag contains a ``<path>`` tag, with a value equal to the name of the file that contains the jacket of the song, usually found in the same directory as the Music.xml file.

## firstLock

The ``<firstLock>`` tag has a value of either ``false`` or ``true``. If the value is ``true``, then the song will not be listed on the song selection screen unless specific criteria has been fulfilled to unlock the song.

## priority

The ``<priority>`` tag always has a value of ``0``. With a value of ``1``, there does not appear to be any difference.

## cueFileName

The ``<cueFileName>`` tag contains a stock array with an ``<id>`` value equal to the ID of the cueFile as seen in the ``CueFile.xml`` file found in ``root¥app¥data¥AXXX¥cueFile¥cueFileXXXXXX``.

## previewStartTime

The ``<previewStartTime>`` tag contains an integer that designates the location in the song, in milliseconds, that the preview, the part of the song that plays when the song is highlighted on the song selection screen, will start.

## previewEndTime

The ``<previewEndTime>`` tag contains an integer that designates the location in the song, in milliseconds, that the preview will end. After ending, it will loop back to the ``<previewStartTime>``.

Todo: worldsEndTagName, starDifType, stageName, and fumens array.