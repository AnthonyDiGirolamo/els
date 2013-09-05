els = ls with emoji icons
-------------------------

This is a simple wrapper for `ls` written in ruby (version 1.9.3 or higher) to
display emoji icons alongside file names. It was written and tested on MacOS X
which uses the BSD version of ls. It will also work with the GNU ls.

All arguments are passed along to ls with the exception of --els-no-color which
disables the built in color handling.

[![](http://anthonydigirolamo.github.io/els/screen1.png)](http://anthonydigirolamo.github.io/els/screen1.png)
[![](http://anthonydigirolamo.github.io/els/screen2.png)](http://anthonydigirolamo.github.io/els/screen2.png)
[![](http://anthonydigirolamo.github.io/els/screen3.png)](http://anthonydigirolamo.github.io/els/screen3.png)
[![](http://anthonydigirolamo.github.io/els/screen4.png)](http://anthonydigirolamo.github.io/els/screen4.png)

### Installation

    curl -O https://raw.github.com/AnthonyDiGirolamo/els/master/els
    chmod +x els

Then place it somewhere in your `$PATH`

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
and send me a pull request if you do so everyone can enjoy your changes. Here is
the current setting:

    FileTypes = {
      :executable => {
        :icon       => '🚀',
        :extensions => %w{ex} },
      :link => {
        :icon       => '🔗',
        :extensions => %w{ln} },
      :directory => {
        :icon       => '📂',
        :extensions => %w{di} },
      :fifo => {
        :icon       => '🚿',
        :extensions => %w{pi} },
      :socket => {
        :icon       => '🔌',
        :extensions => %w{so} },
      :archive => {
        :icon       => '📦',
        :extensions => %w{tar tgz arj taz lzh lzma tlz txz zip z Z dz gz lz xz bz2 bz tbz tbz2 tz deb rpm jzr war ear sar rar ace zoo cpio 7z rz} },
      :cd => {
        :icon       => '💿',
        :extensions => %w{dmg iso cue img} },
      :pdf => {
        :icon       => '📕',
        :extensions => %w{pdf} },
      :image => {
        :icon       => '🗻',
        :extensions => %w{gif tiff jpg jpeg png} },
      :text => {
        :icon       => '📄',
        :extensions => %w{txt} },
      :sound => {
        :icon       => '🔈',
        :extensions => %w{mp3 wav ogg aiff} },
      :movie => {
        :icon       => '📺',
        :extensions => %w{mp4 avi mkv mov} },
      :blank => {
        :icon       => ' ',
        :extensions => %w{} },
    }

### Notes on implementation

This script started out using lots of regexes but that turned out to be very
slow. Now simple string matching is used to detect extensions and `ls -F`
classifiers.

The column formatting tries to reduce the amount of horizontal whitespace and
maximize the number of columns. Using `-l` will disable it of course.

