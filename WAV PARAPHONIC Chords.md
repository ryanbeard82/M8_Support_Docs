# Dirtywave M8 Macrosynth: WAV PARAPHONIC

An exploration of the chords available through the Color parameter values in the Dirtywave M8's Macrosynth instrument, as ported from the [Mutable Instruments Braids] macro oscillator eurorack module.

## Source Code

The source code for Braids is available on GitHub in the [Eurorack modules git repository](https://github.com/pichenettes/eurorack).

The Wave Paraphonic code can be found in the file [digital_oscillator.cc](https://github.com/pichenettes/eurorack/blob/master/braids/digital_oscillator.cc). Specifically, line 1736 defines the static constant "chords" array as the following:

```c
static const uint16_t chords[17][3] = {
  { 2, 4, 6 },
  { 16, 32, 48 },
  { 2 SEMI, 7 SEMI, 12 SEMI },
  { 3 SEMI, 7 SEMI, 10 SEMI },
  { 3 SEMI, 7 SEMI, 12 SEMI },
  { 3 SEMI, 7 SEMI, 14 SEMI },
  { 3 SEMI, 7 SEMI, 17 SEMI },
  { 7 SEMI, 12 SEMI, 19 SEMI },
  { 7 SEMI, 3 + 12 SEMI, 5 + 19 SEMI },
  { 4 SEMI, 7 SEMI, 17 SEMI },
  { 4 SEMI, 7 SEMI, 14 SEMI },
  { 4 SEMI, 7 SEMI, 12 SEMI },
  { 4 SEMI, 7 SEMI, 11 SEMI },
  { 5 SEMI, 7 SEMI, 12 SEMI },
  { 4, 7 SEMI, 12 SEMI },
  { 4, 4 + 12 SEMI, 12 SEMI },
  { 4, 4 + 12 SEMI, 12 SEMI },
};
```

## Testing the Dirtywave M8 Implementation

For testing, I created a new empty project file and created a single WAV PARAPHONIC instrument with a repeating C-5 note in a single phrase. I iterated through each of the Color values and documented the chord produced using both audio (listening to the chord) and visual (looking at the keyboard representation) analysis of the output.

Note that some some values are represented as microtonal increments (denoted by "c", for cents). The source code defines a semitone constant with 128 increments:
```c 
#define SEMI * 128
```

Since a semitone is equal to 100 cents, the source code's microtonal values have been divided by 1.28 to produce the resulting cent equivalency (rounded to the nearest tenth) in the table below:

| Id | Documented Semitone 1 | Documented Semitone 2 | Documented Semitone 3 | Actual Semitone 1 | Actual Semitone 2 | Actual Semitone 3 | Color Range | Chord             | Notes                             |
|----|------------|------------|------------|------------|------------|------------|-------------|-------------------|-----------------------------------|
| 1  |            |            |            | 0          | 0          | 0          | 00 - 07     | Unison            |                                   |
| 2  | 2 (1.6c)   | 4 (3.1c)   | 6 (4.7c)   | 0+         | 0+         | 0+         | 08          |                   | Microtonal (chorus effect)        |
| 3  | 16 (12.5c) | 32 (25c)   | 48 (37.5c) | 0+         | 0+         | 0+         | 09 - 17     |                   | Microtonal (chorus effect)        |
| 4  |            |            |            | 1          | 4          | 7          | 18          | Em6#5/C           | Not documented in source code     |
| 5  | 2          | 7          | 12         | 2          | 7          | 12         | 19-27       | Csus2             |                                   |
| 6  |            |            |            | 3          | 7          | 11         | 28          | C minor-major 7th | Not documented in source code     |
| 7  | 3          | 7          | 10         | 3          | 7          | 10         | 29-37       | Cm7               |                                   |
| 8  |            |            |            | 3          | 7          | 11         | 38          | C minor-major 7th | Not documented in source code     |
| 9  | 3          | 7          | 12         | 3          | 7          | 12         | 39-47       | Cm                |                                   |
| 10 |            |            |            | 3          | 7          | 14         | 48          | Cm add 9          | The 14 sounds flat here           |
| 11 | 3          | 7          | 14         | 3          | 7          | 14         | 49-57       | Cm add 9          |                                   |
| 12 |            |            |            | 3          | 7          | 17         | 58          | D#6/9/C           | The 17 sounds flat here           |
| 13 | 3          | 7          | 17         | 3          | 7          | 17         | 59-67       | D#6/9/C           |                                   |
| 14 |            |            |            | 7          | 11         | 19         | 68          | Cmaj7sus          | Not documented in source code     |
| 15 | 7          | 12         | 19         | 7          | 12         | 19         | 69-77,87    | C5 or Csus        |                                   |
| 16 | 7          |12 + 3(2.3c)|19 + 5(3.9c)| 7          | 12+        | 19+        | 78-86       | C5 or Csus        | Microtonal (chorus effect)        |
| 17 | 4          | 7          | 17         | 4          | 7          | 17         | 88-96       | C add 4           | The 17 sounds sharp here          |
| 18 |            |            |            | 4          | 7          | 17         | 97          | C add 4           |                                   |
| 19 | 4          | 7          | 14         | 4          | 7          | 14         | 98-A6       | C add 9           | The 14 sounds slightly sharp here |
| 20 |            |            |            | 4          | 7          | 14         | A7          | C add 9           | The 14 sounds slightly flat here  |
| 21 | 4          | 7          | 12         | 4          | 7          | 12         | A8-B6       | CM                | The 12 sounds slightly sharp here |
| 22 |            |            |            | 4          | 7          | 12         | B7          | CM                |                                   |
| 23 | 4          | 7          | 11         | 4          | 7          | 11         | B8-C6       | CM7               |                                   |
| 24 |            |            |            | 4          | 7          | 11         | C7          | CM7               | The 11 sounds slightly sharp here |
| 25 | 5          | 7          | 12         | 5          | 7          | 12         | C8-D6       | Csus4             |                                   |
| 26 |            |            |            | 3          | 7          | 12         | D7          | Cm                | Not documented in source code     |
| 27 | 4          | 7          | 12         | 0+         | 7          | 12         | D8-E6       | C5 or Csus        | Microtonal (chorus effect)        |
| 28 |            |            |            | 0+         | 9          | 12         | E7          | Am/C              | Microtonal (chorus effect), Not documented in source code        |
| 29 | 4          |12 + 4(3.1c)| 12         | 0+         | 12+        | 12         | E8          | Octave            | Microtonal (chorus effect)        |

[Mutable Instruments Braids]: https://mutable-instruments.net/modules/braids/
