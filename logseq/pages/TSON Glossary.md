- Expression
  id:: 629146bc-6e1e-4a00-b2a0-5c205cfb23c6
	- **Expressions** are mathematical expressions, which can be used to define various parameters in TSON as an alternative to a real number.
	- They use a simple syntax that you're probably familiar with, but only allow for so much mathematical complexity. Whitespace is ignored.
	- *Syntax*
	  collapsed:: true
		- Operators
		  collapsed:: true
			- Arithmetic: `+`, `-`, `*`, `/`
			- Exponents: `^`
				- *Example:*
				  ```yaml
				  
				  ```
			- Modulo: `%`
				- *Example:*
				  ```yaml
				  
				  ```
			- Parentheses: `( )`
			- Absolute value: `| |`
				- *Example:*
				  ```yaml
				  
				  ```
		- Constants
		  collapsed:: true
			- Pi: `pi`
			- Euler's number: `e`
		- Variables
		  collapsed:: true
			- *Coming Soon!*
	- *Examples*
	  collapsed:: true
		- ***TODO***
- Frequency Ratio
  id:: 62918b58-f893-48c9-b530-4102f7f3c173
	- A **frequency ratio** defines a pitch's distance from a given reference or root frequency.
	- Frequency ratios are used when defining [scales](((6291ba45-59c1-4071-96b1-5d56a5a0f999))) and partial distributions because humans perceive pitch as scaling approximately logarithmically.
	- Ratios allow the real frequency distance (i.e. measured in Hertz) to grow or shrink depending on the  frequency of the root that the ratios depend on.
	- *Example*
	  collapsed:: true
		- Although the notes in the two scales below have the same frequency ratios, the change in the [reference frequency](((62919254-679c-4edd-aacc-105fc45c85b2))) results in different frequencies being mapped onto the notes.
		  ```yaml
		  Tuning System
		    - scales
		      - reference frequency: 100 hz
		        notes
		          - 1			# 100 hz
		          - 1.3		# 130 hz
		          - 1.5		# 150 hz
		          - 1.75		# 175 hz
		      - reference frequency: 500 hz
		        notes
		          - 1			# 500 hz
		          - 1.3		# 650 hz
		          - 1.5		# 750 hz
		          - 1.75		# 875 hz
		  ```
- Max Frequency
  id:: 6291bc28-1b8c-4517-b0b8-d8a6d001ce91
	- If a **max frequency** is defined for a scale, then no notes will be generated above that frequency.
	- This, along with [min frequency](((6296c474-695c-450e-9ecb-d0c2fac4ad30))), allows you to define frequency ranges in which scales can exist.
	- This is particularly useful for multi-scale tuning systems in which you may want different scales to occupy different frequency ranges.
- Min Frequency
  id:: 6296c474-695c-450e-9ecb-d0c2fac4ad30
	- If a **min frequency** is defined for a scale, then no notes will be generated below that frequency.
	- This, along with [max frequency](((6291bc28-1b8c-4517-b0b8-d8a6d001ce91))), allows you to define frequency ranges in which scales can exist.
	- This is particularly useful for multi-scale tuning systems in which you may want different scales to occupy different frequency ranges.
- Note
  id:: 6296c7f7-ddf0-47bc-823c-a717f49b2b63
	- **Notes** represent a scale's pitches.
- Partial Distribution
  id:: 629bee65-cf76-4a03-a0e9-4862024c7d4e
	-
- Reference Frequency
  id:: 62919254-679c-4edd-aacc-105fc45c85b2
	- The **reference frequency** is used to map a scale's notes - i.e., frequency ratios - onto real frequencies.
	- {{embed ((62967efd-95be-4b79-9923-4001e70ef4ff))}}
- Reference Note
  id:: 62919243-8c47-4050-b49c-ca654d73e36b
	- If a **reference note** is defined, then that note will be mapped onto the reference frequency, and all other notes will be mapped relative to the reference note.
	- *Example*
	  collapsed:: true
		- ```yaml
		  Tuning System
		    - scales
		      - reference frequency: 300 hz
		      - reference note: ref
		        notes
		          - 1				# 200 hz
		          - name: ref		# Name is defined so it can be used as a reference note
		            ratio: 1.5	# 300 hz
		          - 1.75			# 350 hz
		          - 2				# 400 hz
		  ```
- Repeat Ratio
  id:: 6291924c-5500-456e-9cca-6a138f6e16c6
	- If a **repeat ratio** is defined, the entire scale will repeat at this ratio.
	- When the scale repeats, the repeat ratio becomes the new root and all of the notes are generated in relation to this new root.
	- The scale also repeats the inverse of this ratio. This means that the scale repeats in both directions across the frequency spectrum.
	  collapsed:: true
		- *Example:* If the scale's repeat ratio is `2` and its root sits at `100 hz`, then the next highest scale iteration will have a root of `200 hz` and the next lowest iteration will have a root of `50 hz`. Then `400 hz` and `25 hz`, etc.
	- This process repeats until either no more notes need to be generated or the [min](((6296c474-695c-450e-9ecb-d0c2fac4ad30)))/[max](((6291bc28-1b8c-4517-b0b8-d8a6d001ce91))) frequencies have been reached.
	- This has often been referred to elsewhere as a ***pseudo-octave***. TSON uses the more generic **repeat ratio** that doesn't refer to specific tonal structures or concepts in western music theory (8 diatonic scale notes per octave, for instance).
- Root
  id:: 62919617-9d52-416c-be4f-c72edbbbda0f
	- In the context of both a scale's [notes](((6296c7f7-ddf0-47bc-823c-a717f49b2b63))) and a spectrum's [partial distributions](((629bee65-cf76-4a03-a0e9-4862024c7d4e))), the **root** refers a [frequency ratio](((62918b58-f893-48c9-b530-4102f7f3c173))) of `1.0`.
	- Thus, all frequency ratios - including the [repeat ratio](((6291924c-5500-456e-9cca-6a138f6e16c6))) - are defined in relation to the root.
	- The root doesn't have to coincide with a note - ie, a note with a frequency ratio of `1` must be defined if you want one to exist there.
- Scale
  id:: 6291ba45-59c1-4071-96b1-5d56a5a0f999
	- **Scales** are groups of [notes](((6296c7f7-ddf0-47bc-823c-a717f49b2b63))) and various parameters that can be used to generate all, or part of, a tuning.
	  id:: 6296869a-0c5b-487b-af9c-dfca96eacf1d
- Spectrum
	- A **Spectrum** (plural: **spectra**) contains information about an instrument sound
	- This is similar to the concept of *timbre*, which is a term that has been used for various purposes in psychoacoustics and music theory. Spectrum has also been used by [Sethares](((62ad1af1-aab8-4080-bf6c-32dfe11b7fb462a39c06-97d3-45d1-9837-a0b012346a75))) et al. in a way similar to its usage in TSON:
	  
	  {{embed ((62ad1b5e-ab92-4f3c-8b69-b37c3f7dc15e))}}
	- At the moment, TSON only supports [partial distributions](((629bee65-cf76-4a03-a0e9-4862024c7d4e))) for spectral components, but more options are planned!