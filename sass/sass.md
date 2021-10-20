# Sass

Welcome to today's lecture notes on Sass, presented by Anna Hsu, Co-President of TJ Dev Club. Feel free to follow along with the presentation [here](https://docs.google.com/presentation/d/1KGZyi-sT9n9aWrFTDooMSzqAq9ftiSogksI4CgSFw0E/edit?usp=sharing).

## What is Sass?
SASS stands for “Syntactically Awesome StyleSheets,” and it’s a way to write CSS with extra features! As we’ll discover later in the lecture today, some of these features include nesting and single line comments. SASS operates as a CSS preprocessor, turning what you write into CSS, bringing you some simpler solutions to CSS issues.

A lot of static site generators, such as Jekyll and Next.js, allow you to use Sass to streamline your design code.

## Installation
You have to first install Sass. While the recommended way is to [download the installation for your platform and add it to your PATH](https://github.com/sass/dart-sass/releases/tag/1.43.2), if you have Node.js, we’d recommend that you use npm to install it for hassle-less editing. As you’re writing, you’ll also need to compile your Sass into CSS, which you can do through a couple of different ways through the command line. If you want it to compile on every save, you can add the `--watch` flag.

```
sass --watch input.scss output.css
sass --watch app/sass:public/stylesheets
```

## Syntax
### Variables
While CSS does have variables, Sass has simple variables that you can also use. (You can also use them together, if you want, although it might get messy.) The obvious reason to use them would include consistent colors for branding—it’s much easier and faster to change any of the colors. However, if you ever need to update colors through JavaScript, you won’t be able to, although this is a very specific problem.

```scss
$var: value;
```

### Nesting
CSS doesn’t have a lot of indentation beyond the first layer, given that it only has one layer. Sass can help organize where styles belong, making it much easier to understand and less prone to bugs. Sometimes it can also help with specificity, although it’s typically considered bad practice is you a) make your code too specific and b) nest too many layers, because then you can’t really understand what’s going on.

```scss
// the Sass version
nav {
    ul {
        margin: 0;
        padding: 0;
        list-style-type: none;
    }
    a {
        font-weight: 700;
        text-decoration: none;
    }
}

```
```css
/* the CSS version */
nav ul {
    margin: 0;
    padding: 0;
    list-style-type: none;
}

nav a {
    font-weight: 700;
    text-decoration: none;
}

```

### Operators
You can even do math in Sass! It follows the order of operations with the standard mathematical operators (`+`, `-`, `*`, `math.div()`, and `%`), and you can mix different units in your calculations. This can be very helpful when you’re working with sizes of things—whether it’s font size, container size, or viewport size. By using operators, it replaces the CSS `calc()` function.

```scss
.container {
	margin: 100px + 200px;
	padding: 1000px / 100px - 10px;
	height: 5px * 3px;
	width: 1in % 9px;
}

```

### Mixins
Sometimes your CSS might feel redundant. Mixins can allow you to simplify your code by reapplying certain styles, and you can also take in arguments to make it more general. Arguments can have default parameters as well. The notion of extension and inheritance also travels into Sass, although it basically works like an argument-less mixin.

```scss
@mixin background-color($color: "#fff") {
	background-color: $color;
	color: #000;
}
```

### Conditionals
Sass has the normal conditionals of languages such as JavaScript and Python—`if`, `else if`, and `else`. Sometimes these can be helpful in places like mixins! They can be used throughout a Sass file wherever you see fit, though. Unlike other languages, though, only `false` and `null` are truthy values.

```scss
@mixin layout($grid: "false"){
    padding-bottom: 20px;
	display: flex;
	flex-direction: column;
	@if $grid {
		display: grid;
		grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
		gap: 20px;
	}
}
```

### Loops
I haven’t really found that many uses for loops (particularly `while` loops), but sometimes they're helpful, I guess? Some people use them to number their layout classes like Bootstrap (which is actually written using Sass), although is that good practice?

```scss
$font-size: 36px;
@for $i from 1 through 6 {
	h#{$i} {
	font-size: $font-size * (2 / $i);
	font-weight: 600;
	}
}
```

### Partials
In some websites with a wide variety of designs, you’ll find that your code might stretch to a couple hundred lines, making you whip out Ctrl+F every time you need to debug. Sass gives you the ability to modularize all of your CSS! To recognize that a file is a partial, just add an underscore (`_`) to the start of your Sass file. To import the file, leave out both the underscore and the file extension, since Sass knows what you’re trying to import.

```scss
@use "typography";
```

### SCSS vs. Sass
If you look on the SASS website, they display a comparison between SCSS and Sass. They’re pretty much the same thing, albeit with a few relatively minor differences and its confusing marketing. (Is it time to say that every time I’ve been referring to Sass in this presentation I actually really meant SCSS?) Since the structure of the language is very similar to CSS, you’re able to run CSS in SCSS. At its core, SCSS is just extra stuff built onto CSS. On the other hand, Sass is the proprietary version of the language, which strips the CSS and SCSS of braces and semicolons, relying on indentation for structure.

For the sake of simplicity, we’d recommend you just use SCSS.

### .gitignore
If you're using Git as Version Control (which you should!), make sure to add a `.gitignore` with these lines.

```
.sass-cache/
*.css.map
*.sass.map
*.scss.map
```

## Any questions? Feedback?
Congrats on making it this far! Let me know if you have any questions about anything we've covered in this presentation, and don't hesitate to reach out if you have any feedback!
