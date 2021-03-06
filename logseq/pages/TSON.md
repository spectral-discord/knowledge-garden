- ***TSON*** (Tuning-Spectrum Object Notation) is a YAML-based file format for storing musical tuning and timbre/spectrum data (and eventually)
  collapsed:: true
	- ### Why another microtonal file/data standard?
		- [Valid question.](((629168a2-5251-438a-983c-1c1a993aeaeb)))
		- Existing formats have too many limitations for modern software and microtonal practices...
		  collapsed:: true
			- Some sacrifice portability and manipulability for readability (SCL, TUN), while others are environment-specific or unreadable (MTS)
			- Each comes some combination of limitations...
				- No reference frequencies
				- No pseudo-octaves/repetition ratios
				- No more than 12 notes per octave
				- Limits on how "detuned" a note can be
				- Not extensible
			- No standardizations or commonly used data structures exist for timbre/spectrum data or for pairing tunings and timbres
			- Most only allow notes to be defined in cents or just intonation ratios - reinforcing the dominance of 12-edo and harmonic timbres in music theory, research, and tech
		- TSON aims to address their shortcomings in a number of ways...
		  collapsed:: true
			- Readable without sacrificing portability and manipulability - YAML is readable and backwards-compatible with JSON... which is supported pretty much everywhere now
			- Compatible with existing tuning formats, yet extensible
			- Pitch ratios can be defined via either numbers (ints/floats) or expressions, preserving support for JI notation as well as cents, via `2^(cents / 1200)`
			- Unrecognized parameters won't break TSON interpretation, they'll just be ignored if not implemented
			- Able to contain timbre/spectrum data, multiple tunings and timbres per file, plus tuning-timbre pairings and sets
			- *Planned*: Instrument data (e.g. key layouts) and further timbre data structures (dynamic/reactive timbres, waveforms, and more)
		- Also, TSON is intended to be a focal point for an set of useful microtonal software...
		  collapsed:: true
			- *Coming Soon!*: [[TSONify]] - open-source packages/libraries for multiple languages with useful features for working with TSON data (and hopefully aiding its adoption)
			  collapsed:: true
				- Conversion between TSON and existing microtonal formats
				- TSON data validation
				- Support for the use of variables in expressions for dynamic tunings, timbres, and instrument models
				- Multi-file aggregation and linking for timbre/tuning pairings and sequences
				- Integration with TonalHub for fetching and updating data hosted in TonalHub instances
				- Tools for including TSON support in your own software
				- And more...
			- *Coming Soon!*: [[TonalHub]] - open-source, self-hostable web app for archiving and working with tuning, timbre, and instrument models
			  collapsed:: true
				- API and UI for archiving, fetching, and manipulating TSON data
				- TSON data model versioning
				- Tools for analyzing and developing tunings and timbres
				- And more...
- *Heads up:* TSON uses a number of terms that you might be unfamiliar with, or may have used differently in other contexts. Check out the [glossary]([[TSON Glossary]]) to see how they're used here!
  {{embed ((62916397-1eda-47e4-9440-e3eb32e673d6))}}
  {{embed ((62916399-7ae9-4f8c-b779-5d680caed091))}}
