# Introduction to Dist::Zilla

<http://dzil.org/>
<http://metacpan.org/release/Dist::Zilla/>

------

# Automates Build and Release

---

# Overwhelmingly Configurable

---

# Plugins for Everything

------

# Start with your dist
## My-Basic-Dist

---

```
lib/My/Basic/Dist.pm
t/dist.t
```

------

# Install Dist::Zilla
## `cpan Dist::Zilla`

---

# The `dzil` command

------

# Create a config file
## `dist.ini`

---

# Dist information
```
name                = My-Basic-Dist
abstract            = A basic dist to try Dist::Zilla
author              = Doug Bell <preaction@cpan.org>
license             = Perl_5
copyright_holder    = Doug Bell <preaction@cpan.org>
copyright_year      = 2015

version             = 0.001
```

------

# Basic CPAN dist

---

```
[@Basic]
```

[Dist::Zilla::PluginBundle::Basic](http://metacpan.org/pod/Dist::Zilla::PluginBundle::Basic)

[Dzil docs on new dists](http://dzil.org/tutorial/new-dist.html)

------
# Run `dzil` commands

------

# `dzil build`

---

# Build Distribution

---

```
$ cd My-Basic-Dist
$ dzil build
[DZ] beginning to build My-Basic-Dist
[DZ] writing My-Basic-Dist in My-Basic-Dist-0.001
[DZ] building archive with Archive::Tar::Wrapper
[DZ] writing archive to My-Basic-Dist-0.001.tar.gz
```

---

# Builds dist
## `My-Basic-Dist-0.001`

---

# Creates archive
## `My-Basic-Dist-0.001.tar.gz`
You can upload this to PAUSE

------

# `dzil test`

---

# Test Distribution

---

```
$ dzil test
[DZ] building distribution under .build/RlLpqtqrdY for installation
[DZ] beginning to build My-Basic-Dist
[DZ] writing My-Basic-Dist in .build/RlLpqtqrdY
Checking if your kit is complete...
Looks good
Generating a Unix-style Makefile
Writing Makefile for My::Basic::Dist
Writing MYMETA.yml and MYMETA.json
cp lib/My/Basic/Dist.pm blib/lib/My/Basic/Dist.pm
PERL_DL_NONLAZY=1 "/usr2/local/perlbrew/perls/perl-5.16.3/bin/perl" "-MExtUtils::Command::MM" "-MTest::Harness" "-e" "undef *Test::Harness::Switches; test_harness(0, 'blib/lib', 'blib/arch')" t/*.t
t/dist.t .. ok
All tests successful.
Files=1, Tests=1,  0 wallclock secs ( 0.02 usr  0.04 sys +  0.01 cusr  0.03
csys =  0.10 CPU)
Result: PASS
[DZ] all's well; removing .build/RlLpqtqrdY
```

---

# Builds Dist
## CPAN-style

---

# Tests Built Dist
## Also CPAN-style

------

# `dzil release`

---

# Upload to PAUSE
[Get Your Credentials](https://pause.perl.org/pause/authenquery?ACTION=request_id)

---

# PAUSE Syncs to CPAN

---

# Configure PAUSE Account

```
$ cat ~/.pause
user PREACTION
password ********
```

---

# Build

```
$ dzil release
[DZ] beginning to build My-Basic-Dist
[DZ] writing My-Basic-Dist in My-Basic-Dist-0.001
[DZ] building archive with Archive::Tar::Wrapper
[DZ] writing archive to My-Basic-Dist-0.001.tar.gz
```

---

# Test

```
[@Basic/TestRelease] Extracting /home/nbkyslo/presentations/Introduction-to-Dist-Zilla-master/My-Basic-Dist/My-Basic-Dist-0.001.tar.gz to .build/5LUeKfVBIC
Checking if your kit is complete...
Looks good
Generating a Unix-style Makefile
Writing Makefile for My::Basic::Dist
Writing MYMETA.yml and MYMETA.json
cp lib/My/Basic/Dist.pm blib/lib/My/Basic/Dist.pm
PERL_DL_NONLAZY=1 "/usr2/local/perlbrew/perls/perl-5.16.3/bin/perl" "-MExtUtils::Command::MM" "-MTest::Harness" "-e" "undef *Test::Harness::Switches; test_harness(0, 'blib/lib', 'blib/arch')" t/*.t
t/dist.t .. ok
All tests successful.
Files=1, Tests=1,  0 wallclock secs ( 0.02 usr  0.03 sys +  0.02 cusr  0.02 csys =  0.09 CPU)
Result: PASS
[@Basic/TestRelease] all's well; removing .build/5LUeKfVBIC
```

---

# Release

```
*** Preparing to release My-Basic-Dist-0.001.tar.gz with @Basic/UploadToCPAN ***

Do you want to continue the release process? [y/N]: y
[@Basic/UploadToCPAN] registering upload with PAUSE web server
[@Basic/UploadToCPAN] POSTing upload for My-Basic-Dist-0.001.tar.gz to https://pause.perl.org/pause/authenquery
[@Basic/UploadToCPAN] PAUSE add message sent ok [200]
```

---

# Relax!

------

# Prereqs

`My-Prereqs-Dist`

---

# Plugin Config
```
[Prereqs]
perl = 5.010
strict = 0
warnings = 0
```

[Docs on configuring Prereqs](http://dzil.org/tutorial/prereq.html)

---

# Test Requirements
```
[Prereqs / TestRequires]
Test::More = 0
```

---

# List Prereqs
## `dzil listdeps`

---

```
$ dzil listdeps
ExtUtils::MakeMaker
strict
Test::More
warnings
```

---

# List `dzil` Prereqs
## `dzil authordeps`

---

```
$ dzil authordeps
Dist::Zilla::Plugin::Prereqs
Dist::Zilla::PluginBundle::Basic
```

---

# Install Prereqs

---

```
dzil listdeps | cpanm
```

---

# Install Missing Prereqs

---

```
dzil listdeps --missing | cpanm
```

------

# Version Management

---

# PkgVersion Plugin

`[PkgVersion]`

---

# Adds `$VERSION` to modules

---

# PodVersion Plugin

`[PodVersion]`

---

# Adds `=head1 VERSION` to POD

---

# Before
```
package My::Versioned::Dist;

use strict;
use warnings;


1;

=head1 NAME

My::Versioned::Dist - A dist with version modifications

```

---

# After!
```
package My::Versioned::Dist;
{ $My::Versioned::Dist::VERSION = '0.001'; }

use strict;
use warnings;


1;

=head1 NAME

My::Versioned::Dist - A dist with version modifications

=head1 VERSION

version 0.001

```

------

# Git Management

---

# Git Plugin Bundle
## `[@Git]`

[Dist::Zilla::PluginBundle::Git](http://metacpan.org/pod/Dist::Zilla::PluginBundle::Git)

---

# Check Repo
## No Missed Changes

---

# Commit Built files

---

# Tag Release

---

# Push Tags

------

# Lots more!

---

# Build Cpanfile

<https://metacpan.org/pod/Dist::Zilla::Plugin::CPANFile>

---

# Auto-Increment Version

<https://metacpan.org/pod/Dist::Zilla::Plugin::Git::NextVersion>

---

# Create README

<https://metacpan.org/pod/Dist::Zilla::Plugin::ReadmeAnyFromPod>

---

# Pod::Weaver

<http://metacpan.org/pod/Dist::Zilla::Plugin::PodWeaver>

---

# Generate Test Scripts

<https://metacpan.org/pod/Dist::Zilla::Plugin::Test::ReportPrereqs>
<https://metacpan.org/pod/Dist::Zilla::Plugin::Test::Compile>

---

# Build Change Log

<https://metacpan.org/pod/Dist::Zilla::Plugin::ChangelogFromGit::CPAN::Changes>

------

# It's over!

<http://github.com/preaction/Introduction-to-Dist-Zilla/>
