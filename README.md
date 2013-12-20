# Installation

* Install [Ruby](https://www.ruby-lang.org/en/downloads/) version 1.9 or higher 
* Install bundler gem using ```gem install bundler```
* Install [nodejs](http://nodejs.org/download/) version 0.8 or higher with npm support
* Install following node modules globally ```npm install -g grunt-cli bower```
* Open a console & navigate to markup project directory (this directory) and issue following commands:
	* ``` bundle install ```
	* ``` npm install ```
	* ``` bower install ```

# General guidelines

* All rules should be class based to ensure maximum reusability
* All images related to styling must be set with css background property. No image tag is allowed for deign purposes. Also use images only when it is mandatory, use CSS3 whenever possible to generate background effect. Also use [compass-rgbapng](https://github.com/aaronrussell/compass-rgbapng) plugin to enable cross browser support for rgba() if you are using.   
* Use of variables & mixins are highly recommended to keep code minimal & configurable.
* Every colors & font sizes & fonts must be defined as variables and used thoroughly whenever needed.
* Use mixins, helpers & utilities provided by [compass](http://compass-style.org/reference/compass/) library whenever possible. Write your own mixins only if there isn't one available in compass. For example, instead of adding browser prefixes manually, use compass CSS3 mixins like border-radius etc. that will take care of adding browser prefixes in generated css files. Also hacks like clearfix should also be used from compass definition.
* Use compass's [sprite helper](http://compass-style.org/reference/compass/helpers/sprites/) to generate css sprites for icons and use the sprites while writing rules.
* If needed, use a grid framework like [susy](http://susy.oddbird.net/) or [singularitygs](https://github.com/Team-Sass/Singularity) instead of using a css based grid framework to avoid use of extra non-semantic classes in markup. This two frameworks will be installed with the ```bundle install``` command and to use the chosen one, just uncomment the respective line in config.rb
* Use ```grunt compass:dev``` to compile files manually and use ```grunt watch``` to ensure autocompile of scss files or ```bundle exec guard``` during markup development to ensure autocompile & live reload in browsers (have to install [livereload extension](http://feedback.livereload.com/knowledgebase/articles/86242-how-do-i-install-and-use-the-browser-extensions-) in browser)

# File structure

```
.
├── Gemfile                             // required ruby gems
├── Gruntfile.js                        // grunt configuration file
├── Guardfile                           // guard configuration file
├── README.md                           // README file in markdown format
├── README.html                         // README file in HTML format
├── bower.json                          // bower packages for js files
├── config.rb                           // compass project configuration
├── css                                 // output directory for compiled css files
├── html                                // developed markup files
│   ├── layouts                         // markup files for layouts
│   │   ├── branded                     // all branded layouts will go here in separate folders/client
│   │   │   └── client_name             // actual client name will replace this name
│   │   │       ├── desktop.html        // client branding applied in desktop layout
│   │   │       ├── mobile.html         // client branding applied in mobile layout
│   │   │       └── tablet.html         // client branding applied in tablet layout
│   │   ├── desktop.html                // generic layout for desktop
│   │   ├── mobile.html                 // generic layout for mobile
│   │   └── tablet.html                 // generic layout for tablet
│   ├── pages                           // all page markups will go here in separate folders
│   │   ├── home                        // home page markups
│   │   │   ├── desktop.html            // client branding applied in desktop home page
│   │   │   ├── mobile.html             // client branding applied in mobile home page
│   │   │   └── tablet.html             // client branding applied in tablet home page
│   └── widgets                         // markups for all widgets will go here in separate files
│   │   ├── branded                     // all branded widgets will go here in separate folders/client
│   │   │   └── client_name             // actual client name will replace this name
│   │   │       ├── leaderboard.html    // client branding applied in leaderboard.html
│       └── leaderboard.html            // generic leaderboard widget markup
├── images                              // image assets used in styling
│   ├── icons                           // each set of icons will have its own folder to be combined in sprite
│   ├── rgba                            // output folder for compass generated rgba png files
│   └── sprites                         // output folder for generated sprite files
├── js                                  // custom javascript files (if any)
│   ├── libs                            // third party libraries (installed via bower)
├── package.json                        // node module dependencies for grunt
└── sass                                // scss files will go here
    ├── branding                        // all client branding specific overrides will go here in separate folders
    │   └── client_name                 // actual client name will replace this name
    │       ├── desktop.scss            // branding overriding rules for desktop site
    │       ├── mobile.scss             // branding overriding rules for mobile site
    │       ├── tablet.scss             // branding overriding rules for tablet site
    │       └── widgets                 // branding overriding rules for widgets will go here in separate files
    │           └── leaderboard.scss    // branding overriding rules for leaderboard widget 
    ├── common                          // common sass rules usable across all devices
    │   ├── _base.scss                  // aggregation of all common rules, to be imported by device specific files
    │   ├── components                  // rules for common ui components will go here
    │   ├── functions                   // common sass functions will go here
    │   ├── mixins                      // common sass mixins will go here
    │   └── variables                   // common variables separated in files by category will go here
    │       ├── _colors.scss            // variables for color
    │       ├── _config.scss            // variables to be used with mixins, functions or frameworks
    │       ├── _forms.scss             // variables for forms
    │       └── _typography.scss        // typographic variables like font-family, font-size, line-height etc.
    ├── desktop                         // extension scripts for desktop site from common will go here
    │   ├── _base.scss                  // same as common but for desktop
    │   ├── components                  // same as common but for desktop
    │   ├── functions                   // same as common but for desktop
    │   ├── ie.scss                     // IE specific hacks will go here
    │   ├── mixins                      // same as common but for desktop
    │   ├── pages                       // page specific partials for desktop site
    │   ├── styles.scss                 // aggregation of base partial, pages & generic desktop styles
    │   ├── variables                   // same as common but for desktop
    │   │   ├── _colors.scss
    │   │   ├── _config.scss
    │   │   ├── _forms.scss
    │   │   └── _typography.scss
    │   └── widgets                     // widget styling rules, each widget will have their own files
    │       ├── _base.scss              // common scripts shared across all widgets
    │       └── leaderboard.scss        // leaderboard widget specific rules
    ├── mobile                          // extension rules for mobile site from common will go here
    │   ├── _base.scss                  // same as common but for mobile
    │   ├── components                  // same as common but for mobile
    │   ├── functions                   // same as common but for mobile
    │   ├── mixins                      // same as common but for mobile
    │   ├── pages                       // page specific partials for mobile site
    │   ├── styles.scss                 // aggregation of base partial, pages & generic mobile styles
    │   ├── variables                   // same as common but for mobile
    │   │   ├── _colors.scss
    │   │   ├── _config.scss
    │   │   ├── _forms.scss
    │   │   └── _typography.scss
    └── tablet                          // extension rules for mobile site from common will go here
        ├── _base.scss                  // same as common but for tablet
        ├── components                  // same as common but for tablet
        ├── functions                   // same as common but for tablet
        ├── mixins
        ├── pages                       // page specific partials for mobile site
        ├── styles.scss                 // aggregation of base partial, pages & generic tablet styles
        └── variables                   // same as common but for tablet     
            ├── _colors.scss
            ├── _config.scss
            ├── _forms.scss
            └── _typography.scss
```               