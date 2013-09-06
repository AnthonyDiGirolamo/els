els = ls with emoji icons
-------------------------

This is a simple wrapper for `ls` written in ruby (version 1.9.3 or higher) to
display emoji icons alongside file names. It was written and tested on MacOS X
which uses the BSD version of ls. It will also work with the GNU ls.


[![](http://anthonydigirolamo.github.io/els/screen1.png)](http://anthonydigirolamo.github.io/els/screen1.png)
[![](http://anthonydigirolamo.github.io/els/screen2.png)](http://anthonydigirolamo.github.io/els/screen2.png)
[![](http://anthonydigirolamo.github.io/els/screen3.png)](http://anthonydigirolamo.github.io/els/screen3.png)
[![](http://anthonydigirolamo.github.io/els/screen4.png)](http://anthonydigirolamo.github.io/els/screen4.png)
[![](http://anthonydigirolamo.github.io/els/screen5.png)](http://anthonydigirolamo.github.io/els/screen5.png)

### Installation

    curl -O https://raw.github.com/AnthonyDiGirolamo/els/master/els
    chmod +x els

Then place it somewhere in your `$PATH`

### Options

All arguments are passed along to ls with the exception of:

* `--els-no-color` disables the built in color handling.
* `--els-icons=fontawesome` uses icons provided by
  [FontAwesome](http://fortawesome.github.io/Font-Awesome/)

Using FontAwesome requires that you install the `FontAwesome.otf` by double
clicking on it in OSX. To actually use it in your terminal you need
[iTerm2](http://www.iterm2.com/) for OSX and change your Non-ASCII Font to
FontAwesome in your profile preferences as in this screen shot:

[![](http://anthonydigirolamo.github.io/els/iterm2config.png)](http://anthonydigirolamo.github.io/els/iterm2config.png)

To use it in Linux within gnome-terminal you need to put `FontAwesome.otf`
inside your `~/.fonts/` folder on Linux. And create a
`~/.config/fontconfig/fonts.conf` file with the following content:

    <?xml version='1.0'?>
    <!DOCTYPE fontconfig SYSTEM 'fonts.dtd'>
    <fontconfig>
    <!-- Font families -->
    <alias>
      <family>serif</family>
      <prefer>
        <family>DejaVu Serif</family>
        <family>Android Emoji</family>
        <family>Symbola</family>
      </prefer>
    </alias>
    <alias>
      <family>sans-serif</family>
      <prefer>
        <family>DejaVu Sans</family>
        <family>Android Emoji</family>
        <family>Symbola</family>
      </prefer>
    </alias>
    <alias>
      <family>monospace</family>
      <prefer>
        <family>Ubuntu Mono</family> <!-- change this to your prefered monospace font if you like -->
        <family>DejaVu Sans Mono</family>
        <family>Android Emoji</family> <!-- put the Symbola line before this if you prefer Symbola to Android Emoji -->
        <family>Symbola</family>
        <family>FontAwesome</family>
      </prefer>
    </alias>
    </fontconfig>

### Colors

`els` honors the `$LS_COLORS` environment variable and expects the GNU format
(not BSD!). This is usually set by the `dircolors` command in Linux. If
`$LS_COLORS` is not set `els` will use a default setting. This lets you use OSXs
default BSD `ls` but still the GNU `$LS_COLORS` features.

If you want the GNU version of `ls` on OSX use [homebrew](brew.sh) to install
coreutils. It will then be available as `gls`. (This isn't required).

    brew install coreutils

### Adding/Changing Icons

You can add your own icons and extensions by editing the source. Fork this repo
and send me a pull request if you do so everyone can enjoy your changes.

### Notes on implementation

This script started out using lots of regexes but that turned out to be very
slow. Now simple string matching is used to detect extensions and `ls -F`
classifiers.

The column formatting tries to reduce the amount of horizontal whitespace and
maximize the number of columns. Using `-l` will disable it of course.

