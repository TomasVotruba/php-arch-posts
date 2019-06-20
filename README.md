# Preparing Your Magazine Article

Thanks for being interested in writing for php[architect] magazine! Here you will find the guidelines for how to prepare your article for us. As of 2013, php[architect] is now completely written & prepared in Markdown. As a starter, you might want to familiarize yourself with the Markdown standard, and specifically the Pandoc extended Markdown documentation:

* Markdown: <http://daringfireball.net/projects/markdown/syntax>
* Pandoc: <http://johnmacfarlane.net/pandoc/README.html#pandocs-markdown>

However, we have some more strict guidelines on exactly how the Markdown is submitted to us, so read on for a basic primer here on some basics and then some specific formatting that our software expects to see.

## General Rules of Thumb

Markdown as a general language supports the inclusion of raw HTML tags, but for our purposes we don't allow them. If there is anything you want to do that normally you'd use HTML for instead of a Markdown native, take a look back at this document and/or pandoc's documents.  There will be another way.

Also note that there are a number of ways to do the same thing in Markdown.  Headers can be made in 3 different ways, lists in a couple of different ways, and highlighting & code blocks in other ways.   It's OK for you to use whatever Markdown/Pandoc will parse, but we will give some examples below of the format that we prefer if you don't have your own preference.  As it makes it cleaner on our copy-editors.

Finally, you should be able to render your article in any Markdown editors that you wish to check if what you are creating looks right. If you are having any issues with a character getting interpreted as Markdown that shouldn't be, you can escape it with a backslash (\).

## Basic Markdown

### Paragraphs

Paragraphs of text in Markdown are simply represented by a blank line:

~~~
My first paragraph

My second paragraph which
happens to run on for a few lines

My third paragraph
~~~

### Headings

Headings are allowed at 5 separate levels (But please try to refrain from using that many; 2-3 should be plenty for a typical article.) They should be formatted as such:

~~~
# Top level heading - Used for your article title only
## Second level heading
### Third level heading
#### You get the idea
##### That wraps it up.
~~~

### Emphasis

There are a number of ways that you can show emphasis in text in Markdown by using bold or italics. These are created by surrounding the text in question with some symbols. While there are various options in markdown for doing this, we prefer that you use `_` for italics and `**` for bold as it makes for very easy reading:

~~~
The following word is in _italics_; however, 
**this whole phrase is bold**
~~~

### URLs

Because the magazine is designed for use in potentially offline situations, no live links should be created that only refer to text. Any URL should be shown and surrounded with `<>` to mark it as such:

~~~
For more information on PHP see: <http://php.net/>
~~~

### Lists

There are multiple kinds of lists that you might want to create in your Markdown. The most common of these are ordered and unordered lists. Unordered lists are created by starting any number of lines with `*`, `+`, or `-`. Sub levels are created by indenting again by at least 4 spaces. Ordered lists work similarly, but you simply use `1.` instead. You can use any number that you wish on the ordered lists, it will be automatically turned into live numbers for you:

~~~
* This is an unordered list
* With multiple items
    * And a second level
        * And now a 3rd
* That's enough
~~~

~~~
1. This is an ordered list
2. You can enter the numbers in order
3. So that it visually looks good.
1. Or just keep entering 1 each time
1. Knowing it will do the right count for you.
~~~

### Monospace (inline code)

If you have any code that you are including in the middle of your text (as opposed to as separate listings/examples), then you can just surround it with a backtick `\``

~~~
So to count the number of characters in a string 
the `strlen()` function should be employed.
~~~

### Code Examples

Where you have code examples that you want to render inline as a separate paragraph—perhaps because you are going to directly reference them in the flow of your text—you can include them by surrounding the block of code above and below with `~~~~`. If you choose to indent your code, it should be indented at either 3 or 4 spaces (no tabs). Code entered as an example this way needs to be no longer than 60 characters long on each line and at most 8 lines long. If you need a longer code listing, see below.

```
So in the following code, you see that we generate an 
anonymous function with a closure:

~~~~
$function = function($x) use ($y) { return $x * $y; }
$result = $function($a);
~~~~

This allows us great power in accessing variables on the fly 
in the proper scope.
```

You can specify the language (for syntax highlighting) for a code snippet by including a `{.php}` when opening the code block. Pandoc recognizes a wide variety of languages, typically whatever extension you'd use to save a file will work. If not, it'll safely render as plain text. 

```
~~~~{.php}
$function = function($x) use ($y) { return $x * $y; }
$result = $function($a);
~~~~
```

### Code Listings

