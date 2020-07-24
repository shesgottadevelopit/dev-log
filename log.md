# Activity Log: She's Gotta Develop It
What am I making? What am I developing? What am I doing? Stream of consciousness notetaking/coding/whatyamajiggy

_Log notes organized by date (most recent)_
<!---
<details><summary>template for entries</summary>

## Entry No. 00x
**Day xx/xx/xxxx**

</details>
--->

## Entry No.34
**Thursday 7/23/2020**
I solved that problem! I should stop while I'm ahead.

I wanted to find a way to add the template class to my template but somehow modify the template class slug to make it easier for me to target it with CSS.

I figured out that in order to match different strings, I need to use the `prep_replace` methods more than once. Here is what I did:
```php
<?php
/**
 * Template Functions & Tags
 * Eventually, some of the functionality here could be replaced by core features.
 * @package lemons
 */
function lemons_template_class($template_class) {
	$sanitized = preg_replace( '~page-templates/~', '', $template_class );
	$sanitized = preg_replace( '~php~', '', $sanitized);
	$sanitized = preg_replace( '/[^A-Za-z0-9_-]/', '', $sanitized );
	$sanitized = $sanitized.'-template';

	return $sanitized; 
}

// And in my template it looks something like this: 
<div id="primary" class="content-area <?php echo esc_html(lemons_template_class( get_page_template_slug( $post->ID )));?>">

// Which outputs something like this:
<div id="primary" class="content-area single-column-template">
```

All of this thanks to a number of resources:
- https://www.php.net/manual/en/function.preg-replace.php 
- https://www.w3schools.com/php/func_regex_preg_replace.asp
- https://www.tutorialrepublic.com/php-tutorial/php-regular-expressions.php
- https://developer.wordpress.org/reference/functions/sanitize_html_class/

Today I also added some CSS Gutenberg files

## Entry No. 033
**Wednesday 7/22/2020**
Today was very productive also.

RE: Lemons Starter Theme, I:
- Included a file that added theme support for Gutenberg features
- Learned how to create Page Templates (which I apparently used with Genesis). I didn't know it was something I could do myself :-)
- While creating new page templates, I decided to explore how to apply various CSS styles to each template and settled on the `get_page_template_slug()` function which would allow me to insert that page template class at various points in the markup. But I realized the santization of the page template slug name wasn't working how I want soooo....

**Next problem to solve:**
I am going to create a function (might be a filter or a function with a filter) and it will find & replace some of those character in the original page template slug first using a PHP method and then I'll run it through the WordPress `santize_html` function. And find a way to insert this function into my markup, 

## Entry No. 032
**Tuesday 7/21/2020**
Soooooooo, I'm pretty sure I did some work on "Lemons" on Friday but didn't bother adding it to the log, my bad.

Today, I decided to update my Maintenance Mode plugin & theme template. The way it currently works is:
- The plugin checks if the theme has a `maintenance.php` file and if it does it renders it
- If it doesn't, it checks the plugin directory to see if it has a maintenance.php file
- If the plugin doesn't it renders a simple message.

Today I added an option that allows me to build out the content & messaging for the Maintenance Mode page like I would on every page. As I'm typing this, I realize I could probably add this to the plugin, so it it works out-of-the-box. I think I might do that too but would need to figure out how to pull in all of the regular theme assets. 

Proud of myself. It is 11:14p right now and I've been working on this since about 6pm (I've done other things but mostly this). 

I love solving a problem. 

## Entry No. 031
**Thursday 07/16/2020**
I was able to consolidate all of my starter themes into a single one that I'm calling "Lemons".

Next I will:
- make any updates pulling in changes from the master _s theme
- look into incorporating the Theme Alliance Hooks feature
- update CSS to make it cleaner, pulling in items from my Genesis Starter and other more final custom themes. I'll also see what might be the easiest way to incorporate newer layout themes that utilize grid & flexbox. Your girl is still with the floats. 

Yesterday I spent more time than I'd like to admit trying to copy over a local database into a new WP install. I figured it out early this morning. No more installs until I have to. But I did it this time because it guaranteed I'd be working with the same set of test content instead of having to reimport it all over again. 

## Entry No. 030
**Wednesday 07/15/2020**
Today I installed those essential plugins and I'm going to try and do a quick clean up. I have like 5 different boilerplate theme versions and I need to figure out what is the most updated, get rid of the others and use that as my baseline.

## Entry No. 029
**Tuesday 07/14/2020**
Soooo on to the next project. This is sort of a mini-admin project. I'm basically going to update my boilerplate WP theme, pulling in new stuff from the WP Underscores theme. 

Later I might also refine my Genesis boilerplate theme called Eve.

In order to do this, I'm doing a few things, mostly optional:
- create new Wordpress instance in WAMP (install the software & setup the database)
- set up a virtual host
- upload test content from 3 different sources

Next I'll need to
- Update the content so it aligns with the theme I'm planning to develop
- Create additional pages
- Install essential plugins

