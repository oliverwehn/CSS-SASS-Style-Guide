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
```
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
```

### Basic Variables
There are just a few Sass variables defined in sass/helpers/_vars.scss to store shared and often used values for layout, colors and stuff.

#### $layouts
The variable $layout contains a Sass map with a field for each breakpoint layout. The layout “default” contains all values for the base layout which can be “mobile first” or whatever you want it to be. 
In the fields of each other layout besides default, there are just the values defined you want to be overriden. When switching to another breakpoint, default and intended layout settings will be recursively merged.
The layout maps contain submaps (I call them “sets”) as a kind of namespaces to easily store and find config values for each layout. For example, “grid” contains the Susy config values for grid calculations. “query” stores values to generate the breakpoints media queries.
The values are easily accessed using the layout-get($layout, $set[, $key]) function covered in the “Functions” section.

```Sass
$layouts: (
  default: (
    grid: (
      …
    ),
    typography: (
      base-font-size: 14px,
      base-line-height: 20px,
      …
    )
    …
  ),
  xl: (
    query: (
      min-width: 1201px
    ),
    grid: (
      …
    ),
    typography: (
      base-font-size: 16px,
      base-line-height: 22px
    )
  …
  ),
  …
);
```
#### $colors
All colors are stored in the $colors variable. Like $layout it is a Sass map. Each color (or palette) is named and itself contains a map with a default value for “base” and as many variations as needed (like “dark” or “light”). Colors are easily accessible through the color-get($palette[, $variation]) function covered in the “Functions” section.

```Sass
$colors: (
  brand: (
    base: #004388,
    dark: #002852,
    light: #4993df
  ),
  text: (
    base: #858585,
    thin: #636363
  )
);
```

#### $base-font-size, etc.
I use some typography-related global vars to easily get to font-size and line-height values. Those are set at the beginning of compilation and overriden (and reset to default afterwards) within breakpoint @content (passed to with-layout($layout [only])) or @content passed to with-type-settings($font-size, [$line-height], [$set-style])).
$base-font-size is always the value defined in the current breakpoint layout, $local-font-size is the current font-size value at this point of the document as it was set by with-type-settings().

```Sass
$base-font-size: layout-get(default, typography, base-font-size);
$base-font-size: layout-get(default, typography, base-font-size);
$local-font-size: $base-font-size;
$local-line-height: $base-line-height;
```

### $susy
By passing the “grid” set of the default layout to this variable, we set up the base for grid calculations done by Susy.
```Sass
$susy: layout-get(default, grid);
```


### Layout Settings

### Important Functions

### Naming Conventions
Thanks to Sass 3.3 and above it is a pure pleasure to work with the BEM methodology in Sass. 
Two underscores separate block from element, double hyphen separate block or element from modifier.
```Sass
.nav {
  …
  &__item {
    …
    &--active {
      …
    }
  }
  &--fixed {
    …
  }
}
```
compiling to
```Css
.nav {
  …
}
.nav__item {
  …
}
.nav__item--active {
  …
}
.nav--fixed {
  …
}
```

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