# ELR WordPress Style Guide

Adapted from: [http://wp.smashingmagazine.com/2012/07/19/guide-wordpress-coding-standards/](http://wp.smashingmagazine.com/2012/07/19/guide-wordpress-coding-standards/)

### Code Formatting

+ The PHP parser doesn’t care how you format your code, so why should you? In reality, the format of your code makes a huge difference in every way imaginable.

### WHY CODE FORMATTING MATTERS

+ Even if you’re working on a pet project, the format of your code says a lot. And if you’re in a multi-developer environment, it speaks volumes. Code that is well formatted and well thought out shows quality (even if it isn’t good), while chaos begets sloppy programming (even if it is genius).

+ Here are but a few reasons to pay attention to the format of your code:

+ Well-formed code is easier to maintain. You might know what’s going on today, but what about a year from now? Taking the time to give structure to your work will save you eons of time later on (… well, maybe not eons).

+ Other developers do not share your brain, so they won’t understand your chaotic code, or they would need a long time to untangle it. Ensuring as little friction in communication as possible is in the project’s best interest, and this can be facilitated by standards-compliant formatting.

+ Slightly less importantly, someone who is learning to program should be able to visit a website and learn something by looking at the source code. Standards usually have an inherent logic, so an onlooker would be able to figure out what’s going on. Adhering to standards could help a lot of budding developers learn programming the right way from day one.
In many cases, good formatting helps maintainability. Many standards require you to space out if statements and other blocks of code. Not crowding the code together will make an “Error on line 267” message much easier to fix.

### PHP IN WORDPRESS

+ Line breaks

    + WordPress’ documentation says nothing in particular about line breaks, but adding a line break after most statements is common practice. Variable definitions, if blocks, array items and so on should be on separate lines.

            $my_value = 'Me';
            $your_value = 'You';
            $their_value = 'Them';

            if ( $my_value == 'You' ) {
                echo 'It seems like you are mixed up with me';
            }

+ Indentation

    + Indent code to show a logical structure. The goal here is readability, so any indentation that makes the code more readable is a good practice. Use tabs at the beginning of lines, and use spaces for mid-line indentation.

            $arguments = array(
                    'mythoughts' => array(
                    'guitars' => 'I love guitars',
                    'applepie' => 'Apple Pie is awesome'
                ),
                    'yourthoughts' => array(
                    'guitars' => 'Meh',
                    'applepie' => 'Love it!'
                )
            );

            if( have_posts() ) {
                while( have_posts() ) {
                    get_template_part( 'template', 'blogpost' );
                }
            }

+ Space usage

    + Remove all trailing spaces from line endings. Empty lines with tabbed or non-breaking spaces is also common — remove these as well. But use spaces to make your code readable, most commonly within parentheses. Insert a break after an opening brace and before a closing brace, except when typecasting.

            $number = (integer) $_GET['number'];
            if( $number === 4 ) {
                echo 'You asked for a four!';
            }

+ Quotes

    + The main rule in the WordPress Codex is to use single quotes when you are not evaluating anything inside a string. If you need to use quotes inside a string, just alternate. Escaping quotes is allowed, of course, but you should rarely need to do so.

            $name = 'Daniel';
            $hello = "My name is '$name'";

+ Braces

    + The easiest method is to always use braces. The standards allow for the omission of braces for single-line if statements but only if there are no multi-line blocks in the same logical structure. Omitting braces is not allowed for single-line loops, though. I find this standard too convoluted — just always requiring braces would be much simpler. In addition, the standards dictate that an opening brace should be put on the same line as the initial statement, not on the line below (as specified in the PHP documentation).

            // The usual style
            if( have_posts() ) {
                the_post();
                the_content();
            }
            else {
                echo 'Steal ALL the posts!';
            }

            // Leaving out braces in this case is allowed.
            if( ! has_post_thumbnail() )
                echo 'This post does not have a featured image';

            // But putting them in looks nicer and is more consistent.

            if( has_post_thumbnail() ) {
                the_post_thumbnail();
            }

+ Formatting SQL queries

    + SQL query keywords must be capitalized, and complex queries should be broken into multiple lines. One must know a lot about queries before using them, especially regarding their security; we’ll cover them further down.

            $simple_query = "SELECT * FROM $wpdb->posts WHERE comment_count > 3 LIMIT 0, 10";

            $complex_query = "
            SELECT * FROM $wpdb->posts WHERE
            post_status = publish AND
            comment_count > 5 AND
            post_type = 'post' AND
            ID IN ( SELECT object_id FROM $wpdb->term_relationships WHERE
            term_taxonomy_id = 4 )
            ";

+ Naming conventions

    + Never use CamelCase for names in WordPress code. Functions may contain only lowercase characters, separated by underscores if needed. Capitalize the first letter of each word in a class name, and separate words with underscores.

    + File names should all be lowercase, with hyphens separating the parts of the name. If a file contains a single class, then name it after the class, prefixed by class-.

    + Use string values for function arguments instead of booleans to make your code more obvious.

            $event = new My_Event();
            $event->save_event_to_file( 'event-file.txt', 'noformatting' );

    + By far the most important rule is to make names self-explanatory. Remember that you are in a collaborative environment, and one of your goals is to help everyone understand what your code is doing.

+ Comparison Statements

    + One great practice, and not just for WordPress, is to always write a variable in a comparison on the right side. Thus, if you forget an equal sign, the parser will throw an error instead of evaluating to true.

            if( 3 == $my_number ) {
                echo 'BINGO!';
            }

    + If you prefer to use ternary operators, the standards allow you to do so but advise that you always check for truth to make things clearer. One exception mentioned is when checking for nonempty variables, ! empty().

+ Overview

    + The main takeaway from this section is to favor clarity and readability over brevity and cleverness. If you forget to follow some spacing rules or you are bent on inserting line breaks before opening braces, you’ll be fine as long as the code is easily understandable.

### FORMATTING HTML

+ The WordPress Codex states that all HTML code must be validated using the W3C Validator. Take care, because valid code isn’t necessarily good code, although there is a definite correlation.

+ Doctype

    + WordPress is based on the XHTML 1.0 specification, which the W3C recommended way back in 2000.

    + A quick look at the Twenty Eleven theme shows that, despite the W3C’s recommendation, WordPress uses HTML5 for this default theme. There seems to be a conflict here, but in reality there is none. HTML5 includes a section on XML serialization, which effectively means that “XHTML5” can be used.

+ Using quotes

    + Quotes are mostly used when placing attributes and their values. You are free to use single or double quotes. Be consistent, though. While I prefer the look of double quotes (although I have no idea why), I use single quotes where possible in HTML. My reasoning is that because single quotes are required in PHP, I might as well follow suit in HTML.

    + By following this methodology, I am able to see whether something “special” is going on in a line just by looking at the quotes.

+ Closing tags

    + The XHTML specification requires that you close all tags. Void (or self-closing) elements must be closed by adding a forward slash just before the last angled bracket. Take care because exactly one space must precede the forward slash, according to the official specification.

+ Indentation

    + The rules for indenting HTML match the rules for indenting PHP. Strive for a logical structure with your indentation. When mixing PHP and HTML, the blocks of PHP should be indented according to the normal flow of indentation.

            <div class='<?php post_class() ?>'>
            <h1><?php the_title() ?></h1>
            <?php if ( has_post_thumbnail() ) : ?>
            <strong>Featured Image</strong>
            <?php the_post_thumbnail() ?>
            <?php endif ?>
            </div>

### FORMATTING CSS

+ Consistent styling is just as important in CSS as in PHP and HTML. When a user wants to change a small detail in your theme, they will inevitably end up in a CSS file. Thus, the CSS could be the most visible code that you write. The “CSS Standards” document is a “rough draft.” Most of what’s there is probably there to stay, but as stated on the page itself, it is all subject to change.

+ Follow the draft closely. If something changes, you’ll still be up to speed on most of the guidelines; and if your existing CSS code doesn’t adhere to it 100%, the reason will be understandable.

+ Indentation and structure

    + Your CSS should follow this rough schema:

            CSSselector {
                property: value;
                property: value;
            }
            selector,
            selector,
            selector {
                property: value;
                property: value;
            }

    + Write each selector on a separate line, even if you are listing multiple selectors for a ruleset. Also, each property-value pair should sit on its own line. Put the opening brace on the selector’s line, and put the closing brace on a separate line with the same indentation as the opening selector’s.

+ Naming conventions

    + Use lowercase characters only.

    + Separate words within a selector with a hyphen.

    + Give your selectors human-readable names.

+ Properties and values

    + There are quite a few rules for writing properties and values. It can seem a bit over the top, but you get used to it very quickly, and it really does help everyone understand each other’s code.

    + Use shorthand versions of properties wherever possible, except when overwriting a previously defined property.

    + Use lowercase HEX code for colors wherever possible. If appropriate, use the shorter version.

    + Insert a space after the colon following a property.

    + Always use lowercase characters, except when an uppercase character is required, such as with font names and vendor-specific properties.

    + Organize CSS properties alphabetically, with the exception vendor-specific properties, which should always precede their general counterpart, and dimensional properties, which should be grouped together. If width and height are specified, write the width first.

            .button {
                background: #34c1ff;
                -moz-border-radius: 5px;
                -webkit-border-radius: 5px;
                border-radius: 5px;
                color: #fff;
                margin: 11px;
                position:relative;
                left:5px;
                top: 5px;
                width:120px;
                height:22px;
            }

+ Commenting

    + CSS supports only one type of commenting — block style; it does not have a separate notation for inline comments. Write short comments on one line, without a line break below. For comments that span multiple lines, insert a line break just after the opening syntax and a line break just before the closing syntax.

            /* Default link style /*
            a {
                color: #ff9900;
            }

            /*

             */
            Some other quick link styles
            so that users can easily use
            whatever they need

            */

            a.prominent {…
            If you use comments to delineate sections of the code, then use the following notation:
            a {
                background: #efefef;
            }

            */ Post Content Styling
            --------------------------------------------------- */

            .post-content {
                padding: 22px;
            }

+ Using CSS preprocessors

    + Using CSS preprocessors such as SASS and Less makes our lives as developers a lot easier, but they are not without drawbacks. The code produced by these tools is usually valid but cannot be said to be very clean. A style sheet produced manually (and thoughtfully) will be much more readable than one produced automatically by Less.

    + It depends on what you’re doing. If your product is commercial, then the ultimate goal is a good user experience, with valid and optimized code. In this case, use the output of the preprocessor as the main CSS, but include the original file for developers. While your CSS will not conform to WordPress’ standards, including the original file bridges the gap somewhat until WordPress takes an official position.

    + Sacrificing CSS coding standards in order to simplify the development process (with the goal of a better user experience) is OK. Sacrificing the validity of code is not.

+ Other languages

    + There is no official documentation for dealing with other languages, but spotting a pattern here isn’t difficult. Aim for legible, well-structured and clear code. Look to the official documentation and community best practices for the given language. When WordPress takes a position, they will most likely do the same.

+ General Development Guidelines

    + Your WordPress product, whether a theme or plugin, must be coded in a certain way if you intend to publish it. In this chapter, we’ll look at some requirements of themes and plugins without which you wouldn’t be able to create a quality product.

### INFORMATION AND DOCUMENTATION

+ Themes and plugins alike come with a bunch of information. A project usually contains four types of information:

    + Information about the theme or plugin itself;

    + Additional information that the author wants to share about the project or themselves;

    + Inline code documentation (the Codex has a guide for this);

    + Separate documentation for end users.

### USING HOOKS

+ The backbone of WordPress development is the hooks API. This great method of programming not only allows for WordPress to be easily extended but ensures that developers don’t have to touch the core code. Using hooks as much as possible instead of writing custom code promotes modularity and simplicity, while decreasing code duplication.

+ More often than not, achieving something in WordPress feels harder than it should be. Want to change the length of the excerpt? Look at the excerpt_more hook. Want to modify the content of the email that users get when they forget their password? Check out the retrieve_password_message hook.

+ Whenever you’re working on something, do a quick Google search or scan Adam Brown’s hooks database for the relevant hook.

+ If your product is fairly complex, try creating hooks of your own. These would enable others to easily extend your product, and you could use them yourself to make the product more modular.

+ For an extensive overview, look at our “Complete Guide to WordPress Hooks.” And in the section on plugins and themes further below, we’ll cover some more tips on particular hooks.

### SECURITY

+ It goes without saying that your product should take advantage of all of the security features of WordPress.

+ This includes (but is not limited to) the following:

    + Use nonces to verify user identity and intent.

    + Escape and prepare SQL statements.

    + Sanitize and validate user input.

    + Use roles and capabilities to make sure users may do what they are doing.

    + Funnel AJAX requests to ajax-admin.php, and use hooks to handle these requests.

    + To learn more about WordPress security in general, look at “Securing Your WordPress Website.”

    + To learn more about database security and about making your SQL queries airtight, give “Interacting With the WordPress Database” a read.

### PRIVACY

+ Always respect the privacy of your users. WordPress does not allow you to create extensions that “phone home.” If you do want to collect user information, then you must use an opt-in method whereby users are made aware of what is happening and explicitly give you permission. The guidelines don’t allow for any hotlinking of bundled resources. Any resource you use must be bundled with your product. API type calls are acceptable, though.

### PLAYING NICE WITH OTHERS

+ Too often do I see two plugins that are incompatible (i.e. completely unrelated in their function) or plugins that are incompatible with themes. While this is sometimes unavoidable, in many cases it can be chalked up to bad development.
One way to maximize the compatibility of your product is to use as many WordPress defaults and options as possible.

+ Don’t write your own pagination code; WordPress has perfectly good functionality available in paginate_links(). Don’t use a separate or bleeding-edge version of jQuery when one is already available in WordPress by enqueueing it with wp_enqueue_script().

### TESTING

+ The robustness of your product is your responsibility. Your code should undergo rigorous testing by at least yourself (the more, the merrier, though). Many developers follow test-driven development (TDD), which aims to minimize the number of errors that pop up. Look at “Writing Unit Tests for WordPress Plugins” for a detailed tutorial on how to start.

### MAINTENANCE

+ If you build something for the WordPress community, you should also maintain it. This does not have to tie you down for eight hours a day. If you feel that you don’t want to work on your project anymore, then try to hand it over to someone, or simply state that the product is no longer being maintained. As long as you don’t keep users in the dark, you should be fine.

+ If you are actively working on it, then include changelogs and development information with the product. This will help users keep up with the changes, and it will be a good reference for you as well.

### LICENSING

+ The license you are required to use depends on the type of product you are developing. To submit your theme or plugin to the WordPress repository, you must use a GPL-compatible license. This effectively means that your work must be free because all non-free licenses are automatically not GPL. Be sure to state the license clearly in your product.

+ If your product is commercial, then you may use any software license you wish. If you are selling through a marketplace, then read its documentation to see what licenses it accepts.

+ You may not, of course, use any resources that you do not own or do not have permission to use. If you are using a free resource under an attribution license, then you must include the attribution in your work.

+ If you are looking for some GPL-compatable icon sets, the “Theme Review” document links to a fair number of them.

### Theme Development Best Practices

+ There is a long list of rules, guidelines and best practices that you need to adhere to when developing a WordPress theme. Most of them are logical, and all serve a purpose. We’ll cover the most important bits below, and a complete list can be found in the “Theme Review” document. You can evaluate your theme’s adherence to most of these rules with the Theme Check plugin.

### ERRORS AND FUNCTIONALITY

+ Your theme must pass five levels of rules and guidelines:

+ Your theme may not generate any PHP warnings, errors, notices or validation errors for HTML, CSS or JavaScript.

+ Your theme may not generate any WordPress-generated errors or notices.

+ All required WordPress features, functions and code elements must be built in, and your theme must support WordPress’ default implementation of these features.

+ If implemented, the recommended features must work according to the specification.

+ Optional functionality must work according to the specification.

### INCLUDED FEATURES

+ As mentioned, some features are required, some are recommended and some are optional. The current “Theme Review” document breaks them down as follows.

+ Required features:

    + Automatic feed links

    + Widgets

    + Comments

+ Recommended features:

    + Navigation menus

    + Post thumbnails

    + Custom header

    + Custom background

    + Custom visual editor style

+ Optional features:

    + Internationalization

    + Each feature above has one or more functions that your theme must contain. To view the complete list, see the relevant section in “Theme Review.”

### HOOKS AND TEMPLATE TAGS

+ Whether required or not, any template tag or hook you use must be implemented properly.

+ The following eight items are currently required for each and every theme you make:

        wp_head()
        body_class()
        $content_width
        post_class()
        wp_link_pages()
        paginate_comments_link or previous_comments_link() and next_comments_link()
        posts_nav_link() or previous_posts_link() and next_posts_link() or paginate_link()
        wp_footer()

+ In about 90% of the cases I’ve seen, a plugin won’t work with a theme because the theme is missing the wp_head() or wp_footer() hook.

### INCLUDING FILES AND RESOURCES

+ If a function exists to include a template file, then you are required to use that function, instead of including the file another way.

+ The following templates may be called with the corresponding functions:

    + Call header.php with get_header()

    + Call footer.php with get_footer()

    + Call sidebar.php with get_sidebar()

    + Call comments.php with comments_template()

    + Call searchform.php with get_search_form()

+ If you create additional templates for your theme, then you must call them using the get_template_part() or locate_template() functions (the latter is best used with child themes).

+ When including styles and scripts, you must use wp_enqueue_style() and wp_enqueue_script(), instead of hard-coding them.

+ The only exception is the theme’s style sheet, style.css, which may be added to the head of the document.

### WORDPRESS-DEFINED CSS CLASSES

+ Whenever a page, comment, post or almost any other element is generated, WordPress attaches classes to it so that it can be identified and manipulated. Your style sheet must support some of these classes.

+ Alignment classes:

        .alignleft
        .alignright
        .aligncenter

+ Caption classes:

        .wp-caption
        .wp-caption-text
        .gallery-caption

+ Post classes:

        .sticky

+ Comment classes:

        .bypostauthor

+ If you do not intend to style them differently, then the .sticky and .bypostauthor classes may be left empty, but they must exist in the style sheet nonetheless. This list will probably fatten up over time to account for evolving requirements.

+ Learning about all of the other classes that WordPress applies to various elements is a good idea. This will enable you to create flexible style sheets that you can reuse from project to project.

### THEME FILES

+ The number of files in your theme can vary greatly, depending on how complex the theme is. It could also operate perfectly with just a simple index.php file. The choice is yours. “Theme Review” offers the following guidelines.

+ Required files:

    index.php
    comments.php
    screenshot.png
    style.css

+ Recommended files:

    404.php
    archive.php
    page.php
    search.php
    header.php
    footer.php
    sidebar.php

+ Optional files:

    attachment.php
    author.php
    category.php
    date.php
    editor-style.php
    image.php
    tag.php

+ Remember that you can also create any arbitrary file in your theme’s directory, as well as create your own templates. Give these files names that don’t clash with WordPress’ template hierarchy.

+ For example, don’t create a page-about.php file to include somewhere because, with the way templates are handled, if the user creates a page named “About,” then page-about.php will be used to display it.

### THEME OPTIONS

+ Creating a theme options page is a great way to give users powerful options. WordPress requires that you plan and code this carefully, rather then copying and pasting from a tutorial.

+ You’ll need to follow a number of specific requirements:

    + Always add a theme options page with the add_theme_page() function.

    + Always base permissions on the edit_theme_options capability, rather than on a role or something else.

    + Save all options in a single array; don’t save them as separate key-value pairs in the database.

### THEME NAMES

+ Quite a few rules regulate how you may name a theme. This is understandable because we want to avoid sensationalism and keyword spam.

+ Your theme’s name may not contain any of the following:

    + The word “WordPress”;

    + The word “theme,” or any related word such as “blog,” “template” or “skin”;

    + Version- or markup-related terms (HTML5, CSS3 and so on);

    + Credit to a contributor;

    + Any keyword spam.

### THEME CREDITS

+ We all want to see our name written in huge bold text in the header of a website, but this (thankfully) is not how WordPress or the open-source community works.

+ Credit may be given, of course.

+ Here’s what you may do:

    + You may use the author URI row in your style.css file to link to your personal or professional website.

    + You may use the theme URI row in your style.css file to link to a demonstration of the theme.

    + You may include one link in the theme’s footer. This must be either the author URI or the theme URI that you defined in the style.css file.

    + You may also have a more elaborate section or module for self-promotion, but this must be opt-in.

    + You may not forbid users from removing these links.

    + Above all else, you may not use any of these for spam or for self-promotion unrelated to the given product.

### DOCUMENTATION

+ There are different ways to handle this, but your theme must have some sort of documentation. The recommended method is to include a readme.txt file in your theme that covers all of the information that a user would need to know. It should be in the Markdown format that readme.txt files for plugins use. I also recommend creating more user-friendly documentation in the form of a website, PDF file or the like. I prefer self-contained documentation such as a PDF file because it will remain available to the user no matter what.

+ For a great tutorial, read “How to Improve Your WordPress Plugin’s Readme.txt.” The article applies to plugins, but the Markdown format and general idea are the same for themes.

+ Plugin Development Best Practices

    + WordPress plugins tend to be a bit more complex than themes — not always, of course, but because plugins need to supersede themes, a much broader breadth of knowledge is needed to build a 100% standards-compliant plugin. In addition, plugins span a wider range of themes and skills. From adding different types of avatars to implementing a full-blown event management system, the spectrum is pretty wide.

    + Because of this, the standards and best practices for plugins are dispersed over many pages of the WordPress Codex and the websites of developers. A good place to start is “Plugin Resources,” where you will find information for the most common cases and a few uncommon ones.

### PLUGIN NAMING

+ Plugins may be named whatever you’d like, but obviously it should bear some relevance to what the plugin does. Try to choose a unique name (search the plugin repository beforehand). While not explicitly stated, the WordPress team would probably want you to follow the same rules for naming plugins as for naming themes (refer to the section on themes above).

### PLUGIN FILES

+ Your plugin requires at least a main file with a unique name (i.e. unique across the plugin repository), related to the plugin’s function. A readme.txt file is also required, formatted according to a specific set of rules.

### INFORMATION ABOUT YOUR PLUGIN

+ A bit of information about your plugin is needed. Without it, your plugin wouldn’t be detected in the administration section. While only the “Plugin Name” field needs to be filled in, filling in the other fields will make your plugin look nicer and more complete.

        /*
        Plugin Name: The Missing Task Manager
        Plugin URI: http://tmtm.com
        Description: A simple task manager for your WordPress website
        Version: 1.2
        Author: Good Guy Greg
        Author URI: http://imtheauthor.com
        License: GPL2
        */

+ Authors usually include an extra block in their plugin’s main file about the copyright. This is not required but is recommended for clarity’s sake.

### USING HOOKS

+ We’ve already looked briefly at hooks. Without them, your plugin would be pretty much useless. Use hooks properly and as much as possible, instead of hard-coding things. The rules for themes apply here as well, but need to be taken even more seriously with plugins. The whole purpose of plugins is to work in across themes and across installations; therefore, hard-coding is not acceptable.

+ Also, find the right tag to hook into. Always look in the Codex to determine where to hook your functions. An incorrect hook can wreak havoc.

+ Developers tend to overlook three hooks in particular that would allow them to add great functionality to their plugin. Here they are below.

+ Activation hook

    + Your plugin might need to perform a number of tasks when activated. You might need to add some options, create a database table or do something similar. An easy way to accomplish this is to use the register_activation_hook() function.

+ Deactivation hook

    + The register_deactivation_hook() hook is similar to the activation hook. It runs when a plugin is deactivated and allows you to do some clean-up before the plugin is deactivated.

+ Uninstall hook

    + When a plugin is uninstalled, the register_uninstall_hook() hook can be used to complete some tasks. You should do a thorough clean-up after your plugin has been uninstalled; don’t burden the user with unnecessary data.

+ Stack Exchange has a great tutorial on creating a class that handles all three functions.

    + For more information about hooks, check out the previously mentioned “WordPress Essentials: The Definitive Guide to WordPress Hooks” here on Smashing Magazine.

### HANDLING DATA

+ There are three methods of storing and retrieving data in a plugin:

    + Store website-specific data via the options mechanism;

    + Store post-specific data using the post meta mechanism (i.e. custom fields);

    + Store data not associated directly with the installation or with individual posts in a separate database table.

+ The Options mechanism and Settings API

    + The options mechanism is an easy way to store named pieces of data in the database. This can be used for website-wide options and other relatively static data. The Settings API was introduced in WordPress 2.7 and is basically an evolved version of the options mechanism. Because use of the Settings API will eventually be required, using it instead of the options mechanism is a good idea.

    + Familiarize yourself with all of the options in the Settings API because it provides not only database-interaction wrappers, but also HTML-generating functions to help you automatically manage your settings fields.

+ The post meta mechanism

    + The post meta mechanism provides a convenient way to store data that pertains to a particular post. Its functionality is very similar to that of the options mechanism. It allows you to add, update, delete or get custom fields. Read the Codex for the nuances of usage, but mastering this one should be pretty easy.

+ Creating new database tables

    + This method is definitely suited to more elaborate plugins and more experienced developers. Adding tables and the functionality they usually support brings with it many new hurdles to jump. Make sure to secure the queries to this table just as you do with regular queries.

    + Use the $wpdb class and the functions that it makes available. Refer to the general section on safety above for more information on database security.

### INTERNATIONALIZATION

+ Internationalization is not required but is a good idea if you want to add your plugin to the repository or to sell it. It enables users and developers to add translations to your plugin very easily. Preparing your plugin for internationalization takes some time if you’ve never done it before; it requires third-party tools and edits to the code to accommodate the translatable strings. Your best friend in this venture will be i18n for WordPress Developers.

### OVERVIEW

+ As you can see, the standards and practices for plugins are much vaguer than the ones for themes. Adapt any standards for themes to your plugin as appropriate. More concrete guidelines will be formulated eventually, so you might as well be prepared.

+ Straying From The Standards

    + In theory, you must follow these standards only if you want to submit your theme or plugin to the WordPress repository. In reality, though, you’re best off following these rules anyway. Any serious marketplace will force a lot of them down your throat anyway, and any serious WordPress developer will frown on code that isn’t standards-compliant.

    + The most important reason to follow the standards is to ensure the health of your project. By following the guidelines laid down in the official documentation, you will ensure that your product is as future-proof as possible and that anyone else who comes onboard to help will understand it immediately.

### BENDING THE RULES

+ In some scenarios, bending or breaking the rules is appropriate. Many developers who create commercial themes for large marketplaces, for example, include plugin functionality in their themes. This is a no-no according to the standards, but it makes sense from a business point of view. Enabling the user to get a great-looking customizable website, complete with e-commerce functionality and mailing-list integration, in one simple download (instead of having to download a theme and two different plugins) is a huge plus.

+ If you’re planning to release a Web app, coding it from scratch might take a while, but you could put up a test version based on WordPress quite quickly. In this case, bending a few rules (such as the one about keeping plugins and themes distinct) is acceptable.

+ Many great things have been created by bending the rules; the trick is knowing when to do so. If you have good reason and you document along the way, you should be safe. The key is communication: making sure other developers (and you, later on) understand the reasons for what you’ve done.

### Conclusion

+ Admittedly, this has been a mouthful, so consider yourself awesome and have a slice of pie. If you’ve made it this far, then you know where to look for information on standards, and you understand the logic behind them.
There is a lot more to know about WordPress development, so below is a bunch of links to help you on your path to enlightenment.

+ As with any community-based project, being nice will get you a mile further than acting like a pompous know-it-all. Community members will value your efforts and help out for sure.