## Entry No. 028
**Saturday 07/11/2020**
Whewwww what a journey! [She's Gotta Develop It](https://shesgottadevelopit.com) is live now! I got an MVP up and of course there are things to fix but I need to remind myself it does not **have** to be perfect. Can't believe this all started in February 2020. I set up all of the appropriate redirects from the older site. I'm happy I got that done now I can move on to my other projects. My goal moving forward to is to reduce the amount of time it takes for me to turnaround one of these "custom" builds. 

I sitll need to prune content on this site & create some new content. I'll also create a post covering my experience creating a Genesis theme from scratch. 

## Entry No. 027
**Saturday 06/20/2020**
I think I have a fully functional version that is ready for the world. I worked on this earlier in the week and really got myself stuck trying to fix something that didn't even matter (the Edit link - which you can only see when you're logged in). I guess I can get around to it later but I had to level with myself and keep it moving. 

I need to now figure out how to package my block plugin & do all the testing and then set up redirects. 

**Pats self on back**

## Entry No. 026
**Sunday 06/15/2020**
Mission Accomplished! I finally figured out how to create a Latest Posts block with WordPress Gutenberg. My block plugin renders the most recent 5 posts. There are things I want to improve on:
- [ ] add the option to modify the number of posts that are included
- [ ] possibily text editing features
- [ ] apply frontend styles to the backend (in general this is a to-do item)

So proud of myself! I'm definitely going to hunker down and learn React this summer but I was able to piece together something that works using the following resources:
- This video tutorial covered how to create a dynamic block that lists the recent posts titles only: https://www.youtube.com/watch?v=XkjrrLR0Y3E&t=1216s
- This video was reinforcement and demonstrated another way of interacting with content via the WP REST API: https://www.youtube.com/watch?v=sYHYTk0jeE8
- This page helped me figure out how to render content without tags/markup showing on the backend: https://developer.wordpress.org/block-editor/developers/richtext/#html-formatting-tags-display-in-the-content
- Reference: https://www.billerickson.net/building-gutenberg-block/
- Reference: https://medium.com/@eudestwt/how-to-make-a-dynamic-wordpress-gutenberg-block-with-server-side-rending-3cb0dd6744ed
- Covers two ways of building Gutenberg blocks: https://jasonbahl.com/2018/11/15/two-ways-to-build-gutenberg-blocks/
- Simple Gist: https://gist.github.com/Shelob9/144055408101e2fdfc4bf34adc85dd04


