# Dummy PulseAudio Debian package!

Do you really, deeply, like PulseAudio not? Do you want to prevent it running,
or better, even existing on your Debian system? Does apt-get still insist on
pulling it as a dependency of something else? Does it get really, really
frustrating when it randomly kills your ALSA mixer setup and stops working when
any app decides to start it?

Say no more!

## Installation

This creates a local repository with pulseaudio `.deb` package that contains
precisely nothing (except for symlinks to `/bin/true` in place of PA binaries):

1. Clone and `cd` the repository
2. `cd pulseaudio/`
3. `debuild -us -uc` will create the dummy packages (in the parent directory). If you don't have `debuild`, install it using `apt-get install devscripts`
4. Install the local debian repository: `apt-get install local-apt-repository`
5. Copy the newly created packages to your local repo: `cd ..; cp pulseaudio_*.* /srv/local-apt-repository/` (you'll need `sudo` or other root)
6. `systemctl restart local-apt-repository` will reindex the packages
7. `apt-get update` will pull your new repo to your system's APT catalog
8. `apt-get install --only-upgrade pulseaudio` should now install the dummy PA version.
9. That's it ma, no pulseaudio!

## Workarounds

For (depraved) stuff that really requires PulseAudio, you can install this
beautiful wrapper:

https://github.com/i-rinat/apulse

## Disclaimer

This _will_ break PA-dependent stuff in weird ways, possibly with linking
errors. I put it together in like 10 minutes so feel free to tell me what I did
totally wrong.

Version number was carefully chosen to be a tiny bit higher than most PA
versions.
