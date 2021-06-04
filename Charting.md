This is a general documentation on the chart files used in the game. These files indicate the structure of the song, such as note placement and tempo.

# Things to know

* This document is not guaranteed to be 100% accurate. Some tag definitions are based on assumptions and might require further testing.
* Most counting in this file format starts from 0. A measure of 0 means at the beginning of the song, a cell of 0 means the first cell on the left, etc.
* The location for chart files can be found in ``root¥app¥data¥AXXX¥music¥musicXXXX``. The file format for charts is ``.c2s``, and are plain text files that can be opened in tools like Notepad++.
* A cell is the corresponding key for the note on the playfield. The playfield has 16 columns, numbers from 0-15 from left to right.
* A measure is a function of time containing a specific amount of beats. Each measure usually contains 4 beats, and stays relatively consistent throughout the song.
* From my experience, Chunithm will usually ignore a note unless it is formatted in a very specific way. In an existing chart file, using tab instead of space to add modifiers to notes works, while using space doesn't. This is exclusive to Notepad++ in my experience.
* Chunithm reloads ``.c2s`` files on selection. This means that it's possible to debug custom charts by simply reselecting the song that is being changed. To streamline this process, use a DANGER skill such as "今わの際" (skill ID 102005), and place ≈20 TAP notes a few measures after your custom notes. This way, you will automatically fail the track and be able to reselect the track much faster, rather than waiting for the song to finish.

# Tags

## VERSION

Usually set to 1.08.00. (denotes the version of the ``.c2s`` handler that the chart is designed for?)

## MUSIC

Usually set to 0. Likely used to be the ID for the Music before the ``Music.xml`` file contained it.

## SEQUENCEID

Usually set to 0.

## DIFFICULT