- ## Specification
  id:: 628ef99f-5c01-4dc6-a801-7a0b7cfe6607
  collapsed:: true
  
  {{embed ((3ac6d6f3-0cb8-4b0e-95b2-869c6cf69d12)) }}
	- ## Tuning Systems
	  id:: 62911960-76e1-4cb8-81a7-ee92fc8019b8
	  collapsed:: true
	  {{embed ((13fe4f0a-b40a-4b39-aad0-392b0e75d2e1))}}
	  | Key | Type | Examples |
	  |-|-|-|
	  | name | String | `Slendro`, `5-limit`, `My Tuning` |
	  | description | String | `A description might be nice to add` |
	  | scales | Array <Object> | See the [scales specification](((629122d9-4089-4ca0-80af-bf8540b22d82))) |
		- ## Scales
		  id:: 629122d9-4089-4ca0-80af-bf8540b22d82
		  {{embed ((6296869a-0c5b-487b-af9c-dfca96eacf1d))}} 
		  
		  The only required parameters are `notes` and `reference frequency`, but the rest may be useful depending on how you want your tuning to work.
		  
		  A [reference frequency](((62919254-679c-4edd-aacc-105fc45c85b2))) is required because the scale's notes are defined as ratios relative to a [root](((62919617-9d52-416c-be4f-c72edbbbda0f))). The reference frequency is used to generate real frequency values for each of the notes. See the ((9ca5419f-19dc-4ba9-a131-4b3891639697)) section for more info and examples!
		  | Key | Alternatives | Type | Examples |
		  |-|-|-|-|
		  | [reference frequency](((62919254-679c-4edd-aacc-105fc45c85b2))) | reference | String, Number | `440 hz`, `200.0` |
		  | [reference note](((62919243-8c47-4050-b49c-ca654d73e36b))) | | String | `ref`, `-0`, `The Root`, `Z#` |
		  | [repeat ratio](((6291924c-5500-456e-9cca-6a138f6e16c6))) | repeat | Number | `2`, `2.1`, `3.0` |
		  | max frequency | max | String, Number | `666 hz`, `20000.0` |
		  | min frequency | min | String, Number | `666 hz`, `20.0` |
		  | notes | | Array<[Expression](((629146bc-6e1e-4a00-b2a0-5c205cfb23c6))), Object> | See the [notes specification](((62918617-11a6-4911-abd6-d068605aaa73))) |
		  {{embed ((4899ac1f-4ff7-4a70-815f-19fcac761588))}}
		-
		- ## Notes
		  id:: 62918617-11a6-4911-abd6-d068605aaa73
		  {{embed ((6291c175-343a-4c3b-9fc7-f20c479ddbef))}} 
		  | Key | Alternatives | Type | Examples |
		  |-|-|-|-|
		  | [frequency ratio](((62918b58-f893-48c9-b530-4102f7f3c173))) | ratio | [Expression](((629146bc-6e1e-4a00-b2a0-5c205cfb23c6))) | `1.557`, `3^(1.3/13)` |
		  | name | | String | `A#`, `Dax`, `7` |
		  {{embed ((fe32a44a-6de1-4888-8d38-f33ba4a3187f))}}
	- ## Spectra
	  id:: 6291b083-cb55-4961-8a93-e977afd6dc98
	- ## Sets
	  id:: 6291b0c2-024a-45e7-86dc-4d149993c94e
	- ### Example TSONs
	  collapsed:: true
		- ```yaml
		  Tuning Systems
		    - name: 12edo
		      scales
		        - reference frequency: 440 hz
		          repeat ratio: 2.0
		          notes
		            - frequency ratio: 1
		              name: A
		            - ratio: 2^(1/12)
		              name: [ A#, Bb ]
		            # etc...
		    - name: JI - BP-edo
		      scales
		        - reference: 440
		          repeat: 2
		          max frequency: 880 hz
		          notes
		            - ratio: 3/2
		            	name: ref
		            - [ 4/3, 5/3 ]
		            # etc...
		        - reference: 880
		          repeat: 3
		          min: 880
		          notes
		            - 3^(1/13)
		            # etc...
		  
		  Spectra
		    - name: harmonic
		      overtones
		        - frequency ratio: 1
		          amplitude weight: 1
		        - ratio: 2
		          weight: 1/2
		        # etc...
		      # TBD
		      # - noise profile
		  
		  Instruments
		    # TBD
		    
		  Sets
		    # TBD
		  ```
