CSS/Sass Style Guide
====================

After having been changing code layout, naming convention and file structure of my CSS/Sass code base from project to project over and over again I finally decided to give the whole thing a deeper thought and document my current idea of what’s useful and fits my personal needs. A lot is adopted from or heavily inspired by techniques and approaches already broadly used in the industry. You’ll find some sources credited at the bottom of this file.

### Premises
* All code should be readable and as meaningful as possible.
* Create reusable blocks, patterns and modules. Avoid redundancies.
* Always have maintainability and expandability in mind.
* No assumptions about the actual presenation should be made in class names (e.g. col_8).
* Build responsive styles, enhance progressively when features are available. Provide fallbacks if possible.
* Content first.

### Tools
* Styles are written in [Sass](http://www.sass-lang.com).
* [Compass](http://compass-style.org/) for compiling to CSS.
* [Susy](http://susy.oddbird.net) for grid systems in Sass.
* [Grunt.js](http://gruntjs.com/) for task automatisation.
* [Autoprefixer](https://github.com/ai/autoprefixer) takes care vendor prefixes.
* [Grunticon](https://github.com/filamentgroup/grunticon) helps managing icons and background images for all devices.

### File Structure
sass/ 
| 
|– base/ 
|   |– _reset.scss       # Set/reset basic element styling
|   |– _typography.scss  # Fonts, basic typography 
| 
|– components/ 
|   |– _navigation.scss  # Navigation 
|   |– _user.scss        # User
|   |– _icons.scss       # Icons 
|   ...                  # Etc… 
| 
|– helpers/ 
|   |– _vars.scss        # General Sass vars, grid values, etc.
|   |– _functions.scss   # Sass functions 
|   |– _helpers.scss     # Placeholders, etc.
|   |– _mixins.scss      # Sass mixins
|   |– _setup.scss       # Setup steps (e.g. Susy grid setup)
| 
|– layout/               
|   |– _header.scss      # Header 
|   |– _footer.scss      # Footer 
|   |– _forms.scss       # Forms 
|   ...                  # Etc… 
| 
|– pages/
|   |– _home.scss        # Home specific styles 
|   |– _contact.scss     # Contact specific styles 
|   ...                  # Etc… 
| 
|– vendors/ 
|   |– _jquery-ui.scss   # jQuery UI 
|   ...                  # Etc… 
| 
|– styles.scss           # primary Sass file
|– ie-fixes.scss         # IE fixes if necessary
|
css/
|
|– styles.min.css        # compiled, autoprefixed css file
|– styles.min.map        # source map for debugging
|– ie-fixes.min.css
|– ie-fixes.min.map

### Basic Variables

### Colors

### Layout Settings

### Important Functions

### Naming Conventions

### Comments

### Declaration

### Nesting

### General Coding Style
* Root font size is set to 100%, block/module font sizes are set in rem relative to root font size, within font sizes are set in em.
* Avoid shorthand notation if possible. E.g. use margin-bottom: 1em; instead of margin: 0 0 1em 0;
* If number values aren’t self-explanatory, lift the secret. Add a comment.

### Breakpoints
For dealing with breakpoints and switching between layout settings, there is the use-layout($breakpoint) mixin taking care of it all.

### Credits
Some sources of insight, influence and inspiration that lead me here:
* [BEM Methodology](http://bem.info/method/)
* [MindBEMding – Getting Your Head Round BEM Syntax](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/)
* [OOCSS](https://github.com/stubbornella/oocss/wiki)
* [SUIT](https://github.com/suitcss/suit/tree/master/doc)
* [SmaCSS](https://smacss.com/)
* [Hugo Giraudel’s “Architecture for Sass Projects”](http://www.sitepoint.com/architecture-Sass-project/)
* [Martin Wolf’s Style Guide](https://raw.githubusercontent.com/martinwolf/CSS-Styleguide/)
* [CSS-Tricks “Font Size Idea: px at the Root, rem for Components, em for Text Elements](http://css-tricks.com/rems-ems/)