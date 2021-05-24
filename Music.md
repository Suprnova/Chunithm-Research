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

## worldsEndTagName

The ``<worldsEndTagName>`` tag contains a stock array, with an ``<id>`` value that corresponds with the WORLD'S END type that the music is, and a ``<str>`` value that has the name of the WORLD'S END type in kanji. If the track is not a WORLD'S END track, then the ``<id>`` has a value of ``-1`` and the ``<str>`` has a value of ``Invalid``. 

## starDifType

The ``<starDifType>`` tag contains an unknown integer. It's possible that this value correlates to the difficulty of the music in question.

## stageName

The ``<stageName>`` tag contains a stock array with an ``<id>`` value equal to the ID of a stage, which is the background video that appears behind the field during gameplay, and can be found in the path ``root¥app¥data¥AXXX¥stage``, and a ``<str>`` value equal to the ``<name><str>`` value found in the corresponding ``Stage.xml`` file.

## fumens

``<fumens>``, which means "譜面" and is translated into simply "music", is the tag that contains all information for each individual difficulty. The fumens tag will contain 5 ``<MusicFumenData>`` tags, one for each difficulty, even if there are less than 5 difficulties.

## MusicFumenData

The ``<MusicFumenData>`` tag contains an array of information for each difficulty on the song. All tags listed below are part of the array.

### resourceVersion

The ``<resourceVersion>`` tag always contains a stock array with an ``<id>`` value of ``0`` and an empty ``<str />`` tag.

### type

The ``<type>`` tag is a stock array that contains information on which difficulty this specific ``<MusicFumenData>`` is. It has an ``<id>`` value that can be anywhere from ``0`` to ``4``. The ``<str>`` value can have a value of ``ID_00``, ``ID_01``, ``ID_O2``, ``ID_03``, or ``ID_04``, but must end with the same digit as the ``<id>`` tag's value. The ``<data>`` tag contains the name of the difficulty, which can be ``BASIC``, ``ADVANCED``, ``EXPERT``, ``MASTER``, or ``WORLD'S END``. This value has to correspond with the ``<id>`` and ``<str>`` tag in order. For example, BASIC has an ID of 0, ADVANCED has an ID of 1, and so on.

### enable

The ``<enable>`` tag can have a value of either ``true`` or ``false``. If the value is false, the difficulty will not appear. This is set to false on the WORLD'S END ``<MusicFumenData>`` tags when the song is normal, and is set to false on all difficulties besides WORLD'S END on WORLD'S END tracks.

### file

The ``<file>`` tag contains a ``<path>`` tag, which has the file name of the .c2s file associated with the specific difficulty. If the difficulty doesn't exist and is disabled, then it is replaced by an empty ``<path />`` tag.

### level

The ``<level>`` tag contains an integer equal to the level of difficulty of the song as shown in-game. If the difficulty doesn't exist, or if the difficulty is WORLD'S END, then the tag has a value of ``0``.

### levelDecimal

The ``<levelDecimal>`` tag contains an integer from 0-99 equal to the decimal difficulty of the track. This is combined with the ``<level>`` tag to create the accurate difficulty level. This level isn't seen during gameplay, but is instead used for sorting tracks by difficulty. If the difficulty doesn't exist, or if the difficulty is WORLD'S END, then the tag has a value of ``0``.

### notesDesigner

The ``<notesDesigner>`` tag is always empty, and as such is written as ``<notesDesigner />``. This is because the ``.c2s`` file contains the note designer's information instead.

### defaultBpm

The ``<defaultBpm>`` tag always has a value of ``<0>``.