- ## Understanding and Using TSON
  id:: 6291b7d7-25fc-4c5b-9a69-31565e1b89d8
	- TSON is designed to hold [Tuning Systems](((62911960-76e1-4cb8-81a7-ee92fc8019b8))), [Spectra](((6291b083-cb55-4961-8a93-e977afd6dc98))), and [Sets](((6291b0c2-024a-45e7-86dc-4d149993c94e)))
	  id:: 3ac6d6f3-0cb8-4b0e-95b2-869c6cf69d12
	  
	  At the top level, TSON is just arrays of each.
	- ### Understanding Tuning Systems and Scales
	  id:: 9ca5419f-19dc-4ba9-a131-4b3891639697
	  collapsed:: true
		- In TSON, tuning systems are made of [scales](((629122d9-4089-4ca0-80af-bf8540b22d82))), and scales are made of [notes](((62918617-11a6-4911-abd6-d068605aaa73))).
		  id:: 13fe4f0a-b40a-4b39-aad0-392b0e75d2e1
		- Scales are functional and generative in the sense that notes are defined in relation to a [root](((62919617-9d52-416c-be4f-c72edbbbda0f))), and a [reference frequency](((62919254-679c-4edd-aacc-105fc45c85b2))) is used to generate real frequency values for all of the notes.
			- *Example:*
			  ```yaml
			  Tuning System
			    - scales
			      - reference frequency: 100 hz
			        notes
			          - 1			# 100 hz
			          - 1.3		# 130 hz
			          - 1.5		# 150 hz
			          - 1.75		# 175 hz
			  ```
		- If using multiple scales in a tuning system, the scales can overlap so that their notes are interlaced.
			- *Example:*
			  ```yaml
			  Tuning System
			    - scales
			      - reference frequency: 100 hz
			        notes
			          - 1			# 100 hz
			          - 1.5		# 150 hz
			          - 1.75		# 175 hz
			  
			      - reference frequency: 80 hz
			        notes
			          - 1 		# 80 hz
			          - 1.5		# 120 hz
			          - 2			# 160 hz
			          - 2.5		# 200 hz
			  ```
	- ### Understanding Scale Parameters
	  collapsed:: true
		- Scales can be made to repeat at a given ratio to the [root](((62919617-9d52-416c-be4f-c72edbbbda0f))) - the [repeat ratio](((6291924c-5500-456e-9cca-6a138f6e16c6))) then becomes the new root. This happens in both directions along the frequency spectrum - both increasing and decreasing in pitch.
			- *Example:*
			  ```yaml
			  Tuning System
			    - scales
			      - reference frequency: 100 hz
			        repeat ratio: 2
			        notes
			          - 1			# ... 50 hz, 100 hz, 200 hz, 400 hz ...
			          - 1.5		# ... 75 hz, 150 hz, 300 hz, 600 hz ...
			          - 1.75		# ... 87.5 hz, 175 hz, 350 hz, 700 hz ...
			  ```
		- By providing [minimum](((6291b4a8-b6bc-43c8-91f1-2e21878b771c))) and [maximum](((6291bc28-1b8c-4517-b0b8-d8a6d001ce91))) frequencies for a scale, you can limit the frequency range that notes will be generated for. This way, you can prevent overlapping scales.
			- *Example:*
			  ```yaml
			  Tuning System
			    - scales
			      - reference: 100 hz
			        min: 300 hz
			        repeat: 2.0
			        notes
			          - 1.0		# 400 hz, 800 hz, 1600 hz, 3200 hz ...
			          - 1.5		# 300 hz, 600 hz, 1200 hz, 2400 hz ...
			          - 1.75		# 350 hz, 700 hz, 1400 hz, 2800 hz ...
			      - reference: 80
			        max: 300
			        repeat: 2.5
			        notes
			          - 1			# ... 32 hz, 80 hz, 200 hz
			          - 1.5		# ... 48 hz, 120 hz, 300 hz
			          - 2			# ... 64 hz, 160 hz
			  ```
		- If a repeat ratio is provided but min/max values are not, the scale could be repeated to cover any frequency range (whether toward $$\infty$$, the infinite regression of the asymptote at $$0$$, or both).
		- If a [reference note](((62919243-8c47-4050-b49c-ca654d73e36b))) is not provided, then the reference frequency will be set to the scale's root (ie, ratio `1.0`) which note [frequency ratios](((62918b58-f893-48c9-b530-4102f7f3c173))) are based on.
		  id:: 4899ac1f-4ff7-4a70-815f-19fcac761588
			- *Warning:* If a note with a frequency ratio of `1` is not defined, then a note will not exist there, nor at repeat intervals. If a reference note isn't defined either, then the scale's notes will be centered around a root and reference pitch that doesn't exist as a note.
			  
			  This may be desirable for some tunings, but many tunings will need a note with a frequency ratio of  `1`.
	- ### Understanding Notes
	  collapsed:: true
		- The only requirement for a note is a [frequency ratio](((62918b58-f893-48c9-b530-4102f7f3c173))), which can be defined using either a number (integer or float) or a valid [expression](((629146bc-6e1e-4a00-b2a0-5c205cfb23c6))) that resolves to a real number greater than zero.
		  id:: 6291c175-343a-4c3b-9fc7-f20c479ddbef
		- While note names are optional, they're required to be used as a scale's [reference note](((62919243-8c47-4050-b49c-ca654d73e36b))), and possibly for some [[TSONify]] functionalities as well.
		  id:: fe32a44a-6de1-4888-8d38-f33ba4a3187f
		  
		  If some or all of a scale's notes don't need a note name, you can just use an array of number and expression strings - you can even use bracket notation arrays as entries in the notes array!
		  *Example:*
		  ```yaml
		  # The two scales below are the same
		  #
		  # This is a valid, if minimal, TSON file
		  
		  Tuning Systems
		    - scales
		        - notes: [ 1, 1.5^(1/4), 1.5^(2/4), 1.5^(3/4) ]
		          reference frequency: 100
		        - notes
		            - ratio: 1.5^(1/4)
		              name: B
		            - 1.5^(3/4)
		            - [ 1, 1.5^(2/4) ]
		          reference frequency: 100
		  ```
- ## Include TSON Support in Your Own Software
  collapsed:: true
	- Coming Soon (once [specifications](((628ef99f-5c01-4dc6-a801-7a0b7cfe6607))) and [[TSONify]] are further developed)
- ## Get Involved
  collapsed:: true
  id:: 628ef99f-655c-4c4d-a9de-a3455a919704
	- **Is TSON missing something?** Do you have an idea that could make TSON more useful, interoperable, or accessible? Please leave a [github issue](https://github.com/spectral-discord/TSON/issues)!
	-
	- **Community!** I'd love for collaborators and contributors for TSON and Spectral Discord. The ideal would be for this to be a community-led project.
		- I'll be setting up a chat server soon... I'd prefer something open-source/secure like [Matrix](https://matrix.org/) or [Cwtch](https://cwtch.im/), but might succumb to Discord for accessibility.
	-
	- **Translating!** I'd like to get this Knowledge Garden translated as it becomes more stable. If you'd like to help translate it to any language, get it touch!
	-