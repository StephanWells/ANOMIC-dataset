# ANOMIC-dataset
This is a musical pattern annotation data set generated from a user study where 26 participants were asked to annotate 6 musical excerpts in MIDI format using a novel musical pattern annotation tool called ANOMIC.

## Background

### What are musical patterns?
**Musical patterns** represent distinct, short musical segments or phrases that are considered to be characteristic to a given piece of music and appear multiple times throughout the piece.

### What are occurrences?
**Occurrences** are simply concrete repetitions of a musical pattern. For example, a musical phrase consisting of seven notes may be found at the start of the piece, and similar repetitions of this phrase (with minor variations or in different transpositions) may appear in the middle and at the end of the piece. Thus, this seven-note musical pattern has three occurrences.

### What is ANOMIC?
[ANOMIC][1] is a novel, open-source software tool developed specifically for musical pattern annotation research. The tool runs on Windows and allows users to load a MIDI file, highlight collections of notes to classify them under patterns and occurrences, and then save their annotations to a `.jams` file.

### What is JAMS?
[JAMS][2] stands for **JSON-Annotated Music Specification**. It is a JSON-based music annotation format that allows for reproducible research in music information retrieval. The annotation data in this data set is all saved in the `.jams` format.

## User Study

### Overview
26 participants were gathered through acquaintances, emailing, and forums, to partake in an online survey where they would use ANOMIC to annotate musical patterns in 6 MIDI files. In total, 2763 occurrences of 788 patterns were annotated by the 26 participants. Participants were also asked to take a short [survey][3], and the results of that can be found in `ANOMIC-survey.csv` as a comma-delimited CSV file.

### MIDI Excerpts
The MIDI excerpts used for this data set were based on the same MIDI excerpts used by Ren et al. in the [HEMAN data set][4]. These are:

- Bach; Cantata BWV 1, Movement 6, Horn (`bach1.mid`)
- Bach; Cantata BWV 2, Movement 6, Soprano (`bach2.mid`)
- Beethoven; String Quartet, Op.  18, No. 1, Violin I (`bee1.mid`)
- Haydn; String Quartet, Op. 74, No. 1, Violin I (`hay1.mid`)
- Mozart; String Quartet, K. 155, Violin I (`mo155.mid`)
- Mozart; String Quartet, K. 458, Violin I (`mo458.mid`)

## Data

### File structure
In the root folder of this repository, you will find `ANOMIC-survey.csv`, which is a comma-delimited CSV file that contains anonymised results from the user study survey.

In the annotations directory, you will find 26 numbered folders, with each folder representing the annotations of a single participant on all six MIDI files. For example, `annotations/03/bee1.jams` represents the 3rd participant's annotations on the `bee1.mid` MIDI excerpt.

### JAMS structure
Each `.jams` file represents all annotations on a single file.

- The outermost `sandbox` object in each JAMS file contains logs of time-stamped usage of the ANOMIC tool.
- The `file_metadata` object contains basic information on the file that was annotated.
- The `annotations` object contains the bulk of the data. There will be two types of annotations, ones with a `pattern` namespace and ones with a `pattern_jku` namespace.
	+ The patterns with the `pattern` namespace represent occurrences that are simply annotated with a "start" and "end" time. No annotations in this data set are of that type.
	+ The patterns with the `pattern_jku` namespace are the ones we are concerned with, as they represent occurrences as collections of notes.

### JAMS annotation format
Each note from the MIDI file that is part of an occurrence is listed in the JAMS file. Among other data, the elements of each note annotation that we are primarily concerned with are:

- `pattern_id`: This is the ID of the pattern starting from `0`.
- `occurrence_id`: This is the ID of the occurrence starting from `0`.
- `midi_pitch`: This is the [MIDI pitch][5] of the note.
- `confidence`: This is a value between `1` (lowest) and `3` (highest) which indicates how confident the annotator was that the occurrence containing the note in question belongs to its pattern.
- `time`: This is the MIDI time in the music that the note plays in.
- `duration`: This is the MIDI duration in the music that the note plays for.

### MIDI time / duration
Time and duration values in the `.jams` files are represented as MIDI time values with 1 **PPQ (points-per-quarter)**. Rather than representing time in milliseconds/seconds/etc, MIDI time with 1 PPQ states that each value represents to musical quarter notes (crotchets) with a 1:1 ratio.

For example, if a note has a time of `7` and a duration of `0.5`, then it means that the note plays on the **seventh** quarter note (crotchet) beat in the music and is an **eighth note** (quaver), i.e. 0.5 of a quarter note (crotchet). 

## Further Reading
Please refer to my [thesis][6] for much more detailed information on this data set, the user study, findings, and implementation of the ANOMIC tool.

[1]: https://github.com/StephanWells/ANOMIC
[2]: https://github.com/marl/jams
[3]: https://tinyurl.com/annotationtoolsurvey
[4]: https://github.com/irisyupingren/HEMANanalysis
[5]: https://newt.phys.unsw.edu.au/jw/notes.html
[6]: https://pdfhost.io/v/O.xqKVEKJ_Creating_a_Tool_for_Facilitating_and_Researching_Human_Annotation_of_Musical_Patterns.pdf