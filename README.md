Mediawiki Simple Breadcrumb
===========================

A hierarchical breadcrumb extension for MediaWiki. Implements a {{#breadcrumb: }} tag to set a parent page for each page. The resulting breadcrumb is displayed under the page title.
Tested with MediaWiki version 1.39.5

Usage
-----

Just add a {{#breadcrumb: }} tag anywhere in your page to set its parent and its (the current page's) alias.

	{{#breadcrumb: Parent_Page | Alias }}

The alias will replace the page's name in the breadcrumb trails for all descendant pages, in addition to the current page. The page at the top of the hierarchy (i.e., the page that has no parent) may still be given an alias, which will show up in all the descendants' breadcrumb trails. The top page will not display a breadcrumb. 

The tag can be used in templates and accepts variables.

	{{#breadcrumb: Category:Releases {{{product}}} | {{SUBPAGENAME}} }}

You should not add more than one breadcrumb tag in each page. In experimentation, if there are two breadcrumb tags, the second one is the one that is effective, but this behavior is not tested.

Installation
------------

Copy the files to a folder named "SimpleBreadcrumb" in your extensions directory. 
Edit LocalSettings.php to include the extension:

	// Simple Breadcrumb
	wfLoadExtension( 'SimpleBreadcrumb' );

Run the update script, which will automatically create the necessary database tables that this extension needs.

Configuration
-------------

The extension offers these configuration variables that can be overriden in LocalSettings.php after the inclusion of the extension.

	$wgbcdelimiter            = ' &gt; ';     // Breadcrumb delimiter string
	$wgbcMaxCount             = 5;            // Maximum elements in breadcrumb
	$wgbcOverflowPrefix       = '&hellip;';   // Prefix when breadcrumb has more elements than fixed limit

The extension adds the class "breadcrumbs-page" to the <body> tag on pages where the parser tag is used. This allows the use of CSS styles for such pages (for example, to suppress **subpage** breadcrumbs on only those pages where this extension is invoked). To do so, the following could be added to Mediawiki:Common.css. 

	/* Hide parent breadcrumbs on subpages*/
	.breadcrumbs-page .subpages { 
	display: none !important;
	}
