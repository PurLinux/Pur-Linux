## News - 01/2018
Pür Linux is now Sanity Linux! This name change comes as I resume work on the disstro, and got tired of people calling it "Purr Linux? Like a cat?"

## News - 06/2017
The distro is looking for contributors! Got the chops to bring a Linux distro to life? There's too much work for me to do alone in a reasonable amount of time. Come waste hours of your life with me and delve into voluntary alcoholism while contributing to a FOSS project that'll let you brag at the hackerspace!

# Sanity Linux
Sanity Linux is a Linux distribution focused on Stability, Security, and Simplicity. No wonky distro-specific changes, no unneeded packages in base, and best of all (in our opinion), no systemd (though we're big proponents of freedom, and do not explicity make system changes designed to render it impossible for you to install systemd if you so choose. We have no intention of providing a package for it, however.)

## About Sanity
Sanity Linux consists of a base system comprised of upstream pure code (GNU utils you'd expect on a Linux system, the latest vanilla Linux kernel upon packaging), and the Linux port of pkgsrc from NetBSD for ports.

Sanity Linux is not a fork, nor respin of any pre-existing Linux Distribution.
The only relation to any other distro is that right now, we use an Arch Linux box for building the environment that gets tar'd.

Unlike other Linux distributions, Sanity Linux uses a Base/Ports paradigm, similar to FreeBSD, wherein the base operating system is updated and maintained separately from user-installed packages. This means you can update them independently, and package updates won't bork your OS.

Sanity Linux will be distributed in a quarterly release schedule.

Installation will be as simple as untarring and running setup.sh, or running setup from a Pür installation disk, similar to Slackware's installation process.

All configurations are done via plaintext files, or shell scripts.

Shells included are csh, ksh, and dash.

We are also the very FIRST Linux Distribution with plans to ship NTPsec rather than classic NTP or OpenNTP by default!
https://www.ntpsec.org/

## The Sanity Linux Team
* Rainbow  - Project Director, BASE team lead, Packages Maintainer. https://twitter.com/hacker_horse
* Brent - Git Wizard, Architecture Engineer, BASE Developer.  https://twitter.com/sysadm_podcast

## Benefits of Sanity
* No weird distro-specific changes to the file-system hierarchy: we use a standardized filesystem layout, similar to FreeBSD and traditional UNIX.
* No binary logs or incomprehensible configuration formats: We're not using systemd. Everything is logged to plaintext. Configuration files are the same, unless otherwise specified by upstream, which brings us to:
* 100% Upstream code: everything is build from upstream code. Everything works as the programmers intended, and all documentation is correct (or as correct as the programmer wrote) for the version installed.
* Latest code: Sanity's goal is to provide the latest stable code releases from the programmers and teams involved. You won't find a 3 year out of date version of something here. Every release is completely comprised of the newest stable releases, unless otherwise specified in the Changelog/Errata Notification
* No new tools to learn: If you know UNIX, you know Sanity Linux. Releases are installed and updated as tarballs you simply extract and overwrite with. Wanna copy your configuration to a whole new system? Tar up /etc and /usr/local, and extract onto a new disk or partition along with the latest Sanity Linux release tarball. Done!
* Releases are synced with the latest stable snapshot of the NetBSD pkgsrc tree, and via pkgin and pkgsrc's automated building framework, binary packages are also available, in addition to the standard From Source methodology provided by pkgsrc
* ZFS is a supported Filesystem, and will be included as a Loadable Kernel Module compiled against the current upstream stable Linux kernel.

## Plans

### Init
We are looking at various init systems right now, as init is the last egg to crack before we're ready to start looking at pre-releases and tuning what packages we include in BASE.
While we do not plan to make it technologically impossible to use systemd on Pür, there will be absolutely no support for such a configuration.
Our current plans are to use an rc-like system, to better integrate with pkgsrc's rc scripts, however the project is open to suggestions from the community.

### Other Stuff
While we would like to include Clang/LLVM, due to the Linux kernel being reliant on GCC-specific tweaks right now, we will be including GCC in base, with Clang available via pkgsrc. Plans will be made to transition to Clang in base as soon as is feasible.

### Project Roadmap
* January 2018 - Initial fork from CURRENT into 2018-STABLE

## Development Branches
Similar to FreeBSD, we currently maintain multiple branches. 
* CURRENT - Bleeding edge. Where most of the work occurs. Constantly contains the latest versions of upstream.
* STABLE - The current non-bleeding-edge development branch of the distribution. Currently, we plan yearly branch forks from CURRENT. The STABLE branch will keep up to date with stable upstream code, but major architectural changes, large software version leaps, and major GLibC updates are restricted to CURRENT. STABLE will be usable, however we suggest running a RELEASE image unless you're a developer or interested in development.
* RELENG - Sanity Linux's Release Engineering branch is where we stage work for release candidates. Additionally, Security updates are imported into this branch, as well as switching to a new STABLE branch of pkgsrc. No version increases occur in RELENG once it forks from STABLE. RELENG branches only exist to provide security updates to RELEASE, and EOL after 3 months.
* RELEASE - The current stable release of Sanity Linux. Releases are formatted as Year.Month-RELEASE, and are tagged out of the RELENG branch. Security updates are tagged with a U, and branched from STABLE. For example, 2016.07-RELEASE-U1 would be the first security update for 2016.07-RELEASE

Due to the release schedule, Security Updates will only be supplied for a version until the next major version release.
This means each major version has a 3 month lifecycle until EOL. You will not receive any help for running an EOL version.

## Installation notes

Please be aware of the following caveats:

As we are using pkgsrc for installed packages, Sanity Linux will be placing all installed packages inside the /usr/local directory, similar to FreeBSD. /bin, /sbin, /etc, /usr/bin, and /usr/sbin will only be used for Base utilities.
As such, some scripts (primarily python and perl scripts where other distros have the interpreters in /usr/bin) you download may require tweaking (We always suggest using the #!/usr/bin/env $shell shebang over hardcoded paths) to work on Sanity Linux.

## Contributing

Please clone the branch of your choice and get to work! Branch it in your fork with the following naming conventions:
$HEADBRANCH/${Feature/Bugfix/Versioning}/$Brief-Description.
Example: CURRENT/Versioning/Update-GCC-5
Open a pull request when you're ready from that branch against $HEADBRANCH and someone from the team will review it as soon as we can!
If you have a commit-bit from us, please follow the same rules, however you can usually merge your own PRs.
Please tag @RainbowHackerHorse for review if it's not urgent.

## FAQ

Q: But I liked the old name!

A: So did I. I got tired of people whining about it, and Sanity Linux makes a little more sense anyway. We're an island of sanity in all the
crazy stuff going on in Linux-land lately.

Q: So does pkgsrc update the whole system?

A: Nope! Sanity Linux breaks the traditional Linux paradigm of EVERYTHING IS A PACKAGE. I'm a FreeBSD contributor, and I really enjoy the separation between the Base system and 3rd party packages. While Sanity Linux won't be developed in a single source tree like FreeBSD (No desire nor need to fork much) there's still going to be separation between the Base OS (Sanity Linux) and Ports (using pkgsrc)

Q: How are we sure no one tampered with anything?

A: Well, as far as the distro itself, you have to trust us. Thing is, you do that with Ubuntu/CentOS/Slackware/Gentoo already anyway. And like them, everything we're doing is open and available, even our build system, so you can reproduce everything. As far as releases go, each release, as well as the source tarballs, will be signed via a minimum of two senior developers from the project, and checksummed.

Q: I wanna send you a message. Wat Do.

A: Email rainbow@purlinux.org

My PGP key is 0x5F94763A

You can also just hit me up on Twitter. https://twitter.com/hacker_horse

You can also follow https://twitter.com/PurLinux or email info@purlinux.org

Q: IRC?

A: #purlinux on irc.freenode.net 
Come say hi!

Q: Primary Project Master repo?

A: On Github, the primary master repo is at https://github.com/SanityLinux/Base 

The original repo was located at https://github.com/RainbowHackerHorse/Pur-Linux/ now https://github.com/RainbowHackerHorse/Pur-Linux-Base/tree/Legacy

Other people may have their own forks. 

Q: How do I build the distro?

A: Clone the branch you want to fiddle with and run purbuild.sh 
