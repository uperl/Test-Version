# Test::Version ![linux](https://github.com/uperl/Test-Version/workflows/linux/badge.svg) ![macos](https://github.com/uperl/Test-Version/workflows/macos/badge.svg) ![windows](https://github.com/uperl/Test-Version/workflows/windows/badge.svg) ![cygwin](https://github.com/uperl/Test-Version/workflows/cygwin/badge.svg)

Check to see that version's in modules are sane

# SYNOPSIS

```perl
use Test::More;
use Test::Version 1.001001 qw( version_all_ok ), {
    is_strict   => 0,
    has_version => 1,
    consistent  => 1,
  };

# test blib or lib by default
version_all_ok();

done_testing;
```

# DESCRIPTION

This module's goal is to be a one stop shop for checking to see that your
versions across your dist are sane. Please ensure that you use version `0.04`
or later only, as earlier versions are old code and may not work correctly.
Current feature list:

- module has a version

    Tests to insure that all modules checked have a VERSION defined, Can replace
    [Test::HasVersion](https://metacpan.org/pod/Test::HasVersion)

- module has a valid version

    Tests to insure that all versions are valid, according to the rules of
    [version](https://metacpan.org/pod/version) method `is_lax`. To quote:

    _The lax criteria corresponds to what is currently allowed by the version
    parser. All of the following formats are acceptable for dotted-decimal formats
    strings:_

    ```
    v1.2
    1.2345.6
    v1.23_4
    1.2345
    1.2345_01
    ```

    _If you want to limit yourself to a much more narrow definition of what a
    version string constitutes, is\_strict() is limited to version strings like
    the following list:_

    ```
    v1.234.5
    2.3456
    ```

    you can cause your tests to fail if not strict by setting [is\_strict](#is_strict) to
    `1`

# FUNCTIONS

## version\_ok

```
version_ok( $filename, [ $name ] );
```

Test a single `.pm` file by passing a path to the function. Checks if the
module has a version, and that it is valid with `is_lax`.

## version\_all\_ok

```
version_all_ok( [ $directory, [ $name ]] );
```

Test all modules in a directory with `version_ok`. By default it will check
`blib` or `lib` if you haven't passed it a directory.

# CONFIGURATION AND ENVIRONMENT

## has\_version

```perl
use Test::Version qw( version_all_ok ), { has_version => 0 };
```

Allows disabling whether a module has to have a version. If set to 0
version tests will be skipped in any module where no version is found.

really doesn't make sense to use with just [version\_ok](#version_ok)

## is\_strict

```perl
use Test::Version { is_strict => 1 };
```

this allows enabling of [version](https://metacpan.org/pod/version)s `is_strict` checks to ensure that your
version is strict.

## consistent

```perl
use Test::Version { consistent => 1 };
```

Check if every module has the same version number.

## ignore\_unindexable

```perl
use Test::Version { ignore_unindexable => 0};
```

if you have at least [Module::Metadata](https://metacpan.org/pod/Module::Metadata) v`1.000020` Test::Version will by
default skip any files not considered [is\_indexable](https://metacpan.org/pod/Module::Metadata#is_indexable)

## filename\_match

```perl
use Test::Version 2.0 { filename_match => [qr{Foo/Bar.pm$}] };
```

Only test files that match the given pattern.  Pattern may be a list of
strings, regular expressions or code references.  The filename will match
if it matches one or more patterns.

- string

    The file matches if it matches the pattern string exactly.

- regular expression

    The file matches if it matches the regular expression.

- code reference

    The file matches if the code reference returns a true value.  The filename
    is passed in as the only argument to the code reference.

## multiple

```perl
use Test::Version 2.02 { multiple => 1 };
```

Test each version for each package if multiple packages are found in a file.

# SEE ALSO

The goal is to have the functionality of all of these.

- [Test::HasVersion](https://metacpan.org/pod/Test::HasVersion)
- [Test::ConsistentVersion](https://metacpan.org/pod/Test::ConsistentVersion)
- [Test::GreaterVersion](https://metacpan.org/pod/Test::GreaterVersion)

If you are using [Dist::Zilla](https://metacpan.org/pod/Dist::Zilla) there is a plugin

- [Dist::Zilla::Plugin::Test::Version](https://metacpan.org/pod/Dist::Zilla::Plugin::Test::Version)

# BUGS

Please report any bugs or feature requests on the bugtracker website
[https://github.com/plicease/test-version/issues](https://github.com/plicease/test-version/issues)

When submitting a bug or request, please include a test-file or a
patch to an existing test-file that illustrates the bug or desired
feature.

# CONTRIBUTORS

- Damyan Ivanov <dmn@debian.org>
- Dave Rolsky <autarch@urth.org>
- Gabor Szabo <gabor@szabgab.com>
- Karen Etheridge <ether@cpan.org>
- Michael G. Schwern <schwern@pobox.com>
- Mike Doherty <doherty@cs.dal.ca>
- particle <particle@cpan.org>

# AUTHORS

- Graham Ollis <plicease@cpan.org>
- Caleb Cushing <xenoterracide@gmail.com>

# COPYRIGHT AND LICENSE

This software is Copyright (c) 2022 by Caleb Cushing.

This is free software, licensed under:

```
The Artistic License 2.0 (GPL Compatible)
```
