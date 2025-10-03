# mediawiki-pages-WikiBook

## Description
A small, ready-to-import MediaWiki package that models a Book with Chapters and Sections. 

The package supports cases where a wiki is used to host an entire book.  

It provides semantic support for two levels of the book hierarchy (Sections > Chapters).

Further structuring within chapters is handled using standard MediaWiki formatting (headings, subheadings, paragraphs, etc.).

The package ships pages for Templates, Forms, Categories, Properties, and a Lua Module so you can create and organize book content in a wiki.

## Requirements

### MediaWiki
Your MediaWiki version can be relatively standard; if you’re unsure, use a currently supported LTS release. 

### Extensions
* [SemanticMediaWiki](https://www.semantic-mediawiki.org/wiki/Help:Installation/Quick_guide)
* [PageForms](https://www.mediawiki.org/wiki/Special:MyLanguage/Extension:Page_Forms/Download_and_installation)
* [Scribunto](https://www.mediawiki.org/wiki/Special:MyLanguage/Extension:Scribunto)
* [SemanticScribunto](https://www.mediawiki.org/wiki/Special:MyLanguage/Extension:Semantic_Scribunto)

You will need [PageExchange](https://www.mediawiki.org/wiki/Special:MyLanguage/Extension:Page_Exchange) to install the package.

## Contents
What this provides
- Templates
  - Template:Book
  - Template:Chapter
  - Template:Section
- Forms (for PageForms)
  - Form:Chapter
  - Form:Section
- Categories
  - Category:Chapter
  - Category:Section
- Semantic properties (for Semantic MediaWiki)
  - Property:Chapter author
  - Property:Has order
  - Property:Has parent page
- Lua module (for Scribunto)
  - Module:Book
- page-exchange.json (package definition for import via [PageExchange](https://www.mediawiki.org/wiki/Special:MyLanguage/Extension:Page_Exchange)

## How to install/import
1) Ensure [PageExchange](https://www.mediawiki.org/wiki/Special:MyLanguage/Extension:Page_Exchange) is installed and configured.
2) Copy this repository (or just page-exchange.json) onto the web server where the wiki can read it; alternatively, host the JSON at a reachable URL.
3) Add the following to the bottom of your `LocalSettings.php`: 
```php
$wgPageExchangePackageFiles[] = 'https://raw.githubusercontent.com/WikiTeq/mediawiki-pages-WikiBook/master/page-exchange.json';
```
4) Navigate to `Special:Packages` and install the package
5) Run `php maintenance/run.php runJobs` (MediaWiki 1.43)

## Basic usage
- Set the book title on `MediaWiki:Wiki-book-title`, replacing the default value (`{{SITENAME}}`) 
- Create a page that will display the full book structure. Insert `Template:Book` call (`{{Book}}`).
- Add Sections using Form:Section
- Add Chapters using Form:Chapter. 
- Module:Book is used by the templates to render indexes or perform logic. It renders:
  - Context-dependent breadcrumbs ( Book / Section / Chapter )
  - In-book or in-section linear navigation ( Previous / Next )
  - A list of Chapters and their respective authors (on the Section pages)
  - A helper form input at the bottom of the Section pages that makes adding new Chapters easier.
