# mediawiki-pages-WikiBook

## Description
A compact, ready-to-import MediaWiki package for modeling books with any hierarchical structure.

The package supports cases where a wiki is used to host an entire book.  

It provides semantic support for the arbitrary levels of the book hierarchy.

The package ships pages for Templates, Forms, Properties, Widgets, System messages, and a Lua Module so you can create and organize book content in a wiki.

## Requirements

### MediaWiki
Your MediaWiki version can be relatively standard; if you’re unsure, use a currently supported LTS release. 

### Extensions
* [SemanticMediaWiki](https://www.semantic-mediawiki.org/wiki/Help:Installation/Quick_guide)
* [PageForms](https://www.mediawiki.org/wiki/Special:MyLanguage/Extension:Page_Forms/Download_and_installation)
* [Scribunto](https://www.mediawiki.org/wiki/Special:MyLanguage/Extension:Scribunto)
* [SemanticScribunto](https://www.mediawiki.org/wiki/Special:MyLanguage/Extension:Semantic_Scribunto)
* [Widgets](https://www.mediawiki.org/wiki/Special:MyLanguage/Extension:Widgets)

You will need [PageExchange](https://www.mediawiki.org/wiki/Special:MyLanguage/Extension:Page_Exchange) to install the package.

## Contents
What this provides
- Templates
  - Template:Book - _renders book hierarchy_
  - Template:Subpage - _stores page semantics and renders package-specific elements_
- Forms (for PageForms)
  - Form:Subpage - _default form for managing the book page metadata_
- Semantic properties (for Semantic MediaWiki)
  - Property:Has lead author
  - Property:Has contributing author
  - Property:Has author - _internally joins values of the previous two_
  - Property:Has order - _defines the order of the page across the siblings of the same parent_
  - Property:Has parent page
- Lua module (for Scribunto)
  - Module:Book
- System messages
  - MediaWiki:Wiki-book-footer - _stores content of the book footer_
  - MediaWiki:Wiki-book-breadcrumbs-separator - _allows for custom separator between breadcrumbs, default `>`_
  - MediaWiki:Wiki-book-create-subpage-prompt - _stores prompt for the subpage creation form_
  - MediaWiki:Wiki-book-children-list-intro - _a dynamic heading for the list of the current page subordinates_
- Assets
  - Widget:Wiki-book - contains the package-specific scripts and styles
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
6) Create `MediaWiki:Wiki-book-title` and set the book title there. Keep it plain and simple, as it will be used as a page name. 

## Basic usage
- Create a page that will display the full book structure (e.g., the same page you set in `MediaWiki:Wiki-book-title`). Insert `Template:Book` call (`{{Book}}`).
- Add Sections using Form:Section
- Add Chapters using Form:Chapter. 
- Module:Book is used by the templates to render indexes or perform logic. It renders:
  - Context-dependent breadcrumbs
  - Linear navigation ( Previous / Next )
  - Author list
  - List of subordinate pages
  - A helper form input that makes adding new Chapters easier
  - Book footer
