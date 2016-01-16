
## About

I created this tool that will export your DayOne journal entries
into individual jpeg files with the entry text as the caption
metadata of the jpegs.

I use this export to build a photo book in Lightroom (using the
Book Module).  Unfortunately there doesn't seem to be a way to
maintain formatting of the entries (newlines, boldness, etc) so
you'll have to manually go into each entry on Lightroom and fix
the formats.

## Installation

1. Clone this repo
2. `gem install bundler` (if you don't already have it)
3. `bundle install`

## Usage Examples

* `rake` (export the last 30 days)
* `rake from=2014-01-01 to=2014-12-31` (export 2014)
* `rake include='Tag1,Tag2' exclude='Tag3'`

`from`, `to`, `include`, and `exclude` can all be used together.
