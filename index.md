# Ten Simple Rules for Robustifying Your Software

* Morgan Taschuk (OICR)

> **Abstract**
>
> FIXME: abstract

FIXME: explain the problem.

* The difference between software running and being usable.
  * "Works for me on my machine" vs. "works for other people on a cluster I've never met".
* The "right" answer is to create a package on e.g. CPAN with full documentation and a set of regression tests.
  * But not everything worth doing is worth doing right.

How to tell if the software is working:

* Test in a 'vanilla' environment,
  such as another user's computer or a dummy account with none of the settings of the original developer.
* Test with different sizes of data:
  ridiculously small, small, medium, and large.
  The software should run on all sizes given some parameter tweaking,
  or fail with a sensible error message if the data is too big.
* Compare results from multiple iterations that have the same parameters and inputs.
  (See rule #8.)

## 1. Have a README that explains in a few lines what the software does and what its dependencies are.

* This is readable *before* the software is installed (or even downloaded).

## 2. Print usage information when launching from the command line that explains the software's features.

* And tells users where to find more information.

## 3. Do not require root or other special privileges.

## 4. Allow configuration of all major parameters from the command lines, including input files, thresholds, memory required, and other params.

* Configuration files are nice, but awkward to create on the fly when the tool is being run from shell scripts etc.

## 5. Eliminate hard-coded paths.

* Allow the user to set the name and location for the output files or results.
  * Common offenders: reference datasets, output directories.
* Corollary: do not require navigating to a particular directory to work,
  or operate on files only in the current working directory without allowing an override.
  * "Where I have to be" is just another hard-coded path.

## 6. Do not rely on launching software from the command line or by "shelling out" from a script.

* Common offenders: samtools, Picard tools, tabix.
* Those tools may not be installed, or may not be on the path.
* Some leniency here for Bash, R, Python, Java, Perl, and other tools that are included by default in Linux distributions.

## 7. Include a small test set that can be run to ensure the software is actually working.

* This is *not* to check that the software is working correctly (though that would be nice), just that it will actually run.

## 8. Produce identical results when given identical inputs.

* The test set isn't useful without this.
* And people won't be able to debug problems without it either.
* Common offender: random number generators
  * So require their seed as a parameter.
  * Or if the seed is set internally (e.g., using clocktime), echo it to the output for re-use later.

## 9. Do not rely on the pre-installation of non-standard packages or libraries, unless clearly defined in docs.

* Common offenders include a lot of Perl, R, and Python libraries, and user-local scripts.

## 10. Give the software a meaningful version number.

* Make it easy for users to figure out which version they actually have.
* Semantic versioning (and remember to change it on each release).
* Make the version number discoverable (e.g., echo it in usage).
