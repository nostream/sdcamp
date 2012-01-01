# Introduction #

As open source books, ebooks and pdf format should be created on fly, the following chapter describe those solution detail.

The solution below is reused from [Pro Git](progit)

#Making Ebooks#

[ruby rdiscount](https://github.com/rtomayko/rdiscount) is used to convert all the markdown files to html format.

[Calibre](calibre)'s command `ebook-convert` is used to convert html files into ebooks like `.mobi` (Kindle) and `.epub` (for iPad), it exists in several platforms (Windows, OS X, Linux).

After preparing the environment, you can simple run the command below to generate related ebooks

    $ ./makeebooks zh  # default for .mobi
	$ export FORMAT=epub ; 
	$ ./makeebooks zh  # for epub

## Ubuntu ##
Ubuntu 11.04 (Natty) is verified, it should work in other version as well with slight changes.

    $ sudo apt-get install ruby calibre rubygems # ruby 1.8.7 is used
	$ sudo apt-get install calibre # calibre 0.7.44 for ubuntu 11.04
	$ gem install rdiscount ruby-debug 
	
## Windows (not fixed) ##
	
[RubyInstaller & DevKit](http://rubyinstaller.org/downloads/) is needed for ruby environment on windows, ruby 1.9 is verified, and "Git for windows" is used to provide unix environment.
	
	$ gem install rdiscount 
	$ gem install ruby-debug19 # have problem
	
	Building native extensions.  This could take a while...
	ERROR:  Error installing ruby-debug19:
        ERROR: Failed to build gem native extension.

        c:/Ruby193/bin/ruby.exe extconf.rb
	checking for vm_core.h... no
	c:/Ruby193/lib/ruby/gems/1.9.1/gems/ruby_core_source-0.1.5/lib/ruby_core_source.rb:39: Use RbConfig instead of obsolet
	and deprecated Config.
	checking for vm_core.h... no
	*** extconf.rb failed ***
	...
	
[Calibre](calibre)'s command `ebook-convert` is under `calibre` directory, it should be added into your path, then the related ebook can be created.	
	
## Fedora platform ##
This is copied from [Pro Git](progit), not verified yet

On Fedora you can run something like this::

    $ yum install ruby calibre rubygems ruby-devel rubygem-ruby-debug 
    $ gem install rdiscount
    $ makeebooks en  # will produce a mobi
	
#Making Pdf books#
PDF format is used to printout in nice way like real book, and [Calibre](calibre) is not good at this area, [pandoc](http://johnmacfarlane.net/pandoc/) is used instead to generate latex from markdown, and latex tool `xelatex` (is part of [TexLive](texlive) now) is used to convert pdf from latex.

Please check [ctax](http://www.ctan.org/) and [TexLive](texlive) for more background for latex, which is quite complicated and elegant if you have never touched before.

## Ubuntu Platform ##

[pandoc](http://johnmacfarlane.net/pandoc/) can be installed using `apt-get` command directly.

Though texlive exists inside Ubuntu repository, it is little old. texlive 2011 from [TexLive](texlive) is recommended. After installed according to the instruction, configure the binary path.

`pandoc` needed X-Windows for some reason, If X-Windows is not used like server only, then [xvfb](http://en.wikipedia.org/wiki/Xvfb) (Virtual Framebuffer 'fake' X server) package should be installed to support headless X-Windows. Simple X-Windows server like XMing doesn't support X-Input.

	$ sudo apt-get install pandoc
	$ #mount texlive iso file and install directly
	$ export PATH=$PATH:/usr/local/texlive/2011/bin/i386-linux
	$ sudo apt-get install xvfb
	
You may need to install related fonts like Chinese, fortunately they exist in repository already.
    
    $ sudo apt-get install language-support-fonts-zh-hans	
	
Then you should be able to generate pdf

    $ xvfb-run ./makeebooks zh # if no X-Windows
	$ ./makeebooks zh

[calibre] : http://calibre-ebook.com/
[progit] : http://github.com/progit/progit 
[texlive] : http://www.tug.org/texlive/
