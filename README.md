Multi-speaker Setswana TTS corpus
=================================

This is a brief description of the multi-speaker Setswana
text-to-speech (TTS) corpus. The aim of this corpus was to investigate
the implementation of a TTS system using multiple voices recorded
using a low-cost process (i.e. using non-professional volunteers and
informal recording environments).

The Setswana corpus was recorded in Potchefstroom, South Africa using
volunteers from the campus of the North-West University in the first
quarter of 2016.

A brief description focussing on aspects relevant for application of
the corpus follows. For more information on the development process
also see the following paper:

D.R. van Niekerk, C. van Heerden, M. Davel, N. Kleynhans,
O. Kjartansson, M. Jansche, L. Ha, "Rapid development of TTS corpora
for four South African languages," in Proceedings of the 18th Annual
Conference of the International Speech Communication Association
(Interspeech), pp. 2178-2182, Stockholm, Sweden, August 2017.

Furthermore,

 - The original release is available at: http://www.openslr.org/32/
 - This version can be found on http://www.demitasse.co.za/~demitasse/
 - The most up-to-date version of the text components (transcriptions
   and dictionaries) are available at: https://github.com/NWU-MuST

--------------------------------------------------------------------------------

## 1. Basic format and technical notes

This package should contain this file `README.md` and the following
subdirectories:
  - `dictionaries`
  - `recordings`
  - `transcriptions`


### 1.1 Dictionaries

This contains the phone sets and dictionaries covering the
pronunciation of all tokens in the normalised transcriptions.

  - `*.phoneset.p2p` contain the complete set of phones used in
    International Phonetic Alphabet (IPA) [1] and X-SAMPA [2].
  - `*.regular.dict` contain the standard pronunciations that are
    suitable for grapheme-to-phoneme rule extraction.
  - `*.irregular.dict` contain the standard pronunciations that do not
    follow the spelling rules of the language (may not be suitable for
    G2P extraction).
  - `*.addendum.dict` contain entries for speaker-specific and other
    deviations from standard pronunciations found in the corpus.

For more information on the protocol followed during development refer
to Section 5 and the accompanying technical report.


### 1.2 Recordings