Also, this is the path to the json file with post info from the WordPress REST API: `/wp-json/wp/v2/posts`, just append that to your domain/url. More info is [here](https://developer.wordpress.org/rest-api/reference/)

Links to check out later:
- https://markcormack.co.uk/getting-gutenberg-how-im-using-wordpress-new-editor/
- https://johnblackbourn.com/gutenberg-block-template-part/
- 


Other things: I might change the width of my site container to 750px.

What's left to do with `front-page.php` is styling the blocks & other content.

Mission Accomplished!


## Entry No. 025
**Sunday 06/14/2020**
Ok so I'm finally going to try and create a gutenberg block, so I'll be following along with a couple of tutorials.

1. Installed `create-guten-block` globally and following the instructions in the documentation for setting up the block.
2. I activated the gutenberg block plugin in my admin dashboard and viewed a page to test whether it was active (it was!)
3. For this exercise, I'm going to use `front-page.php` since that is the page I'm creating this block for (although it can be used on other pages)
4. All of the work I'll be doing will be done on files withing the `src` directory. According to this [CSSTricks.com article](https://css-tricks.com/learning-gutenberg-3-primer-with-create-guten-block/),
these are the key files within the block directory that:

> block/block.js — All the JavaScript for the individual block.
> block/editor.scss — Sass partial for styles specific to the editor view,
> block/style.scss — Sass partial for styles specific to the front-end view, i.e. what you see when you view your page/post.

Ok, so as far as I got today was creating the block and rendering it. I haven't figured out how to use the API yet but next time.


## Entry No. 024
**Wednesday 06/09/2020**
Started a new job this week so haven't had as much time to return to this. I'm going to work on gaining a better understanding of how blocks work in Gutenberg/WordPress. This [key concepts](https://developer.wordpress.org/block-editor/principles/key-concepts/) page is a great starting point. 

### Static vs dynamic
> Blocks can be static or dynamic. Static blocks contain rendered content and an object of Attributes used to re-render based on changes. Dynamic blocks require server-side data and rendering while the post content is being generated (rendering).
> Each block contains Attributes or configuration settings, which can be sourced from raw HTML in the content via meta or other customizable origins.

### Reusable blocks
> Reusable blocks are a way to share a block (or multiple blocks) as a reusable, repeatable piece of content.
> Any edits to a reusable block are made to every usage of that repeatable block.
> **Reusable blocks are stored as a hidden post type** and are dynamic blocks that “ref” or reference the post_id and return the post_content for that wp_block.

I'll also follow along with the tutorial on this page: https://developer.wordpress.org/block-editor/tutorials/block-tutorial/

This tutorial also explains why the `create-guten-block` is helpful: https://www.angelleye.com/gutenberg-wordpress-tutorial-build-custom-block/


Videos I found that I'll revisit
- Video 1: https://www.youtube.com/watch?v=sYHYTk0jeE8 __this was easy to follow and explained why the `create-guten-block` app would be helpful__
- Video 2: https://www.youtube.com/watch?v=2CGFLwSoDbY (and the accompanying playlist: https://www.youtube.com/playlist?list=PLriKzYyLb28lHhftzU7Z_DJ32mvLy4KKH)
- Video 3: https://www.youtube.com/watch?v=XkjrrLR0Y3E
- Video 4: https://www.youtube.com/watch?v=vxxHoEqxjKE


Other resources: 
- https://www.advancedcustomfields.com/blog/the-state-of-acf-in-a-gutenberg-world/
- https://webdevstudios.com/2019/10/24/advanced-custom-fields-gutenberg-wd_s/
- https://awhitepixel.com/blog/wordpress-gutenberg-create-custom-block-part-9-dynamic-blocks-php-render/
- https://github.com/WordPress/gutenberg/tree/master/packages/block-library/src/latest-posts



## Entry No. 023
**Saturday 06/06/2020**
Haven't been doing the best job of documenting. As expected, the race to wrap up the major parts of these Genesis theme requires me to do alot of Googling, testing, and internal negotiating (mostly reminding myself that I don't need to the perfect solution, just a solution that works).

Most of the theme is done. I have some styling things I will eventually fix but the main next thing requiring my attention would be the redesign of the static-ish homepage (It will have static content and then a listing of the most recent posts). And then I'll need to develop a strategy for redirecting pages to the newer domain. 

Update:
I did all the small styling fixes so my focus now is on how I'm able to design a hybrid static/dynamic homepage. The core features of the page will be:
- requirement #1: a classic text editor block
- requirement #2: a listing of my most recent 4-5 posts (or just 4-5 featured posts)
- requirement #3: a listing of projects I've curated for display on the homepage. This should be optional. 

**The only dynamic part should be the recent/featured posts.**

As a result of my research, I've been able to cobble together what seems like a way to do what I want:
- I'm able to just add blocks at the top of the page in the Admin dashboard so that satisfies requirement #1. 
- This post describes out create the template page (e.g. `front-page.php`) and add a custom loop to satisfy requirement #2: https://www.abrightclearweb.com/a-custom-homepage-for-the-genesis-framework/. Of course I'll need to update the formatting for this and might start using template parts (e.g. https://wpshout.com/get-template-part/).
  - This post is another solution for adding dynamic content to a static template: https://robincornett.com/custom-front-page/
  - Other resources:
    - https://carriedils.com/custom-page-template-genesis/
    - https://www.netklik.com/wordpress/add-blog-posts-static-home-page-genesis-wordpress/
- I now need to figure out how include a field in the `front-page.php` file that allows me to add blocks and/or additional copy below the custom loop.

Something else I'm now realizing is that I might be able to fulfill this task more easily if I create a dynamic block for the "Recent Posts" and then just building a page with a bunch of different blocks. Hmmm. I'll return to this later:
- https://riad.blog/2017/10/16/one-thousand-and-one-way-to-extend-gutenberg-today/
- https://torquemag.io/2019/12/how-to-create-a-custom-wordpress-website-with-gutenberg-block/
- https://torquemag.io/2019/05/create-gutenberg-block/
- https://appsaloon.be/blog/how-to-build-a-dynamic-gutenberg-block-tutorial/
- https://joeyfarruggio.com/wordpress/custom-post-loop-as-a-gutenberg-block/
- https://www.billerickson.net/building-a-wordpress-theme-with-gutenberg/
- https://www.nutsandboltsmedia.com/acf-genesis-landing-page/
- https://developer.wordpress.org/block-editor/developers/block-api/block-templates/
- https://wpshout.com/get-template-part/


Also learned about block templates as part of my research: 
- https://www.billerickson.net/gutenberg-block-templates/

Once I sit my ass down, I get shit done. I'm actually surprised by how much I was able to get done in such a short period of time.

## Entry No. 022
**Wednesday 06/03/2020**
My goal over the next 2-3 days is to finalize this design and launch this new site! Enough already. 

What I worked on today:
1. After hours of googling to better understand the differences between `return`, `sprintf`, and `printf` I figured out how to get my comments to render like this: **"15 comments on [insert name of post]"** . Slightly modified my original iheartcode markup to filter it. 
2. Finished styling for individual posts & pages

## Entry No. 021
**Tuesday 04/13/2020**
Today I struggled to figure out how to get the number of comments to appear below the blog post like so:  "15 comments on [insert name of post]"

Will try again tommorrow, I'm spent. 


## Entry No. 020
**Tuesday 04/07/2020**
An entire month. Alot has happened since my last updates... like coronavirus. But I'm back like I never left.

I updated my project board breaking out tasks I need to complete to get my theme in tip-top shape. Today I'll focus on:
- defining variables in my stylesheet (colors & font sizes)
- exporting my logo as SVG for the web
- styling the individual post page
- figure out how to move my "post-meta" into the "entry-header"

### Tips for optimizing SVG for web:

- Select Objects -> Artboards -> Fit Artboard to Bounds
- Profile: SVG 1.1
- Type: Convert to outline – This makes sure that any text used is converted to shapes.
- Image location: Embed – If you are including bitmap images (probably not), they will be included in the file, rather than linked to separate files.
- Decimals: This is the level of precision. You may want to set to 2 or 1 decimals (default 3) to decrease the file size.
- Keep “Compressed” and “Optimized for Adobe SVG Viewer” unchecked (Visible in main “Save for Web” export menu in Adobe CS3).
*source: https://joshuawinn.com/svg-export-settings-for-the-web-with-adobe-illustrator/

Other resources:
- https://medium.com/@colinlord/how-to-export-svgs-for-the-web-from-illustrator-829bc1c841f6
- https://css-tricks.com/snippets/svg/abobe-illustrator-export-options/
- 


## Entry No. 019
**Friday 03/06/2020**
My todo list is slightly different than what I had before but that is fine, I'm tracking it in the theme folder anyway. 

Today I focused on 
1. adding support for the ACF field I use for subtitles
2. figuring out how to make sure my theme uses the original WordPress category/tag descriptions instead of the Genesis one
3. adding class names to existing elements using Genesis filters and Genesis attributes (e.g. genesis_attr_footer-widget-areas), very handy for the footers I finally got around to
4. removed support for structural wraps throughout the theme... realized I don't need it
5. removed support for some of the layouts (this is a full-width site) and sidebars/widgets

One major lingering data structure thing I need to figure out is appending "Category:" or "Tag:" to my archive page when users navigate to those taxonomy pages. It works fine on monthly archive pages. So once I figure that out, I think I'll be able to move on to the actual styling part because right now, everything is right where I want it to be. 

Of course at some point I'm going to need to design this new homepage, since the blog will no longer be at the root of the site. 

Exciting progress! I think I'm going to give myself a break for the weekend. 

## Entry No. 018
**Thursday 03/05/2020**
So just to recap last night's success: I now have two ways of modifying markup. Of course the version I outlined below is more ideal to me because I can read the code and it makes sense. The other option (from Bill Erickson) I'm not entirely sure how to read it. But both of them work. So in my theme I've got the entry header all fixed up. Now time to move on to the entry footer. 

Things left to do:
- [ ] fix formatting for the post pagination
- [ ] fix the styling for the header
- [ ] fix the styling for the widgets
- [ ] fix the styling for the footer
- [ ] fix the styling for the posts
- [ ] style archive pages
- [ ] design a homepage
- [ ] add acf to theme & figure out how to reapply that

## Entry No. 017
**Wednesday 03/04/2020**
I never got a chance to update the log last night when I wrapped up but I'm so excited to share my updates. So in process of trying to recreate my existing them in Genesis, I realized I didn't have as much control with styling and repositioning things like the `genesis_post_meta` which includes categories & tags and `genesis_post_info` which includes the post date, author link, etc.

Genesis uses shortcodes which makes formatting that kind of thing easier, but it comes with the default Genesis markup. This isn't normally an issue but in my theme the entry header is structured like this:

```
category 1 | date
entry title
tag1 tag2 tag3
edit link (when the admin is logged in)
```

This layout splits up the `post_info` (e.g. the date and edit link) and it also separates the `post_meta` (e.g. the categories and tags). I had to use a number of hooks to get this ordered just the way I want. 

One side effect of this **reordering** is that Genesis automatically wraps the content in an element with a particular CSS class name, in this case it is a paragraph tag with `entry-meta` as the class. This isn't a big issue but that class appears twice in the page (with the category & date and then further down with the tag and edit link) and there might be some clashing with the design if they're both grouped under the same class name. There could be other side effects, but I don't what they'd be yet. I sometimes even noticed times when an empty paragraph tag would appear below the actual `post-meta` content. Also not a big issue but I just don't want random elements scattered through my markup. So I was trying to figure out a way to customize the wrapper element that is automatically generated when `genesis_post_meta` is rendered on the page. 

After lots of "Google-ing" I figured out a way to do it through the Genesis Markup API, but first I needed to know how to use the API and finding documentation on that was a challenge. The closest thing I could find for that was [this article](https://wpbeaches.com/changing-the-genesis-header-html-output/), so I tried my hand at doing something similar but for a different segment of the entry and it finally worked! My one big win of the day.

Using the Genesis Markup API means I need to find the original code that is used to generate something like `genesis_post_meta` and copy that into my `functions.php` file and then make modifications as needed. I would of course need to remove the original hook and then add a new hook with this newer function with my custom code. 

The code for `genesis_post_meta` appears in the `post.php` file inside the Genesis Framework (`lib > structure > post.php`).

Here's the before in `post.php`:
```php
function genesis_post_meta() {

	if ( ! post_type_supports( get_post_type(), 'genesis-entry-meta-after-content' ) ) {
		return;
	}

	$post_meta = wp_kses_post( genesis_get_option( 'entry_meta_after_content' ) );
	$filtered  = apply_filters( 'genesis_post_meta', $post_meta );

	if ( '' === trim( $filtered ) ) {
		return;
	}

	genesis_markup(
		[
			'open'    => '<p %s>',
			'close'   => '</p>',
			'content' => genesis_strip_p_tags( $filtered ),
			'context' => 'entry-meta-after-content',
		]
	);

}
```

And here is the after that I'll store in my `functions.php`:

```php
function customized_genesis_post_meta() {

	if ( ! post_type_supports( get_post_type(), 'genesis-entry-meta-after-content' ) ) {
		return;
	}

	$post_meta = wp_kses_post( genesis_get_option( 'entry_meta_after_content' ) );
	$filtered  = apply_filters( 'genesis_post_meta', $post_meta );

	if ( '' === trim( $filtered ) ) {
		return;
	}
	genesis_markup( array (

			'open'    => '<div class="my-class">', // this is the only line I've modified
			'close'   => '</div>',
			'content' => genesis_strip_p_tags( $filtered ),
			'context' => 'entry-meta-after-content',

	) );

}

/**
* And these are the hooks I activate in the theme to make this all work the way I want
*/

remove_action('genesis_entry_footer', 'genesis_post_meta');
add_action( 'genesis_entry_header', 'customized_genesis_post_meta', 10);
```

As a result of all of this "Google-ing" I also had to become acquainted with some other WordPress things like the `do_shortcode()` [function](https://developer.wordpress.org/reference/functions/do_shortcode/).

I never got a chance to try another idea I had, but it would involve using a Genesis filter to replace the `.entry-meta` class with one of my choice using a function like this:

```php
function replace_class_name( $attributes ) {
	$attributes['class'] = 'my-meta';
	return $attributes;
  }
  add_filter( 'genesis_attr_entry-meta-before-content', 'replace_class_name' );
```

Some resources:
- https://www.billerickson.net/code/genesis-post-info-markup/ (This also works exactly how I'd need it to but I hadn't tried it yet)
- https://wpbeaches.com/adding-attribute-html-section-genesis/
- https://www.jeanphilippemarchand.com/code/add-custom-class-html-elements-genesis/
- https://designody.com/genesis-attributes/
- https://gist.github.com/inetbiz/0eba8d4af82a880fceb13f086dcb03b7#file-markup-php-L159


The feeling I get when I solve a problem, **chef's kiss**.


## Entry No. 016
**Tuesday 03/03/2020**
Still working on recreating my theme for `akudo.codes` using Genesis. The layout won't change much, I might actually add some new layouts and a "front page/home page". The color palette will definitely be updated. 


## Entry No. 015
**Monday 03/02/2020**
Today I'm working on branding for my site and also still toying around with fonts.

I'll also start porting over some legacy styles into my new Genesis stylesheet, things I know I'll want to maintain in my new theme. 

Examples include:

```scss
// existing theme --> genesis theme
.site-page --> .site-container
.masthead .full-width-bar --> .site-header
.all-content --> .site-inner
.site-content --> .content
.site-widgets --> .sidebar .sidebar-primary .widget-area
.site-footer .full-width-bar --> .site-footer
.article-header --> .entry-header
.article-title --> .entry-title
.article-meta --> .entry-meta
.article-content --> .entry-content
no footer class --> .entry-footer // use for pagination on single posts
.navigation .post-navigation -->
.post-comments --> .entry-comments

```

## Entry No. 014
**Friday 02/27/2020**
One of my projects uses a custom font so I'm learning for the first time how to properly use the `font-face` property. I've always used Google Fonts so this is a new beast that will take some figuring out. 

Learned I can use the [FontSquirrel](https://www.fontsquirrel.com/tools/webfont-generator) service to convert my **legal** font to the `woff` format and it also generates a `.css` file. Very cool. 

## Entry No. 013
**Thursday 02/26/2020**
I started playing around with Genesis hooks and filters, read up on some of the documentation and just dived in. Some things I tried out:
- moving the post info (date, time, byline, comments,etc) to a different location on the page, above the post title
- making the change listed above only appear on single posts and not the general loop
- adding post navigation (not the same as post navigation for the entire site)

Also learned that with Genesis 3.something you're able to move the post info (or post meta) using shortcodes directly in the WordPress Customizer, which is cool.

But I'm still figuring out shit.

## Entry No. 012
**Wednesday 02/25/2020**
I need to do a better job of using this log because it doesn't just keep me accountable but it is a good way to remind myself I'm making progress, small steps, but steps nonetheless.

I've been learning how to use the Genesis WordPress framework and have been doing a mixture of coding/experimenting and environment setup.

Yesterday I needed to figure out how to use a plugin to find/replace entries in the database I'm planning to import into one of my staging sites.

Today, more site setup and creating a new directory for this particular project. Plan is to move `akudo.codes` to `shesgottadevelopit.com`. That will require some redirects and database migration. I'm also doing a theme refresh as a part of it.

Other than that, here are the goals I had for Q1 of this year:
- [x] Learn about and how to build child themes with the Genesis framework 
- [x] Learn about and how to use Wordpress Gutenberg
- [ ] Learn about the AWS Cloud Practitioner exam and decide if I want to take it
- [ ] Learn how to deploy a small project on AWS
- [ ] Build a small app with React

I've made progress so far and I'm happy about that :-).

## Entry No. 011
**Tuesday 01/14/2020**
I'm conducting tests to make updates on a post on my site that has gotten a few comments/questions/concerns. Here is the [original post](https://akudo.codes/2018/12/10/mklink-command-in-windows-ubuntu-wsl).

I'll need to update this post because I've been using this script since the earliest iterations of Windows Bash.

**Project Folder Hierarchy**
The `target` directory is located here on my computer: /mnt/c/projects/mklink-test/target
```
├── c
|	├── projects
|	│   ├── mklink-test
|	|	│   ├── target
|	|	│   │   ├── readme.md
|	|	│   │   └── testing.txt
|	├── newProjects
|	│   ├── mklink-test-2
```
And the creation of the symlink will result in this updated directory tree:

```
├── c
|	├── projects
|	│   ├── mklink-test
|	|	│   ├── target
|	|	│   │   ├── readme.md
|	|	│   │   └── testing.txt
|	|	│   ├── ***newSymlink
|	|	│   │   ├── readme.md
|	|	│   │   └── testing.txt
|	├── newProjects
|	│   ├── mklink-test-2
|	|	│   ├── ***newSymlink
|	|	│   │   ├── readme.md
|	|	│   │   └── testing.txt
```
### Here is what I learned

**pwd is inside of WSL directories**
If you're in your WSL home directory (e.g. the pwd is `\\wsl$\Ubuntu\home\badgalriri`), and you're attempting to create a symlink from a target directory on Windows, you can create a symlink using an absolute path:
`mklink /projects/mklink-test/symlink1 /projects/mklink-test/target`
FYI: You need to omit the `/mnt/c` part of the path.

**pwd is inside of your WSL symlink**
If you're like me and have linux symlinks created using this command (`ln -s /mnt/c/projects/ myProjects`) and which results in a directory listing like: `myProjects -> /mnt/c/projects`, then when your pwd is `~/myProjects`, you can use relative paths:
```bash
mklink mklink-test/symlink2 mklink-test/target
```

**pwd is inside of a Windows directory**
If you're in a Windows directory (e.g., the pwd is somewhere in `/mnt/c` or `/mnt/c/projects` or `/mnt/c/Users/Rihanna/`), you can create a symlink using an absolute path or a relative path (if you're in the directory) using one of the following commands. 

```bash
## Absolute Path from pwd /mnt/c
mklink projects/mklink-test/symlink3 projects/mklink-test/target

## Relative Path from pwd /mnt/c/projects
mklink mklink-test/symlink4 mklink-test/target

## Relative Path from pwd /mnt/c/projects to a completely different directory referenced by the absolute path
mklink /newProjects/mklink-test-2/symlink5 mklink-test/target # note that the link path is Absolute here

```

**Key changes**: I'm using a modified `mklink.sh` file which is referenced here: 
All of these edits are reflected in my [post](https://gist.github.com/shesgottadevelopit/84c6bb230e6128aea4fb13fc8c79b93a).


## Entry No. 010
**Tuesday 11/19/2019**
Whewww I took a little bit of a break and have not been updating my log.

Decided to sort of pivot and work on setting up some automation with Slack, Trello, Google Drive, and maybe some other apps. 

That's the update :-). 

## Entry No. 009
**Tuesday 11/5/2019**

Backk to theming. I'm going to give Local by Flywheel a try... again. I'm using the Beta version for 5.something. I didn't know that this application was basically a Docker app, so that is pretty cool.

That said, because it stores things in `/mnt/c/users/username` I decided to create a symlink to that directory in my regular project folder because I don't use my Windows home directory. 

I used my own [tutorial](https://akudo.codes/2018/12/10/mklink-command-in-windows-ubuntu-wsl/) on creating cross-platform symlinks but ran into an issue when I tried to run my command using absolute paths.

```bash

pwd /mnt/c/myProjectFolder/localSites
$ mklink localSites /users/myUserAccount/localSites

```
That command would result in a broken symlink that looked like this `localSites -> /mnt/c/mnt/c/users/myUserAccount/localSites`. Not sure why it kept adding an extra `/mnt/c`. So after almost an entire hour of debugging, I tried this instead: `mklink localSites /users/myUserAccount/localSites` and it finally worked. Not sure why that is though. 

## Entry No. 008
**Monday 11/4/2019**

I decided to try out Local by Flywheel and I think I'm going to pass on that for now. Seems like it really makes things easier but having to store files in my Windows user directory is not the wave.

So I need to resume my previous activity of watching a video tutorial on how to get up & running with Vagrant & VCCW with WSL. 

Video: https://www.youtube.com/watch?v=W6Yp9PO7mr0

I manually added these settings to my `.bashrc` file so I don't need to type the command in each time. Lets see if it actually works. 

```bash
export PATH="$PATH:/mnt/c/Program Files/Oracle/VirtualBox"
export VAGRANT_WSL_ENABLE_WINDOWS_ACCESS="1"
export VAGRANT_WSL_WINDOWS_ACCESS_USER_HOME_PATH="/mnt/c/vvv" # this is modified home path because vagrant will fail if commands run in a directory is not the actual home directory
```

I think I'll try this again to set up the project I'm trying to set up.

I'm going through the steps for setting up vagrant with the help of some scripts again. Will recap at some point. 

## Entry No. 007
**Friday 11/1/2019**

So I'm working on my iTunes-sync script.

Back up: I never got around to finishing the migration of my site to a new host because the host is having issues with my SSL. 

Now back to the iTunes sync script. Access my project here:

I store my iTunes library on MyCloud so in order to run a script that can copy my library XML file, I'll need to have access to this Network Storage Device from the commandline. I can do that by mounting, which WSL apparently enables but I kept running into issues, which I figured out were a result of me only referencing my actual server and not the actual directory on the server.

The commands for mounting are:
```bash
sudo mkdir /mnt/music-library
sudo mount -t drvfs '\\server\myMusicCollection' /mnt/music-library # the issues I ran into occured when I only used \\server without adding the actual directory
```

I think created a symlink my home directory like this `ln -sf /mnt/music-library ~/music`.


New commands I've learned during this process:
```bash
sudo mount -a
mount -l # lists out the mounted drives with their "metadata"
```

Other important things worth noting: apparently, you're now able to access linux files from the Windows Explorer using this command in the HOME directory: `explorer.exe .`. And apparently you can manipulate the Linux files from Windows. Yes, my mind is blown now. More details [here](https://www.thurrott.com/windows/windows-10/199652/windows-10s-file-explorer-will-soon-let-you-access-your-linux-subsystem-files)

Anyway, what is next? I need to create a script that copies the file I have in my main library to a new location. 

The command I'm starting with is simple `cp itunes/"iTunes Library.xml" itunes/library-itunes12/`. I looked into other options like `rsync` and whether there are benefits to use that. I'd say, it doesn't seem like an issue to keep using `cp`. I did notice the program lagged while copying but it is a large file.

What I might also implement is a way to copy over the existing itunes12 library to the "Previous Libraries" folder as a backup. I think the library does that already, but it doesn't hurt to do it again :-). 

## Entry No. 006
**Thursday 10/31/2019**

Why does it feel like it's been so long since I did anything?? Today I'm migrating my blog to a new host, so mostly admin stuff. But decided to put together a easy breezy cheatsheet I can use whenever I have to do this, which is not often but sometimes you need to switch hosts.


## Entry No. 005
**Tuesday 10/22/2019**

Today I decided to read up on Jamstack. I don't think there are a lot of good explanations or articles making enough distinctions between it and other options. But I found some interesting stuff:
- https://itnext.io/why-building-with-a-jamstack-is-awesome-39696e9ef8d6
- https://bejamas.io/blog/jamstack/

My dive into JAMstack then led me into an exploration of __headless CMSs__. I'm interested enough to explore it for a project at some point. Sounds like it would allow you to maintain content the same way, using the admin dashboard & whatnot, but then I could use Nunjucks templating (or something else) to create layouts and render without being tied to the PHP templating options.

## Entry #004
**Monday 10/21/2019**
Ok I'm giving vagrant a spin, for real this time.

The issue I'm having right now is the `vagrant-hostsupdator` package won't install. I'm getting this error:  `timed out (https://gems.hashicorp.com/specs.4.8.gz)`

Found some issues on GH related to it: https://github.com/hashicorp/vagrant/issues/8795 but nothing to help me work around the issue. Luckily this is optional. So I'll keep it moving. Picking up where I left off and following this [video](https://www.youtube.com/watch?v=W6Yp9PO7mr0)...

*What I already did:*
- installed VirtualBox
- installed vagrant on Windows & in WSL, using the same version
- tested to see if vagrant was installed with `vagrant -v`. Things are looking good so far.


Following the tutorial, I decided to download the vagrant-wordpress starter scripts from (VCCW)[vccw.cc].
I downloaded those files into my project folder labeled `vagrant-starter`. And that was where I left off before today.


1. I need to modify my `hosts` file to add the IP address found in `default.yml`. I can do that from the command line, using a terminal with elevated Windows privileges: `nano /mnt/c/Windows/System32/drivers/etc/hosts`. No need for `sudo` because Windows does not care about that. 
2. I could also create an alias that would write to the `hosts` file

I ran into some permission issues and recalled this article, so I needed to set some environment variables:
```bash 
#  export PATH="$PATH:/mnt/c/Program Files/Oracle/VirtualBox"
#  export VAGRANT_WSL_ENABLE_WINDOWS_ACCESS="1"
#  export VAGRANT_WSL_WINDOWS_ACCESS_USER_HOME_PATH="/mnt/c/sgdi/vvv"

```

I had to `vagrant halt` and then `vagrant up` and then `vagrant provision` before the wordpress install was successful. Successful meaning the `vagrant up` command would terminate prematurely for reasons I don't know yet and when I checked the project folder, I didn't see any files in the wordpress directory which let me know the install was not successful yet.

Very excited that things worked out. 

Now let's see about configurations, turning this thing on again later this week and making some things with this fancy vagrant box.

## Entry #003
**Friday 10/18/2019**
I actually created a script for updating my hosts file LOL. Why am I like this?? It is here in my [github](https://github.com/shesgottadevelopit/wamp-vhost).

So I guess I can now focus on vagrant and doing all the stuff I did in WAMP in WSL without WAMP. 

Let me start with the WAMP stuff, the process for setting up a site in WAMP is something like this:
- add a vhost (there is a built-in mechanism for this but you can also add it manually) and this typically appears in `C:\wamp_directory\bin\apache\apache2.2.22\conf\extra\httpd-vhosts.conf`
- update host files, which is typically in `C:\windows\System32\drivers\etc\hosts`
- restart services
- the end

The process is a little different for WSL. When I was working on my lil script above about 9 months ago, I found a bunch of other scripts that basically do all the steps I outlined above. So I'm not about to do that exercise again, but I do want to understand whats happening and really walk through all the steps without automation, particularly for the WSL stuff. How does the WSL process differ from WAMP? 

**the hosts files**
in WSL, the host file is a mirror of Windows host file, so I won't need to worry about modifying that file. I'll only need to continue to modify the Windows one, which can be accessed through this path `/mnt/c/windows/System32/drivers/etc/hosts`.

**vhost conf locations & process**
- As for the vhost configuration. Apparently there are two key directories: `/etc/apache2/sites-enabled` and `/etc/apache2/sites-available`. Inside the latter is a `default.conf` file which resembles the `httpd-vhosts.conf` file for the WAMP environment. You would copy that default file and create a new file that will be associated with you new vhost. 
- For example, if we have a project stored in `/mnt/c/myprojects/site1` and we want to create a vhost for that project called `site1.local`. Then we'd created a config file and label it `site1.local.conf`. That file would live in `sites-available`. Inside the config file, we'd add all the important details I included above, like where to find projects files and what you want to refer to this project by. 
- Once you've saved that new file, you'll need to run this command: `sudo a2ensite site1.local.conf` which basically tells enables the new site in the `sites-enabled` directory. 
- Of course you'd need to update the hosts file (which I covered already) and then restart.

These are the scripts that allow you to automate this process and I'm looking forward to using them:
- https://github.com/RoverWire/virtualhost/blob/master/virtualhost.sh
- https://github.com/mattmezza/vhost-creator

This tutorial covers the WordPress part of it and how to integrate wp-cli: https://hellojason.net/blog/how-to-setup-wordpress-locally-on-windows-subsystem-for-linux/

**Final comments**
I tested it out and all works out fine. Things I could probably adjust in the script:
- the userDir
- the IP address being piped into the `hosts` file.

I guess it is time to move on to vagrant for real for real this time. I'll also need to figure out how to launch apache2 and mysql when I open the terminal because I always forget. 

## Entry #002
**Thursday 10/17/2019**
Started watching this tutorial: https://www.youtube.com/watch?v=W6Yp9PO7mr0
When he got to the `default.yml` file updates, I realized I'd need to make changes to the hosts.conf file on Windows and theres no easy way to do that. So I decided to try setting up an apache server via WSL and seeing if I can utilize their `hosts` mechanism instead.

I successfully installed the lamp stack, configured apache, mysql and phpmyadmin. I suppose this would also eliminate WAMP maybe??

I'd need to figure out a way to automate updates to this file: `/mnt/c/Windows/System32/drivers/etc/hosts`. Reading up on solutions: https://www.reddit.com/r/bashonubuntuonwindows/comments/65fav1/syncing_windows_hosts_file_to_etchosts/.

I haven't found a script for adding and removing entries in the host file so I may have to create one or update the one I have using these as inspiration:
- https://gist.github.com/markembling/173887/1824b370be3fe468faceaed5f39b12bad010a417
- https://tomssl.com/2019/04/30/a-better-way-to-add-and-remove-windows-hosts-file-entries/
  
Okay before I log off here is what I've got:
- I can modify the host script from WSL but I'll need to launch my terminal with elevated privileges in Windows to make sure I'm actually able to write the changes when I run the command and/or script. 
- Closest answer my question came from here: https://www.reddit.com/r/bashonubuntuonwindows/comments/9glbro/how_to_manage_administrator_permissions_with_wsl/


## Entry #001
**Wednesday 10/16/2019**
Spent the evening reading up on using vagrant for WordPress development. This way I don't need to worry about conflicts with package versioning, etc.

I installed VirtualBox and also Vagrant but didn't get anything up & running