Usually set to 00. Likely used to be the difficulty (BASIC, ADVANCED, EXPERT, MASTER, WORLD'S END) for the Music before the ``Music.xml`` file contained it.

## LEVEL

Usually set to 0.0. Likely used to be the level for the chart file before ``Music.xml`` contained it.

## CREATOR

Designates the creator of the chart file. Note that this string will appear on the bottom left of the song's card on the song selection screen unless the difficulty is set to BASIC or ADVANCED.

## BPM_DEF

Designates the default BPM.

### Schema:

| 1 | 2 | 3 | 4 |
| ---- | ---- | ---- | ---- |

1 usually contains the true default BPM, or the BPM that the song starts with. 2 usually contains the alternative BPM, or the BPM that the song has the most often besides the BPM in 1. If there is no alternative BPM, then 2 mirrors 1. 3 and 4 seem to mirror 2 and 1 respectively.

## RESOLUTION

Denotes the resolution of the song. Always set to 384.

## CLK_DEF

Always set to 384.

## PROGJUDGE_BPM

Always set to 240.000.

## PROGJUDGE_AER

Always set to 0.999.

## TUTORIAL

Designates whether or not the specified track is a tutorial track.

## BPM

Designates the BPM for the specified measure of the song.

### Schema:

| Beginning Measure | Offset | BPM |
| ---- | ---- | ---- |

## MET

Designates the time signature for the specified measure of the song.

### Schema:

| Beginning Measure | Offset | Second Value | First Value |
| ---- | ---- | ---- | ---- |

It is very important to note that the values for the time signature are in reverse. It is also worth mentioning that this is purely cosmetic. The only thing that this value will affect is the placement of the thin measure lines on the playfield.

## SFL

Designates the speed of the playfield at the specified measure of the song.

### Schema:

| Beginning Measure | Offset | Duration | Multiplier |
| ---- | ---- | ---- | ---- |

It is important to note that the multiplier must have an accuracy of 0.000001, meaning that it should have six digits after the decimal point. This value will multiply the player's current playfield speed, so notes will appear faster or slower based on this value. This value is purely cosmetic, and will not affect the placement of notes in the .c2s file, only the player will see a difference. This value can also be made negative, which will result in the board moving in reverse, usually used for aesthetic purposes such as [this section of Fracture Ray's MASTER chart](https://youtu.be/5m7bMyIDoec?t=48).

# Notes

## Universal Note Schema

| Note Type | Measure | Offset | Cell | Width |
| ---- | ---- | ---- | ---- | ---- |

### Note Type

A note type is the type of note that you want to be placed at this particular point. There are various types of notes that can be used, and most of them will have additional variables that will be appended to the end of the typical schema. There will be more information later on explaining each of these notes.

#### Note Types:

* TAP (tap)
* CHR (ex-note)
* HLD (hold)
* SLD (slide)
* SLC (slide control point)
* FLK (flick)
* AIR (air)
* AUR (air up-right)
* AUL (air up-left)
* AHD (air hold)
* ADW (air downwards)
* ADR (air down-right)
* ADL (air down-left)
* MNE (mine)

### Measure

The measure is the specific measure that you want the note to be placed in. Each measure is (usually) 4 beats. The value starts from 0 and continues infinitely, although should always end with the song.

### Offset

A function of time to show how offset a note or timing point should be from the measure. This relies on the resolution of the song, designated by the RESOLUTION tag. The full resolution is an entire measure, so with a resolution of 384, the first beat of a measure would be 0, the second would be 96, the third would be 192, the fourth would be 288. To get the desired beat, divide the resolution by 4, multiply it by the beat that you want, and then subtract it by the resolution divided by 4.

For a fraction of a beat, divide the resolution by 4, then multiply it by the fraction of the beat you want. Then add that result with the desired beat.

The function for this would be:

```b(r/4)-(r/4) + f(r/4)```

where b is the desired beat rounded down to a whole number, r is the resolution of the song, and f is the fraction of the beat.

For example, if I wanted a note on the 2 1/2th beat of a 4 beat song with a resolution of 384, I would perform the following:

```
2(384/4)-(384/4) + 1/2(384/4)
192 - 96 + 48
144
```

### Cell

As stated above, the cell is the numerical ID for the column in the playfield that the note should appear in. Note that this value should be the column that the note first appears in **from the left**.

### Width

Separate from the Cell value, the Width value notes how wide the note should be, extending from the value listed in Cell to the right. The minimum value is 1, which means that the note only occupies the column listed in cell. As an example, a width of 3 on a note with a cell value of 7 would have the note occupy columns 7, 8, and 9.

## Additional Note Values

Most note types require additional information to function correctly. This section will provide an example of the schema that the note uses, followed by an explanation for any values not included in the universal schema. Any values in quotes indicate a value that is consistent with that note.

### Tap

Tap notes are the most basic notes that can be charted. They simply require the player to hit the cell that the note occupies at the required time.

#### Schema:

| "TAP" | Measure | Offset | Cell | Width |
| ---- | ---- | ---- | ---- | ---- |

Tap notes do not differ from the universal schema listed above.

### Ex-Notes

Ex-Notes are similar to tap notes, although they give the player more score for hitting them accurately.

#### Schema:

| "CHR" | Measure | Offset | Cell | Width | Unknown |
| ---- | ---- | ---- | ---- | ---- | ---- |

* Unknown: Seems to always have a value of "UP", "CE", or "DW".

### Hold

Hold notes are similar to tap notes, but require the player to keep the designated cell pressed over a continuous period of time.

#### Schema: 

| "CHR" | Measure | Offset | Cell | Width | Duration |
| ---- | ---- | ---- | ---- | ---- | ---- |

* Duration: The amount of time that the note needs to be held down for. This value is based on the same format for offset.

### Slide

Slide notes are similar to hold notes, but are capable of moving between cells while sustaining the hold. There are two types of slide notes, SLD and SLC. Slides that start with a straight line begin with an SLD, while slides that start immediately with movement start with an SLC. All slides end with an SLD note.

#### Schema:

| "SLD"/"SLC" | Measure | Offset | Cell | Width | Duration | End Cell | End Width |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |

* Duration: The amount of time that the note will take to move to the target cell. This value is based on the same format for offset.
* End Cell: The column that the slide will move towards over the duration of the slide. Similar to the Cell value, this value will be where the left side of the cell is, and can be anywhere from 0-15. To have a slide that stays straight over the duration, make the End Cell value the same as the Cell value.
* End Width: The width that the slide will have at the end of the duration. Similar to the Width value, this value can be anywhere between 1-16. If the End Width differs from the original Width, the slider will gradually shrink or expand in width over the course of the slide.

A slide will not end until you call an SLD in the same cell that another slide is in at that moment in time, without having another slide follow afterwards. Having an SLD in the middle of a continuous slide will add an additional blue note at that specific point, which is purely cosmetic. To adjust a slide without adding another note, use SLC.

The feature of sliders shaking from side to side rapidly is not a built-in function of the game, it instead simply involves having the slider move left and right a few cells on very short offsets.

### Flick

A flick note involves the player having their finger within the cells that the flick inhabits, and then swiping in any horizontal direction.

#### Schema:

| "FLK" | Measure | Offset | Cell | Width | Unknown |
| ---- | ---- | ---- | ---- | ---- | ---- |

* Unknown: Always has a value of "L". Note that this is not the direction of the flick, flick notes can be hit from either direction.

### Air

An air note involves the player raising their hands through the IR sensors above the physical keyboard. Unlike other notes, these notes act as modifiers for already existing notes. There are also different cosmetic versions of the note, however they each function identically.

#### Schema:

| "AIR"/"AUR"/"AUL" | Measure | Offset | Cell | Width | Target Note |
| ---- | ---- | ---- | ---- | ---- | ---- |

* AIR/AUR/AUL: Each of these note types are identical functionality-wise, although affect the appearance of the arrow above the note. AIR has an upwards arrow, AUR has an up-right arrow, and AUL has an up-left arrow.
* Target Note: This value designated what note the Air note "leeches" off of. You should have this note be in the same cell, measure, and offset as the Air note. It's also recommended to only use this note at the end of a note, rather than in the middle of a sustained note. This recommendation can be discarded for high-level charts.

## Air Hold

An air hold note involves having the player hold their hands up towards the sensor after performing an air note. Air holds will always end with a mid-air downwards note automatically.

#### Schema:

| "AHD" | Measure | Offset | Cell | Width | Target Note | Duration |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- |

* Target Note: This value designated what note the Air note "leeches" off of. You should have this note be in the same cell, measure, and offset as the Air note. It's also recommended to only use this note at the end of a note, rather than in the middle of a sustained note. This recommendation can be discarded for high-level charts.
* Duration: The amount of time that the note will take to move to the target cell. This value is based on the same format for offset.

To have mid-air downwards notes in a sustained air note, make the first air hold note last until the point where the mid-air note would be, then add another air hold note that starts at the same offset where the preceeding air hold note ends.

### Downwards

A downwards note involves the player lowering their hands through the IR sensors above the physical keyboard. Unlike other notes, these notes act as modifiers for already existing notes. There are also different cosmetic versions of the note, however they each function identically.

#### Schema:

| "ADW"/"ADR"/"ADL" | Measure | Offset | Cell | Width | Target Note |
| ---- | ---- | ---- | ---- | ---- | ---- |

* ADW/ADR/ADL: Each of these note types are identical functionality-wise, although affect the appearance of the arrow above the note. ADW has a downwards arrow, ADR has a down-right arrow, and ADL has a down-left arrow.
* Target Note: This value designated what note the downwards note "leeches" off of. You should have this note be in the same cell, measure, and offset as the downwards note. It's also recommended to only use this note at the end of a note, rather than in the middle of a sustained note. This recommendation can be discarded for high-level charts.

### Mines

A mine note involves the player not touching the cell that the mine is placed on. Touching the cell will result in the player losing score and possibly failing the track.

| "MNE" | Measure | Offset | Cell | Width |
| ---- | ---- | ---- | ---- | ---- |

Mine notes require the same information as Tap notes, and simply follow the universal schema mentioned above.

# Notes Demonstration

Below is a recreation of the MASTER difficulty chart for Cyaegha, which has a RESOLUTION of 386.

```
TAP	8	0	6	4
TAP	8	0	12	4
SLC	8	96	4	4	7	3	4
TAP	8	96	10	4
SLC	8	103	3	4	10	2	4
SLC	8	113	2	4	13	1	4
SLC	8	126	1	4	22	0	4
SLD	8	148	0	4	236	0	4
TAP	8	192	8	4
SLC	8	288	6	4	4	7	4
SLC	8	292	7	4	12	9	4
SLC	8	304	9	4	9	10	4
SLC	8	313	10	4	12	11	4
SLC	8	325	11	4	23	12	4
SLD	8	348	12	4	36	12	4
AHD	9	0	0	4	SLD	192
CHR	9	0	4	8	CE
AIR	9	0	4	8	CHR
AHD	9	0	12	4	SLD	192
TAP	9	288	3	4
TAP	9	288	9	4
```

Below is what the gameplay for this section looks like. This will be broken down into each line of the excerpt above to see their corresponding patterns in gameplay.

![Demonstration of Cyaegha Excerpt](https://raw.githubusercontent.com/Suprnova123/Chunithm-Research/main/_assets/cyaegha%20example.gif)

The two tap notes at the beginning appear as:
```
TAP	8	0	6	4
TAP	8	0	12	4
```

The order of values in these lines is the following:

``Tap note | on the 8th measure | with an offset of 0 | starts on cell 6/cell 12 | extends 4 cells to the right``

You can tell that these notes are supposed to occur at the same time because they share the same measure and offset. Remember that the cells are labelled as 0-15, meaning that the first cell on the left is cell 0.

The next two notes are a slide and a tap that occur at the same time. These appear in the document as:
```
SLC	8	96	4	4	7	3	4
TAP	8	96	10	4
```

Note that the slide has the note type of SLC, since the slider starts in motion. If the slider was stationary at the beginning, it would've had an SLD note type.

The order of values for the slide note is the following:

``Slide note | on the 8th measure | with an offset of 96 | starts on cell 4 | extends 4 cells to the right | has a duration of 7 resolution | ends on cell 3 | ends with a width of 4``

There are a few important things to note here. For one, with a measure of 8 and an offset of 96, this means that the note happens on the second beat of the 8th measure (remember, an offset of 0 means the first beat). It also has a very short duration, at only 7 resolution. This means that the slider only lasts for almost 2/100th of a measure. The reason it's so short is because it's designed to look like a curve. There are later SLC notes that attach to the first slider that gradually change to the shape to a curve.

The tap note later on has an order of values of:

``Tap note | on the 8th measure | with an offset of 96 | starts on cell 10 | extends 4 cells to the right``

Again, since the two notes occur at the same measure and offset, they are simultaneous.

The next notes are several control points for a slider, as well as creating a new slider, and a tap note. Their lines are:
```
SLC	8	103	3	4	10	2	4
SLC	8	113	2	4	13	1	4
SLC	8	126	1	4	22	0	4
SLD	8	148	0	4	236	0	4
TAP	8	192	8	4
SLC	8	288	6	4	4	7	4
SLC	8	292	7	4	12	9	4
SLC	8	304	9	4	9	10	4
SLC	8	313	10	4	12	11	4
SLC	8	325	11	4	23	12	4
SLD	8	348	12	4	36	12	4
```

There are several important things to note here. For one, the SLCs at the top are within very quick succession of each other. As stated above, this is because it's creating a curved slider, so it's very precise to look smooth. There is also an SLD immediately after it, which has a duration of 236 resolution. This is important because you can see that this slider is supposed to end at the same time as the other slider. If you add together the offset, which is 148, and the duration, you'll get a value of 384. If you add together the offset and duration of the second SLD at the bottom, you also get 384. Since they are both on the same measure, this shows that they will end at the same time as each other. It's also worth mentioning that the second pair of SLCs are not related to the first pair. They start on a separate cell from the other slider, so it creates a new slider instead of extending a previous one.

The final part of the excerpt contains several air notes, an air hold, an ex-note, and several tap notes. These appear in the file as:
```
AHD	9	0	0	4	SLD	192
CHR	9	0	4	8	CE
AIR	9	0	4	8	CHR
AHD	9	0	12	4	SLD	192
TAP	9	288	3	4
TAP	9	288	9	4
```

You'll notice that both AHDs, the AIR, and the CHR notes all start at the same time, since they share the same measure and offset. Let's break down each note.

The AHD notes represents the following:

``Air hold note | on the 9th measure | with an offset of 0 | starts on the 0th cell/12th cell | extends to the right by 4 cells | leaches off of the Slider note that occupies that same cell | has a duration of 192 resolution``

The CHR note represents:

``Ex-note | on the 9th measure | with an offset of 0 | starts on the 4th cell | extends to the right by 8 cells | CE modifier``

The AIR note represents:

``Air note | on the 9th measure | with an offset of 0 | starts on the 4th cell | extends to the right by 8 cells | leaches off of the ex-note that occupies the same cell``

The excerpt finally ends with two TAP notes, which mean the following:

``Tap note | on the 9th measure | with an offset of 288 | starts on the 3rd/9th cell | extends to the right by 4 cells``

This concludes the analysis of this excerpt of Cyaegha.

# Ending Tags

**Note:** Although resulting from minimal testing, these values do not seem to influence the functionality of the track. As such, they can be completely ignored when creating custom tracks.

## T_REC_XXX

``XXX`` is replaced with the shorthand for a note type (TAP, CHR, FLK, MNE, HLD, SLD, AIR, AHD), as well as one field labeled ``T_REC_ALL``. Appears to be a count of the amount of notes of the specified type that are in each chart. ``T_REC_ALL`` is equal to the values of the preceeding ``T_REC_XXX`` fields added together.

## T_NOTE_XXX

Seems to be identical to ``T_REC_XXX``, although the values are different from each other despite being in the same chart.

## T_NUM_XXX

Seems to be identical to ``T_REC_XXX`` and ``T_NOTE_XXX``, although there is no ``T_XXX_ALL`` field,  instead there is an unknown ``T_NUM_AAC`` field.

## T_CHRTYPE_XX

``XX`` is replaced with the shorthand for the CHR note's modifiers (UP, DW, CE). Appears to count the amount of CHR notes with the specified modifier in the track.

## T_LEN_XXX

``XXX`` is replaced with the shorthand for "sustain" notes (HLD, SLD, AHD, ALL), as well as one field labeled ``T_LEN_ALL``. Seems to be identical to ``T_REC_XXX``, although it instead counts the amount of milliseconds that the specified type of "sustain" note is active. ``T_LEN_ALL`` is equal to the values of the preceeding ``T_LEN_XXX`` fields added together.

## T_JUDGE_XXX

Unknown.

## T_FIRST_XXXX

Has two tags, ``T_FIRST_MSEC`` and ``T_FIRST_RES``. Both denote the timestamp of the first note in milliseconds and resolution respectively.

## T_FINAL_XXXX

Has two tags, ``T_FINAL_MSEC`` and ``T_FINAL_RES``. Both denote the timestamp of the last note in milliseconds and resolution respectively. This is not necessarily equal to the timestamp of the note listed in the chart file, as sustained notes will move the timestamp to when the note is finished.

## T_PROG_XX

Has 20 tags, starting from ``T_PROG_00`` and progressing to ``T_PROG_95`` as the final tag in increments of 5. Unknown.

# Cosmetics

This portion of the document will outline various cosmetic information on the notes found in game. This is NOT about generic information on the notes, like what the exact color of a note is, but rather the small details that might be useful to know when creating custom charts. This information does not have any bearing on gameplay.

## Flick Notes

Flick notes appear as a gray note with a small blue note inside of it. The blue note has a third of the width of the flick note and is centered on the note.

## Air/Down Notes

Both air and down notes have an arrow either above or below the note that it leeches off of, which has the same width as the note in question. Angled versions of these notes are always angled in a way that points to the cell immediately to the left or right of the original note.