If you need to provide longer code listings, they can be included as separate entries. These should be saved into a separate `.php` file unique to each code listing, such as `listing1.php`. You can use alsmost any file extension here, to indicate the language, ie. `listing2.html`, `listing3.js`, etc. Code inside of this separate file should be formatted the same way (60 characters per line, indented consistently 3 spaces). These code listings should be approximately no more than 100 lines long. In the PDF magazine they will be rendered in a sidebar. In the ePub/Mobi versions, they will be rendered inline but shown slightly differently than inline code. To use these, reference the code listing in your text as "Listing 1" (or another appropriate phrase), and then insert the special markdown link shown below. This can occur wherever you feel it is best for your code listing to flow into the document. NOTE: Longer code listings are allowed but will not be rendered inline and shouldn't be referenced from your article other than in passing. These will be instead included in the downloadable Code Package for that month's issue.

```
So as you can see in Listing 1, it's possible to generate an
entire webserver with only 12 lines of code, by using this
special technique we've been discussing.

[Listing 1](listings/listing1.php)

Now moving on to our next topic ...
```

### Images & Figures

Similar to how you include code listings, there is a feature that allows you to include figures in your articles. Save these into a figures subdirectory, and name them `figure1.png` or accordingly. These should be in `png`, `jpg`, or `gi`f format, and of high enough resolution for print output and for display on any modern screen. Typically minimum width of 800px is good. Reference these in similar fashion to the Code Listings, mentioning them in your text, but then using similar code to inject them where you feel they will fit best. NOTE: It's possible to include a description of your figure if you wish, but not necessary.

```
After the user enters their password they will be
presented a screen as shown in Figure 2, which allows
them to accept the Terms of Use for the website.

![Figure 2: Terms of Use](figures/figures2.png)
```

### Other Features

There are a number of other features such as definition lists, tables, and more that are possible. If you feel the need to use any of these to better get your point across, please contact us in advice for guidance.

### Building your Article

So far we've discussed the overall Markdown language as php[architect] uses it, but we haven't actually discussed how to assemble your article for submission to us. Let's remedy that now. First of all, note that all files that you send to us should be saved as plain-text UTF-8 files. You should submit to us a .zip or .tar.gz file containing a full directory structure of files that together make up your article. The internal format of this should look something similar to:

```
article.zip
  ├─ bio.markdown 
  ├─ page.markdown 
  ├─ requirements.markdown 
  ├─ notes.txt
  ├─ figures
  │    ├─ figure1.png
  │    └─ figure2.png
  └─ listings
       ├─ listing1.txt
       └─ listing2.txt
```

The various files here should be formatted to include the appropriate pieces of information about your article. The figures and listings directories have already been explained above. The other files each in turn should be:

#### bio.markdown

This should contain a one paragraph, short bio for you the author. It should also be formatted to the following specifications using an h3 and a blockquote:

```
> ### Biography
> Jane Smith is a rolling stone, having worked with many
programming languages before finding her home in PHP.
```

### page.markdown

This is the main file for your article. It will include the entire article, formatted as you wish with Markdown and following the above formatting guidelines. The beginning of the file should start with a level 1 heading with the title of your article, followed directly by a level 6 heading that is your byline (your name). After that the next paragraph should be offset as a block quote, and be a one paragraph (100 words max) abstract of your article explaining what it will discuss in the coming pages. Therefore an example file would look like:

```
# Using closures in PHP
###### by Jane Smith

> Closures are a fairly new feature built into PHP in
the most recent releases, and give amazing flexibility
in your coding. We will evaluate the benefits of
closures as well as how they can complicate your code
as well.

Some more text inserted here.

## Introduction

Something about how great closures are …
```

####requirements.markdown

This is an optional file, but if it exists can have 3 separate sections, each with a level 3 heading and an unordered list of items. These sections are 'Requirements' (To explain what versions of PHP and libraries you need to use the article), 'Other Software' (Any other software that you might need), and 'Related URLs' (to provide links off for more information). Such as:

```
### Requirements:
- PHP: 5.4+

### Other Software:
- MySQL 5.0+

### Related URLs:
- MySQL – <http://www.mysql.com/>
- PECL – <http://pecl.php.net/pdo>
```

### notes.txt

The notes file is again optional, and simply should contain anything that you might want to call to our attention. Perhaps some specific formatting suggestions. One thing in particular that should be brought out here, are any specific phrases from your article that you feel would be good callouts. That is to say, a phrase that would be good to be shown pulled out in a highlight box from the text.

```
Please make sure that Listing 2 shows up near all 
3 paragraphs that refer to it. Also the whitespace
indenting on code Listing 4 is extremely important.

For callouts consider using:
"...the beauty of these closures is their flexibility..."
"That's when I fell in love with PHP."
```

## Submitting Your Finished Article

Once your article is complete, just zip it up into a single file for us and email it to your editor. (If you aren't sure who you should contact, then <editors@phparch.com"> always works) But most importantly just remember:

Don't Panic!

If any of these guidelines seem too complex, or if you get mixed up on how the formatting should be handled, don't panic! Your editor is here to help. Don't get too hung up on formatting; these guidelines are intended to smooth the editorial process and final layout, but we're much more concerned about getting informative text from you, the expert, than on having it formatted perfectly.

If you have any issues we'll be happy to help you out, and then share the final results back with you so that you can see how we'd like things submitted in future articles from you!