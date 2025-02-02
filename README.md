# Markdown Resume Generator [![Build Status](https://travis-ci.org/there4/markdown-resume.png?branch=master)](https://travis-ci.org/there4/markdown-resume)[![nodesource/node](http://dockeri.co/image/there4/markdown-resume)](https://registry.hub.docker.com/u/there4/markdown-resume/)

> Convert markdown to HTML and PDF resumes

Turn a simple Markdown document into an elegant resume with both a perfect
pdf printable format, and a responsive css3 html5 file. You can view a sample
at the [blog post for the project][blog], or look in examples/output to see sample PDFs.

## Features

* Multiple styles to choose from: `modern`, `blockish`, `unstyled`, `readable`, `swissen` _(Fork and add more!)_
* PDF generation via [wkhtmltopdf][wkhtmltopdf]
* Responsive design for multiple device viewport sizes
* Simple Markdown formatting
* Single file deployment (no external stylesheets)
* You can now version control and branch your resume.

## Installation

### Docker

Run those commands in the directory where you put your markdown resume.

#### Oneshot command

This is best suited for use in scripts or in CI environments:

`docker run -v ${PWD}:/resume there4/markdown-resume md2resume [options] command [arguments]`

#### Interactive console

This allows you to enter an interactive console where you can easily experiment and run different commands:

`docker run -it -v ${PWD}:/resume there4/markdown-resume`

### Local

1. Clone the repo `git clone git@github.com:there4/markdown-resume.git` or [Download ZIP](https://github.com/there4/markdown-resume/archive/master.zip)
2. **PHP 7** and **[composer](https://getcomposer.org/download/)** are installed and on your PATH
3. `composer install` inside of the project directory to install dependencies

4. For generating PDF files, you need to install `wkhtmltopdf`
    * OSX: `brew cask install wkhtmltopdf` via [Homebrew Cask](https://caskroom.github.io/)
    * Debian: `sudo apt install php7.0-mbstring wkhtmltopdf`
    * Fedora `sudo dnf install php-mbstring wkhtmltopdf`

## Usage

The two most important commands are the following two. Run them
inside the cloned directory

```bash
./bin/md2resume html examples/source/sample.md examples/output/
./bin/md2resume pdf examples/source/sample.md examples/output/
```

## Help

```
Markdown Resume Generator version 2.3.0 by Craig Davis

Usage:
  [options] command [arguments]

Options:
  --help           -h Display this help message.
  --quiet          -q Do not output any message.
  --verbose        -v|vv|vvv Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
  --version        -V Display this application version.
  --ansi              Force ANSI output.
  --no-ansi           Disable ANSI output.
  --no-interaction -n Do not ask any interactive question.

Available commands:
  help        Displays help for a command
  html        Generate an HTML resume from a markdown file
  list        Lists commands
  pdf         Generate a PDF from a markdown file
  stats       Generate a word frequency analysis of your resume
  templates   List available templates
  version     Show current version information

```

## Examples

Choose a template with the -t option.

```bash
./bin/md2resume html --template blockish examples/source/sample.md examples/output/
```

If you want to edit your markdown resume in your editor while watching it
update in your browser, run this command:

```bash
watch ./bin/md2resume html --refresh yes --template modern examples/source/sample.md examples/output/
```

This makes the build script run periodically, and html document will refresh
every two seconds via a meta tag. Open the `./examples/ouput/sample.html` file
in your browser, and then just save your markdown document when you want to see
a fresh preview.

Adding a profile picture (for now only added to the `readable` template):

```shell
./bin/md2resume html --template readable --profile_picture photo.png test.md output/
```

## Authoring Your Resume

Markdown is limited to basic html markup. Follow the `examples/source/sample.md`
file  as a guideline. This file includes various headers and several nested
elements. This allows us to construct a semantic HTML document for the resume,
and then use CSS rules to display a nicely formatted resume. Note that because
we have very few ways to nest or identify elements that many of the css rules
are based on descendant and adjacent selectors.

## Feature Development

In order to add new commands, you'll need to first install the dependencies via `composer install`

After that, you can run the `md2resume_dev.php` file from the command line.

## Building a Release

1. Tag the repo with the new build number.
2. Run `composer build`.
3. Push both the tag and the code.

## Acknowledgments

The initial inspiration is from the [Sample Resume Template][srt].
However, no HTML from that project has been used in this. General layout has
been reused, and media queries have been added. It's a nice template, and if you
are a more comfortable with html than markdown, you should use it.

## Changelog

* __2.3.1__ : Fix embedded images in PDF generation with Docker  [@danielklim](https://github.com/danielklim)
* __2.3.0__ : Add Docker support to ease the installation process  [@spawnia](https://github.com/spawnia)
* __2.2.0__ : Dropped phar file distribution, removed Pake and migrated to composer commands
* __2.1.0__ : Dropped PHP5 support
* __2.0.12__ : Added new `Roboto` template from [@ejwaibel](https://github.com/ejwaibel)
* __2.0.10__ : Updated spacing in moder template with commites from [@501st-alpha1](https://github.com/501st-alpha1)
* __2.0.9__ : Updated Modern template with improved spacing. Update parsing of
  `--template` option to close [issue #7](https://github.com/there4/markdown-resume/issues/7)
* __2.0.8__ : New `readable` theme contributed by @ahmadnazir, minor refactor
  to support a /links directory
* __2.0.7__ : Update composer to use `sunra/php-simple-html-dom-parser` this
  appears to be better maintained and more popular to [close #27](https://github.com/there4/markdown-resume/issues/27)
* __2.0.6__ : Fix empty template list from phar file to [close #24](https://github.com/there4/markdown-resume/issues/24)
* __2.0.5__ : Remove default value for the `--refresh` option to [close #22](https://github.com/there4/markdown-resume/issues/22)
* __2.0.4__ : Fix path resolution problem with absolute paths to [close #16](https://github.com/there4/markdown-resume/issues/16)
* __2.0.3__ : Add optional duration to the `--refresh` option to [close #15](https://github.com/there4/markdown-resume/issues/15)
* __2.0.2__ : Add new dependency check for `mbstring` to [close #20](https://github.com/there4/markdown-resume/issues/20)
* __2.0.1__ : Add new `swissen` template with Helvetica styling [@beautifulcode](https://github.com/beautifulcode)
* __2.0.0__ : Complete rewrite with the [symfony console component][console].
  Deployment is now done with a compiled phar file, and development dependencies
  are managed with composer.
* __0.9.0__ : Add composer and update README with new changelog
* __0.8.8__ : Add Chinese text example [@ishitcno1](https://github.com/ishitcno1)
* __0.8.7__ : Update pdf formatting of the modern template [@roleary](https://github.com/roleary)
* __0.8.6__ : Fix output path [@abhikandoi2000](https://github.com/abhikandoi2000)
* __0.8.5__ : Fix [issue #2](https://github.com/there4/markdown-resume/issues/2)
* __0.8.4__ : Correct chmod and add parameter for output directory [@kevinxucs](https://github.com/kevinxucs)
* __0.8.2__ : Update build script and add refresh command option
* __0.8.1__ : Updating formatting of initial templates
* __0.8__ : Initial Release to Public

[srt]: http://sampleresumetemplate.net/ "A great starting point"
[blog]: http://there4development.com/blog/2012/12/31/markdown-resume-builder/
[pake]: https://github.com/indeyets/pake/wiki/Installing-Pake
[wkhtmltopdf]: https://github.com/pdfkit/pdfkit/wiki/Installing-WKHTMLTOPDF
[console]: http://symfony.com/doc/current/components/console/introduction.html
