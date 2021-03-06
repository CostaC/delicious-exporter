# Delicious Exporter

A script for scraping and exporting your bookmarks from del.icio.us.

## Background

deli.icio.us is a bookmarking service that went through a series of increasingly more unfortunate acquisitions. As of January 1st, 2017, the website is frequently down, yet doesn't allow users to export their bookmarks. At the same time, it no longer offers an API, and prohibits anyone from content scraping.

That's deeply unsettling, since many users have used del.icio.us to store thousands of bookmarks, capturing years of internet browsing history.

This script allows users to export their content to [HTML bookmarks](https://msdn.microsoft.com/en-us/library/aa753582.aspx "Netscape Bookmark File Format") file, in the format accepted by major browsers. It will preserve tags and dates. Additional option enables validation and skipping of dead URLs.


## Requirements

* Ruby
* nokogiri gem. Check nokogiri documentation for [installation instructions](http://www.nokogiri.org/tutorials/installing_nokogiri.html).
* [curl](https://curl.haxx.se/download.html)

## Usage

### Export all public links

`./export.rb -u USERNAME -o bookmarks.html`

`USERNAME` the name of del.icio.us user whose bookmarks will be exported. `bookmarks.html` is the output file, where the bookmarks will be saved.

The above command will export all public links from selected del.icio.us account, including dead ones. This may take few minutes, depending on the number of links.

### Export all links, including private:

`./export.rb -u USERNAME -p PASSWORD -o bookmarks.html`

If you provide a password, the script will attempt to login on your behalf and export all links, including those marked as private. To make it easier to identify private links later, the script adds a special tag to them: *___private*.

### Export only valid links

`./export.rb -u USERNAME -o bookmarks.html --validate`

When you provide `--validate` option, the script will try to fix or skip dead links:

1. If the server doesn't respond within 5 seconds, the link will be skipped.
2. If the server sends a redirect header, the script will follow it and save the target URL.

This mode is much slower and can take about 2 minutes for every hundred links.

## License

The script is available under provisions of [public domain license](https://creativecommons.org/publicdomain/zero/1.0/). You are free to copy and modify it without asking for author's permission. The author doesn't provide any warranty or support.

Please be aware that content scraping is currently not allowed by [del.icio.us' terms and conditions](https://del.icio.us/terms). The author doesn't take any responsibility for your usage of this script.
