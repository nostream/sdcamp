#Making Ebooks#

The solution below is reused from [Pro Git](http://github.com/progit/progit) with more detail instruction. 

[ruby rdiscount](https://github.com/rtomayko/rdiscount) is used to convert all the markdown files to html format.

[Calibre](http://calibre-ebook.com/)'s command ebook-convert is used to convert html files into ebooks like .mobi (Kindle) and .epub (for iPad), it exists in several platforms (Windows, OS X, Linux).

After preparing the environment below, you can simple run the command below to generate related ebooks

    $ ./makeebooks zh  # default for .mobi
	$ export FORMAT=epub ; 
	$ ./makeebooks zh  # for epub

## Ubuntu ##
I use Ubuntu 11.04 is used , it may be different to other version.

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
	
Calibre's command `ebook-convert` is under `calibre` directory, it should be added into your path, then the related ebook can be created.	
	
## Fedora platform ##
This is copied from Pro Git's solution, not verified yet

On Fedora you can run something like this::

    $ yum install ruby calibre rubygems ruby-devel rubygem-ruby-debug 
    $ gem install rdiscount
    $ makeebooks en  # will produce a mobi
	
#Making Pdf books#
