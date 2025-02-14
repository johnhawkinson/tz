# Contributing to the tz code and data

The time zone database is by no means authoritative: governments
change timekeeping rules erratically and sometimes with little
warning, the data entries do not cover all of civil time before
1970, and undoubtedly errors remain in the code and data.  Feel
free to fill gaps or fix mistakes, and please email improvements
to <tz@iana.org> for use in the future.  In your email, please give
reliable sources that reviewers can check.

## Contributing technical changes

To email small changes, please run a POSIX shell command like
`diff -u old/europe new/europe >myfix.patch`, and attach
`myfix.patch` to the email.

For more-elaborate or possibly-controversial changes,
such as renaming, adding or removing zones, please read
"[Theory and pragmatics of the tz code and
data](https://www.iana.org/time-zones/repository/theory.html)".
It is also good to browse the [mailing list
archives](https://mm.icann.org/pipermail/tz/) for examples of patches
that tend to work well.  Additions to data should contain commentary
citing reliable sources as justification.  Citations should use
"https:" URLs if available.

For changes that fix sensitive security-related bugs, please see the
distribution's `SECURITY` file.

Please submit changes against either the [latest release of the Time
Zone Database](https://www.iana.org/time-zones) or the main branch of
the development repository.  The latter is preferred.

## Sample Git workflow for developing contributions

If you use Git the following workflow may be helpful:

  * Copy the development repository.

		git clone https://github.com/eggert/tz.git
		cd tz

  * Get current with the main branch.

		git checkout main
		git pull

  * Switch to a new branch for the changes.  Choose a different
    branch name for each change set.

		git checkout -b mybranch

  * Sleuth by using `git blame`.  For example, when fixing data for
    Africa/Sao_Tome, if the command `git blame africa` outputs a line
    `2951fa3b (Paul Eggert 2018-01-08 09:03:13 -0800 1068) Zone
    Africa/Sao_Tome 0:26:56 - LMT 1884`, commit 2951fa3b should
    provide some justification for the `Zone Africa/Sao_Tome` line.

  * Edit source files.  Include commentary that justifies the
    changes by citing reliable sources.

  * Debug the changes, e.g.:

		make check
		make install
		./zdump -v America/Los_Angeles

  * For each separable change, commit it in the new branch, e.g.:

		git add northamerica
		git commit

    See recent `git log` output for the commit-message style.

  * Create patch files 0001-..., 0002-..., ...

		git format-patch main

  * After reviewing the patch files, send the patches to <tz@iana.org>
    for others to review.

		git send-email main

    For an archived example of such an email, see
    "[[tz] [PROPOSED] Fix off-by-1 error for Jamaica and T&C before
    1913](https://mm.icann.org/pipermail/tz/2018-February/026122.html)".

  * Start anew by getting current with the main branch again
    (the second step above).

Please do not create issues or pull requests on GitHub, as the
proper procedure for proposing and distributing patches is via
email as illustrated above.

-----

This file is in the public domain.
