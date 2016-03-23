linenoise.io
=================

This is the codebase that runs [Danne Stayskal's music site](http://linenoise.io/). It is developed using [nanoc](http://nanoc.stoneship.org/) and rsynced in static form to the server.

Installation
------------

Prerequisites: [OpenSSH](http://www.openssh.com/), [Rsync](http://rsync.samba.org/), [Ruby](http://www.ruby-lang.org/), [RubyGems](http://rubygems.org/pages/download), [Ruby Version Manager](https://rvm.beginrescueend.com/), and [Bundler](http://gembundler.com/).

First, clone this codebase

	$ git clone git@github.com:linenoise/io.git linenoise-io

Second, accept the RVM version and gemset, building Ruby 2.2.2 if you need

	$ rvm install ruby-2.2.2

Finally, install Bundler and the rest of the gemset

	$ gem install bundler
	$ bundle install

At this point, you're ready to make changes.

Maintenance
-----------

This codebase uses nanoc to build a tree of static HTML, CSS, and JavaScript resources to be uploaded to the server.  Assets (such as images and recordings) are included in this final build.  Once Bundler has nanoc and friends installed, running a maintenance server is straightforward:

	$ nanoc autocompile

This will automatically compile any changes made to the build and make them available through a lightweight webserver running at http://localhost:3000/.

Uploading a Set
---------------

Play music. Dance (optional, recommended). Record the set (required).

Materials:

* MP3 recording (320 bitrate) of your set.
* TXT track listing text file ("0:00 Artist - Track\n"...)
* TXT genre listing (tech.house, dub.techno, uk.garage, ...)
* HTML description of the set (when, where, link to event ...)
* JPG cover image for Mixcloud

Get it onto AWS:

1. [Login to AWS S3](https://console.aws.amazon.com).
2. Upload the set.
3. Make it public.
4. Set metadata: `Content-Type` is `application/octet-stream` and `Content-Disposition` is `attachment`. This should force most browsers (but sadly not all) to download rather than stream the set.

Get it onto MixCloud:

1. Upload set (along with track listing, cover image, etc) to MixCloud.
2. Get the embed code for the set. Options to click: 100% width, Show Cover, Light Widget, Show Tracklist, Show Artwork. Options to make sure are un-clicked: Auto Play, Mini Player.

Get it onto Linenoise.io:

1. Clone this repo.
2. Add an HTML file in `content/sets` (just copy the structure from a different release). You'll need the title, date, genres, download link, description, and embed code.)
3. Add above file to Version control (`git add content && git push origin master;`)
4. `./push`

Deployment
----------

To deploy, make sure you've got your deploy keys in place, then run:

	$ ./push

Easy as pie.
