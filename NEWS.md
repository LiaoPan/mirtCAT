# mirtCAT 1.2

- `progress` logical added to `mirtCAT()` to print the progress of Monte Carlo simulations
  with the `pbapply` package

- Shadow testing and optimal test assembly designs supported by adding `constr_fun` input to 
  `mirtCAT()` and `objective` input to `findNextItem()`. See the `findNextItem()` documentation
  for details and examples

- `computeCriteria()` function added to return all the criteria values (e.g.,
  maximum information) associated with each respective item

- population-level Theta terms tracked internally for Monte Carlo simulations because
  `generate_pattern()` now stores the respective population values as a silent attribute. 
  Will now be displayed in summary/print/plot outputs, where applicable

- allow the internal `design` object to be modified through the `customNextItem()` function 

- added an `extract.mirtCAT()` function to better document and extract the components
  of the `person`, `design`, and `test` objects in `customNextItem()`. Allows for safer 
  and easier customization of item selection maps

- new `test_properties` and `person_properties` inputs to `design` element to allow for 
  prior information about the test/persons (e.g., selecting particular items based on 
  prior demographic information). Intended for use with a `customNextItem()` 
  function definition

# mirtCAT 1.1

- added `StemExpression` to `df` input to support arbitrary R expressions for stems to 
  be rendered with standard R code. Allows for inputs such as audio, video, etc, 
  as well through the use of a suitable `tags$FUN(...)`

- new `password` input to `shinyGUI` list to allow login and password gates. Useful when hosting 
  CAT on a server with potentially sensitive items

- default `shiny` stem wrapper function for `df` when it is a `data.frame` is now exposed via the 
  `stem_default_format` input to `shinyGUI`

- MathJax is now explicitly supported in the item stems and response options. 
  As before, users can provide a manual list explicilty defining the `shiny` functions; 
  jowever, if a `data.frame` object is used then the stems/responses
  will be automatically wrapped within a suitable `shiny::withMathJax()` function to render the output

- mental preparation screen now disabled for non-scored tests when 
  the `mo` object is ommited (i.e., equivalent to setting 
  `shinyGUI = list(begin_message = "")`)

- `'select'` Type input to `df` now uses a blank option as the default to avoid 
  clicking through accidently. Also works better with the `forced_choice` default

# mirtCAT 1.0

- released for JSS publication

# mirtCAT 0.9

- fix MLWI/MPWI selection criteria

- `findNextItem()` is allowed to return all items given the selection criteria

# Changes in mirtCAT 0.8

- include `constraints` option for `excluded` items (useful for re-testing situations where 
  item selection is from the same bank of items but previously answered items should not appear)

- new `'none'` presentation Type to allow empty material with no responses (mainly for presenting 
  reading passages or other testlet-based items). Useful when used in conjunction with the 
  `constraints` input from the `design` list so that these items have predictible dependent 
  pairings (or can be used with the `customNextItem` form as well for explicit dependencies)

- `shinyGUI` input gained a `ui` element to allow users to completely customize the graphical UI 
  with shiny code

- added `customNextItem` function to allow a completely customized method for declaring the 
  item selection scheme

- support `checkbox` input type for `checkboxGroupInput()` function. Supplying one or more 
  answers will score the items in a partial credit style

- include missing input options in `df` input for `shiny` (e.g., width, placeholder, inline). 
  Removed `'radio_inline'` input because this can now be acomplishied by passing 
  `Type = 'radio'` and `inline = TRUE`

# Changes in mirtCAT 0.6

- added `getPerson()` function to assign a person object following the use of `createShinyGUI`

- the `raw_responses` vector returned for each participant is now a character vector instead of an 
  integer

- added `slider` Type input for `sliderInput` rating scale questions

- `resume_file` removed, now if an associated `temp_file` is detected it will be used to resume
  the GUI session

- new `begin_message` input to `shinyGUI` to change message prior to starting the CAT

