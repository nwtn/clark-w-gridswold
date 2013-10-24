# Clark W. Gridswold

A customizable responsive grid system, by [David Newton](http://davidnewton.ca/) ([@newtron](http://twitter.com/newtron)).

## What it is

A simple, SASS-based responsive grid that can be easily customized for your responsive design.

## Why it is

Yes, there are a billion responsive grid systems out there. I built this one because I couldn’t find one that did exactly what I wanted, in the way I wanted, and nothing else.

## Customization

The SASS file let’s you customize:

* `$bps` Your breakpoints (using a `min-width` value). You can have as many breakpoints as you like.
* `$grids` The number grids and the number of columns in each grid. You can have has many grids as you like.
* `$gutters`, `$nogutters` Whether you want a grid with gutters, without gutters, or both.
* `$before`, `$after` Whether you want classes to add empty columns to the left and right of an element.
*  `$hgutter` The width of your horizontal gutters.
* `$vgutter` The height of your vertical gutters.

## How it works

The options will generate CSS classes. You can use these classes to align your HTML elements to a grid. Classes are all breakpoint-dependent, so it’s easy to have different layouts for different breakpoints.

There are 5 different basic class types that you can use:

1. **Rows**, e.g. `grid-bp0-row-gutters`: These are used to define rows in a grid.
2. **Columns**, e.g. `grid-bp0-col`: These are used to define that an element is on a grid.
3. **Column widths**, e.g. `grid-bp0-col-1-of-12`: These are used to determine the width of an element.
4. **Empty columns to the left**, e.g. `grid-bp0-col-1-of-12-before`: These are used to define the number of empty grid columns before an element.
5. **Empty columns to the right**, e.g. `grid-bp0-col-1-of-12-after`: These are used to define the number of empty grid columns after an element.

## Smart defaults settings

If you don’t want to use SASS and customize Clark W. Gridswold at all, that’s alright. The pre-generated CSS file uses some smart defaults that you can use right away:

* Includes two grids, one with 12 columns and one with 20.
* Both grids come in a no-gutter variety, and a 3.75% gutter variety.
* Vertical gutters are 1em.
* Breakpoints are at 20em, 48em, and 60em. At a 16px default font size, this translates to 320px, 768px, and 960px.
* Classes to add empty columns before or after an element are included.

## Examples

### Basic example

Let’s start with a very simple structure:

	<header>
		<div>
			<!-- HEADER CONTENT -->
		</div>
	</header>
	<main>
		<aside>
			<!-- SIDEBAR CONTENT -->
		</aside>
		<article>
			<!-- ARTICLE CONTENT -->
		</article>
	</main>
	<footer>
		<div>
			<!-- FOOTER CONTENT -->
		</div>
	</footer>

We want to style this using a simple, mobile-first design. We’ll use a basic typography-based design for very viewports, and then have one breakpoint at 40em. At the 40em breakpoint, we want a 6-column grid with 3% gutters.

In the SASS file, we’ll set the following values:

	$bps:		40em;
	$grids:		6;
	$gutters:	true;
	$nogutters:	false;
	$before:	false;
	$after:		false;
	$hgutter:	3%;
	$vgutter:	1em;

To generate CSS from the SASS file, you’ll need to [install SASS](http://sass-lang.com/install) and then run something like:

	sass clark-w-gridswold.scss > clark-w-gridswold.css

The generated CSS can be included normally in your HTML.

Now, to map our structure to the new grid. We’ll want out header to be its own row, spanning the entire width of the viewport. The sidebar (`aside`) and article should be side-by-side, with the sidebar spanning 2 columns of our grid, and the article spanning 4. Finally, like the header, the footer should span the entire with of the viewport.

To achieve this, we’ll first add classes to define our rows:

	<header class="grid-bp0-row-gutters">
		<div>
			<!-- HEADER CONTENT -->
		</div>
	</header>
	<main class="grid-bp0-row-gutters">
		<aside>
			<!-- SIDEBAR CONTENT -->
		</aside>
		<article>
			<!-- ARTICLE CONTENT -->
		</article>
	</main>
	<footer class="grid-bp0-row-gutters">
		<div>
			<!-- FOOTER CONTENT -->
		</div>
	</footer>

In the code above, the `header`, `main`, and `footer` elements are defining the rows in our grids. The class is broken into four parts:

* `grid`: tell us this is part of the grid system
* `-bp0`: tells us this applies to the first breakpoint
* `-row`: tells us this defines a row
* `-gutters`: tells us the columns in this row have gutters

The children of these *row* elements will define our columns:

	<header class="grid-bp0-row-gutters">
		<div class="grid-bp0-col">
			<!-- HEADER CONTENT -->
		</div>
	</header>
	<main class="grid-bp0-row-gutters">
		<aside class="grid-bp0-col">
			<!-- SIDEBAR CONTENT -->
		</aside>
		<article class="grid-bp0-col">
			<!-- ARTICLE CONTENT -->
		</article>
	</main>
	<footer class="grid-bp0-row-gutters">
		<div class="grid-bp0-col">
			<!-- FOOTER CONTENT -->
		</div>
	</footer>

* `grid`: tell us this is part of the grid system
* `-bp0`: tells us this applies to the first breakpoint
* `-col`: tells us this defines a column

So far, though, we haven’t defined the width of these columns. To do so, we need to add one more class to each column:

	<header class="grid-bp0-row-gutters">
		<div class="grid-bp0-col grid-bp0-col-6-of-6">
			<!-- HEADER CONTENT -->
		</div>
	</header>
	<main class="grid-bp0-row-gutters">
		<aside class="grid-bp0-col grid-bp0-col-2-of-6">
			<!-- SIDEBAR CONTENT -->
		</aside>
		<article class="grid-bp0-col grid-bp0-col-4-of-6">
			<!-- ARTICLE CONTENT -->
		</article>
	</main>
	<footer class="grid-bp0-row-gutters">
		<div class="grid-bp0-col grid-bp0-col-6-of-6">
			<!-- FOOTER CONTENT -->
		</div>
	</footer>

* `grid`: tell us this is part of the grid system
* `-bp0`: tells us this applies to the first breakpoint
* `-col`: tells us this defines a column
* `-2-of-6`, `-4-of-6`, and `-6-of-6`: tells us how many columns on the grid these elements should cover

### Changing the options

Let’s say that, instead of having a 3% horizontal gutter, you wanted no gutter at all baked into the grid. You’d simply change a couple options in the SASS file:

	$gutters:	false;
	$nogutters:	true;
	$hgutter:	3%;

(Strictly speaking, you don’t need to define `$hgutter` at all. Any value you put there will be ignored if `$gutters` is `false`.)

This change will generate classes with names like `grid-bp0-row-nogutters` instead of `grid-bp0-row-gutters`.

If you wanted some rows to use gutters and some not, you can do that too:

	$gutters:	true;
	$nogutters:	true;
	$hgutter:	3%;

With these settings, both `-gutters` and `-nogutters` row classes will be defined, and you can mix and match them in your document.

It’s also easy to change the number of columns in your grid:

	$grids:		3;

Doing this would split the grid into 3 columns instead of 6, and give you classes with names like `grid-bp0-col-1-of-3` instead of `grid-bp0-col-1-of-6`.


### Adding another breakpoint

Most responsive designs have more than one breakpoint. Many grid systems try to intelligently guess how your columns should change and adapt at these different breakpoints.

Nuts to that. You’re the designer, you should be making that decision. That’s why Clark W. Gridswold gives you the power to change grid definitions at each breakpoint.

So, starting with our same example from above, let’s say we want to add another breakpoint at 60em. We just add that to our SASS file:

	$bps:		40em, 60em;

…regenerate the CSS, and we’re good to go.

Now, in addition to the `grid-bp0-` classes we used above, we’ll also have a new set of `grid-bp1-` classes we can use.

At the 60em breakpoint, the sidebar is getting too wide, so we want to snap it back to one column, and change the article to 5 of our 6 columns. As before, first we define our rows for this breakpoint:

	<header class="grid-bp0-row-gutters">
		<div class="grid-bp0-col grid-bp0-col-6-of-6">
			<!-- HEADER CONTENT -->
		</div>
	</header>
	<main class="grid-bp0-row-gutters grid-bp1-row-gutters">
		<aside class="grid-bp0-col grid-bp0-col-2-of-6">
			<!-- SIDEBAR CONTENT -->
		</aside>
		<article class="grid-bp0-col grid-bp0-col-4-of-6">
			<!-- ARTICLE CONTENT -->
		</article>
	</main>
	<footer class="grid-bp0-row-gutters">
		<div class="grid-bp0-col grid-bp0-col-6-of-6">
			<!-- FOOTER CONTENT -->
		</div>
	</footer>

Here we’ve added `grid-bp1-row-gutters` to `main`, to say that it will be a row for our new breakpoint. Since the `header` and `footer` rows aren’t changing from the previous breakpoint, we don’t need to add or change any classes there.

Next, we’ll define our columns and widths:

	<header class="grid-bp0-row-gutters">
		<div class="grid-bp0-col grid-bp0-col-6-of-6">
			<!-- HEADER CONTENT -->
		</div>
	</header>
	<main class="grid-bp0-row-gutters grid-bp1-row-gutters">
		<aside class="grid-bp0-col grid-bp0-col-2-of-6 grid-bp1-col grid-bp1-col-1-of-6">
			<!-- SIDEBAR CONTENT -->
		</aside>
		<article class="grid-bp0-col grid-bp0-col-4-of-6 grid-bp1-col grid-bp1-col-5-of-6">
			<!-- ARTICLE CONTENT -->
		</article>
	</main>
	<footer class="grid-bp0-row-gutters">
		<div class="grid-bp0-col grid-bp0-col-6-of-6">
			<!-- FOOTER CONTENT -->
		</div>
	</footer>

That’s it!

### Multiple grids

Sometimes our grids don’t work easily from one viewpoint to another. Sometimes it’s fun to just switch things up. Either way, you may want different grids at different breakpoints, and Clark W. Gridswold is OK with that.

Just list the number of columns for each grid in the SASS:

	$grids:		6, 5;

…and you’re cookin’. Now, you’ll have a 6-column grid and a 5-column grid available to you at each breakpoint.

Going back to our previous example, maybe shrinking the sidebar down from 1/3 to 1/6 of the viewport was too drastic. 1/5 is probably about right, but we can’t do that with a 6-column grid! Enter the 5-col grid:

	<header class="grid-bp0-row-gutters">
		<div class="grid-bp0-col grid-bp0-col-6-of-6">
			<!-- HEADER CONTENT -->
		</div>
	</header>
	<main class="grid-bp0-row-gutters grid-bp1-row-gutters">
		<aside class="grid-bp0-col grid-bp0-col-2-of-6 grid-bp1-col grid-bp1-col-1-of-5">
			<!-- SIDEBAR CONTENT -->
		</aside>
		<article class="grid-bp0-col grid-bp0-col-4-of-6 grid-bp1-col grid-bp1-col-4-of-5">
			<!-- ARTICLE CONTENT -->
		</article>
	</main>
	<footer class="grid-bp0-row-gutters">
		<div class="grid-bp0-col grid-bp0-col-6-of-6">
			<!-- FOOTER CONTENT -->
		</div>
	</footer>

By making the above change to our SASS settings, and changing the `aside` from `grid-bp1-col-1-of-6` to `grid-bp1-col-1-of-5` (and the `article` to `grid-bp1-col-4-of-5`), we get the desired change on the new 5-column grid.

### Empty columns

Our design is coming along swimmingly, but the main content is feeling a bit cramped. We could adjust our horizontal gutters, but it won’t give us enough breathing room. Instead, let’s shrink our `article` to 3 columns wide (on the 5 column) grid, and include and empty column between it and the sidebar.

	<header class="grid-bp0-row-gutters">
		<div class="grid-bp0-col grid-bp0-col-6-of-6">
			<!-- HEADER CONTENT -->
		</div>
	</header>
	<main class="grid-bp0-row-gutters grid-bp1-row-gutters">
		<aside class="grid-bp0-col grid-bp0-col-2-of-6 grid-bp1-col grid-bp1-col-1-of-5">
			<!-- SIDEBAR CONTENT -->
		</aside>
		<article class="grid-bp0-col grid-bp0-col-4-of-6 grid-bp1-col grid-bp1-col-3-of-5">
			<!-- ARTICLE CONTENT -->
		</article>
	</main>
	<footer class="grid-bp0-row-gutters">
		<div class="grid-bp0-col grid-bp0-col-6-of-6">
			<!-- FOOTER CONTENT -->
		</div>
	</footer>

Just changing the width isn’t enough, though. The code above will leave the sidebar and article right next to each other, leaving an empty column after the `article`. We need to get an empty column *before* the `article`. To do this, we just need to enable an option in SASS:

	$before:	true;

This will generate classes like `grid-bp1-col-1-of-5-before`, which we can use to add an empty column before (to the left) of the `article`:

	<header class="grid-bp0-row-gutters">
		<div class="grid-bp0-col grid-bp0-col-6-of-6">
			<!-- HEADER CONTENT -->
		</div>
	</header>
	<main class="grid-bp0-row-gutters grid-bp1-row-gutters">
		<aside class="grid-bp0-col grid-bp0-col-2-of-6 grid-bp1-col grid-bp1-col-1-of-5">
			<!-- SIDEBAR CONTENT -->
		</aside>
		<article class="grid-bp0-col grid-bp0-col-4-of-6 grid-bp1-col grid-bp1-col-3-of-5 grid-bp1-col-1-of-5-before">
			<!-- ARTICLE CONTENT -->
		</article>
	</main>
	<footer class="grid-bp0-row-gutters">
		<div class="grid-bp0-col grid-bp0-col-6-of-6">
			<!-- FOOTER CONTENT -->
		</div>
	</footer>

Depending on how your brain works, you may want to add an empty column *after* (to the right of) the sidebar, instead. You can do that too! In the SASS:

	$after:	true;
	
In the HTML:

	<header class="grid-bp0-row-gutters">
		<div class="grid-bp0-col grid-bp0-col-6-of-6">
			<!-- HEADER CONTENT -->
		</div>
	</header>
	<main class="grid-bp0-row-gutters grid-bp1-row-gutters">
		<aside class="grid-bp0-col grid-bp0-col-2-of-6 grid-bp1-col grid-bp1-col-1-of-5 grid-bp1-col-1-of-5-after">
			<!-- SIDEBAR CONTENT -->
		</aside>
		<article class="grid-bp0-col grid-bp0-col-4-of-6 grid-bp1-col grid-bp1-col-3-of-5">
			<!-- ARTICLE CONTENT -->
		</article>
	</main>
	<footer class="grid-bp0-row-gutters">
		<div class="grid-bp0-col grid-bp0-col-6-of-6">
			<!-- FOOTER CONTENT -->
		</div>
	</footer>

Blamo.

## Default styling

Clark W. Gridswold operates under the assumption that a) the browsers you’re targetting can understand media queries, and b) if they don’t, they won’t be getting a design that needs a grid. If you do need the grid classes to be available in your base (non-MQ) styles, just set your first breakpoint to "0" and manually delete the `@media` declaration from the generated CSS.

## Contribute!

I’ve only done really limited testing with this so far, so definitely file an issue or pull request if you run into problems. I’m sure I screwed *something* up.

## A few words on verbosity

There are a lot of classes, and they have long names. Ya man, I know. It’s cool. Nothing’s going to be the right fit for everybody.

## License

[The MIT License (MIT)](http://opensource.org/licenses/MIT)