These are the recordings in [FLAC format](https://xiph.org/flac/),
16-bit per sample at 48kHz sampling rate with basenames corresponding
to utterance entries in the transcriptions files.

No post-processing or audio editing has been done after recording, it
may thus be advisable to apply gain normalisation and some form of
dereverberation filtering before further processing. Recordings also
have variable lengths of silence (which may contain ambient noises) at
the start and end of each utterance.


### 1.3 Transcriptions

Two versions of the orthographic transcriptions are provided. The
first version (`utts.data.orig`) is in the original form as at the
time of recording. The normalised and reviewed forms corresponding to
the provided dictionaries are in `utts.data.norm`.

Text files are in UTF-8 encoded Unicode (NFC).

--------------------------------------------------------------------------------

## 2. Text resources

The corpus contains Setswana and English sentences, developed as
follows:

Setswana sentences were sourced from online stories available by
permission under the Creative Commons licence from three sources
(Nal'ibali [3], African Storybook [4] and sentences translated from
Wikipedia) and processed as follows:

  1. Full sentences were extracted and divided into subsets according
     to length (number of words).
  2. Sentences in each length subset were selected for phonetic
     coverage (diphone units), selecting more shorter sentences than
     longer.

Additional sentences were generated and added to represent the
following domains and types: navigation, weather, questions, sport and
numbers. Proper names originating from different languages were
included to provide cases of foreign or code-switched tokens.

English sentences were sourced from the CMU Arctic TTS corpora [5, 6],
of which all "set A" sentences were used.

After the recording and initial quality control (QC) process a subset
of usable utterances were obtained. Specifically, some utterances were
discarded due to the presence of buffer-underrun artifacts that were
not detected during the recording process.

--------------------------------------------------------------------------------

## 3. Speakers and corpus stratification

Each speaker read a subset of sentences of each language. For Setswana
a small set of (overlap) sentences containing the rarest phones were
read by all speakers.

After discarding utterances with audio quality issues, the corpus
consists of the following (duration excludes non-speech/silence):

|         | Utterances |         | Duration (seconds) |         |
|--------:|-----------:|--------:|-------------------:|--------:|
| Speaker |   Setswana | English |           Setswana | English |
|      01 |        302 |     139 |              16.74 |    6.41 |
|      02 |        304 |     143 |              16.64 |    6.21 |
|      03 |        303 |     144 |              16.33 |    6.00 |
|      04 |        312 |     153 |              18.23 |    6.50 |
|      05 |        297 |     145 |              15.77 |    6.14 |
|   Total |       1518 |     724 |              83.73 |   31.28 |


--------------------------------------------------------------------------------

## 4. Orthographic transcriptions and quality checking

The following describes the basic process followed after recording:

  1. Manual _text normalisation_ (expanding numbers, dates and mark-up
     of foreign and "special" words)
  2. Semi-automatic _verification of transcriptions and dictionaries_
     by manually reviewing words flagged by automatic techniques as
     potential inaccuracies [7].

These are described in the following subsections.


### 4.1 Text normalisation and mark-up

  * Numbers are expanded using `-` between words to preserve original
    tokens. Tokens should be split on `-` before determining
    pronunciations using the accompanying pronunciation dictionaries.
  * Capitalisation and punctuation is kept (though simplified in some
    cases). No attempt has been made to mark intonation
    phrases/breathgroups.
  * The presence of `_` in a token indicates a word which a "special"
    pronunciation, this includes:
	 - Pronunciation of letters (usually starting with `char_`)
	 - Alternative pronunciations per speaker/utterances (usually
           ending in digits, e.g. `_0`)
	 - Alternative pronunciations per accent (usually ending in
       letters, e.g. `_a`)
  * Tokens preceded by the _pipe symbol_ (`|`) are foreign words,
    i.e. words requiring a non-native phoneset. In this corpus all
    foreign words are assumed to be English (using the English phone
    set). Words were marked in this way purely on phonetic grounds,
    possible prosodic units were not considered.

Marking of foreign words was done on phonetic grounds only, i.e. no
attempt was made to mark words consistently with prosodic or syntactic
structures (e.g. proper noun phrases).


### 4.2 Transcription and pronunciation verification

As a final step, the transcriptions have been manually checked for
basic errors and an attempt has been made to specify the
pronunciations of tokens more accurately in certain contexts. However,
because this was a manual verification process, no gaurantees are made
regarding consistency or exhaustiveness. Potential corpus users should
verify the set of words marked in this way (identifiable by the
presence of an underscore `_`), especially when different
pronunciation resources are used.

Manual verification was done as follows:

  1. Transcriptions were reviewed by comparing expected durations of
     words with automatic phone alignments [7] and gross
     transcription and pronunciation deviations marked.
  2. Pronunciations of capitalised words were reviewed by comparing
     the mel-cepstral distance [7].
  3. Some tokens with possibly different orthographic (Lesotho)
     conventions were reviewed and marked (e.g. tokens containing the
     _kh_ grapheme sequence).

With the exception of these cases, all pronunciations were handled
systematically to be phonemically consistent as described in the next
section.

--------------------------------------------------------------------------------

## 5. Phone set and pronunciation dictionaries

The phone set and G2P rules used to develop the corpus is based on the
NCHLT project [8, 9]. The phoneset used here deviates from the
original NCHLT set by merging some phones into affricates and
diphthongs to simplify syllable specification (see
`dictionaries/phoneset.p2p`).

All dictionary entries aim to be consistent in the following ways:

  - Except for speaker-specific and other special entries in the
    pronunciation _addenda_ pronunciations follow the conventions used
    during the NCHLT project.
  - Words of foreign origin are transcribed as close to as possible to
    their original language pronunciations (in terms of both syllable
    and phones).

As described in Section 4.2, pronunciations of certain subsets of
tokens were reviewed in more detail and the resulting entries are
found in the pronunciation _addenda_. The rationale for reviewing
these subsets are:

  - The corpus contains a significant number of proper names
    originating from different languages. Considering the difficulty
    in predicting pronunciations for proper names, these tokens were
    not phonetised and considered during text selection. The work of
    reviewing pronunciations against the actual recordings
    (phonetically) should thus not compromise the intended baseline
    phone distributions of the corpus.

The dictionaries released with this corpus are intended to provide an
experimental protocol and cover the tokens in the corpus. For actual
system development it may be advisable also to refer to the
dictionaries available at the NCHLT project site [9].

### 5.1 Further notes

  - The Setswana phone set does not include the phonemes /z/, /v/, /g/
    and /K/ associated with graphemes "z", "v", "g" and "hl" which may
    occur in loan words and names. In this corpus these phonemes were
    mapped to /s/, /f/, /k_>/ and /h l/ respectively which may have to
    be reviewed when using the corpus.

  - The Setswana orthography does not explicitly represent all the
    distinct vowels in the language's sound system. It is known that
    graphemes "o" and "e" each may represent more than one phoneme
    [11], this is not captured in the resources released here.

  - Setswana also makes tonal distinctions (high and low tones on
    syllables) which are not marked in the orthography. This is not
    captured in the resources released here.
    
--------------------------------------------------------------------------------

## 6. References

[1] https://en.wikipedia.org/wiki/International_Phonetic_Alphabet

[2] https://en.wikipedia.org/wiki/X-SAMPA

[3] http://nalibali.org/

[4] http://www.africanstorybook.org/

[5] http://festvox.org/cmu_arctic/

[6] J. Kominek and A.W. Black, "The CMU Arctic speech databases," in
    Proceedings of the 5th International Speech Communication
    Association Speech Synthesis Workshop, Pittsburgh, PA, USA, 2004,
    pp. 223-224.

[7] D.R. van Niekerk, "Experiments in rapid development of accurate
    phonetic alignments for TTS in Afrikaans," in Proceedings of the
    Twenty-Second Annual Symposium of the Pattern Recognition
    Association of South Africa, Vanderbijlpark, South Africa, 2011,
    pp. 144-149.

[8] E. Barnard, M.H. Davel, C.J. van Heerden, F. de Wet and
    J.A.C. Badenhorst, "The NCHLT speech corpus of the South African
    languages," in Proceedings of the Workshop on Spoken Language
    Technologies for Under-resourced languages (SLTU), St. Petersburg,
    Russia, 2014.

[9] M.H. Davel, W.D. Basson, C.J. van Heerden and E. Barnard, "NCHLT
    Dictionaries: Project Report," North-West University, Technical
    Report, 2013. [Online]. Available:
    https://sites.google.com/site/nchltspeechcorpus

[10] https://sites.google.com/site/nchltspeechcorpus

[11] https://en.wikipedia.org/wiki/Tswana_language