- changed `lastpage` element in `shinyGUI` input from a list to a function to allow messages 
  containing information pertaining to the session

# Changes in mirtCAT 0.5

- fix bug when using SH exposure control when the pool runs out of items

- add `delta_thetas` argument to design list to stop CAT if change between latent trait updates
  is less than this distance criteria

- include more functions to allow easier web hosting in locations such as `shinyapps.io`. Namely,
  `mirtCAT_preamble()` and `createShinyGUI()`

- graphical images (png, gif, and jpeg) no logner supported. Stems preferably should in HTML 
  for best results and control

- Stem paths can now point to and render HTML and markdown files in the GUI

- `df` input can now be a list for including more fine tuned shiny inputs

- check for the existance of graphical item stems, and allow relative or absolute paths

## BUGFIX

- fix stem location bug, and add better aspect ratio

- the `summary(mod, sort=FALSE)` argument returned a NULL object instead of the unsorted response.
  This has been patched and is now tested for
  
- when no `df` is supplied, check that the responses are in a plausible range 
  (reported by Gerard Flens)

# Changes in mirtCAT 0.4.2

- `forced_choice` argument for shinyGUI input to state whether respones for each item are 
  required (for CATs, this should always be TRUE)

- respones in GUI now are blank by default

- in `preCAT` list input change `nitems` to `min_items` and `max_items` for better control. Also 
  include a `response_variance` logical to terminate the preCAT stage when variability in the 
  the response options occurs (so that ML estimation becomes plausible)

- include Sympson-Hetter method of item exposure control

- major re-write of shiny inputs. Now the questions, answers, and options are all supplied through
  a `data.frame` object for better clarity, and all shiny inputs regarding the questions, image 
  locations, etc, are specified in this object
  
- `mirt_object` input renamed to `mo` for short

- the `local_pattern` input now accepts a matrix of response patterns for running simulation 
  designs. Returns a list of person objects instead of a single object
  
- `generate_pattern()` now supports multiple Theta inputs specifically for simulation designs

- `start_item` input now accepts character value inputs (in addition to explicit numeric inputs)
  corresponding to the `criteria` argument. This allows the first item to be selected using the 
  (adaptive) selection criteria

- added `generate.mirt_object()` function to build the required `mirt_object` input given
  population parameters
  
- new `cl` argument in `mirtCAT()` for passing a parallel cluster object defined from the 
  parallel package. Used to run simulation designs with parallel architecture for better speed
  
- by default, the demographics page is no longer generated in the GUI  

# Changes in mirtCAT 0.3

- `item_answers` can now be a list input, indicating that more than one correct answer is
  possible for a given item

- allow the first page and demographics page to be skipped by passing empty list arguments 

- added 'fixed' method to keep latent trait estimates at fixed values (useful for preCAT)

- Fisher information matrix added for remaining multidimensional models supported by `mirt`,
  including custom item types

- add 'Arule' and 'APrule' for minimum trace criteria of asymtotic covariance matrix

# Changes in mirtCAT 0.2

- temporary files can now be saved while the GUI is running, and restored at a later time

- more estimation options can be passed to `fscores()` via the ... argument

- sensitive objects are now removed from the package namespace when the `mirtCAT()` finishes 
  unsuccessfully 

- categories are always returned with based 1 for first response in the GUI

- add content balancing option

- various bug fixes, and update documentation

- new `findNextItem()` input for users to locate the next item to administer (likely for custom
  CAT interfaces that do not use the Shiny package). Can be updated with the `updateDesign()` 
  function
  
- moved 'Next' button in the web interface to the left panel box so that it will always remain in 
  the same location
  
- support CSS customization

- switch multidimensional selection criteria to use analytical expressions rather than numerical.
  Several multivariate Fisher information matrix computation currently not supported analytically,
  but will be steadily added.
  
- add classification capabilities to `design` list input
