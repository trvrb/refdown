## Compile references from DOIs in a Markdown document

*This is currently only a spec.  Implementation forthcoming.*

This is a simple Ruby library / command-line tool that scans a Markdown document for DOI links and creates a references section using the [CrossRef](http://search.labs.crossref.org/) API.  Citations in Markdown should accomplish the following:

* Make sense in the plain text context.  This means not uglifying the text and being useful.
* Be self contained to the Markdown document.  I don't [pandoc's](http://johnmacfarlane.net/pandoc/) implementation for this reason.  It forces storing and keeping up-to-date a separate `.bib` references file.
* Easily compile to something submittable for publication.

This library takes the following Markdown syntax and transforms it.

## Example

### Before

*Inline-style links*

```md
Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna
aliqua [Bedford et al. 2010](http://dx.doi.org/10.1371/journal.ppat.1000918). Ut enim ad minim veniam, quis nostrud
exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in
voluptate velit esse cillum dolore eu fugiat nulla pariatur [Bedford and Hartl
2009](http://dx.doi.org/10.1073/pnas.0812009106). Excepteur sint occaecat cupidatat non proident, sunt in culpa qui
officia deserunt mollit anim id est laborum [Bedford et al. 2012](http://dx.doi.org/10.1186/1741-7007-10-38).
```

-----------

*Reference-style links*

```md
Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna
aliqua [Bedford et al. 2010]. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea
commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla 
pariatur [Bedford and Hartl 2009]. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt 
mollit anim id est laborum [Bedford et al. 2012].

- [Bedford et al. 2010]: http://dx.doi.org/10.1371/journal.ppat.1000918
- [Bedford and Hartl 2009]: http://dx.doi.org/10.1073/pnas.0812009106
- [Bedford et al. 2012]: http://dx.doi.org/10.1186/1741-7007-10-38
```

### After

Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua [[1]](#References). Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur [[2]](#References). Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum [[3]](#References).

#### References

1. [Bedford T, Cobey S, Beerli P, Pascual M. 2010. Global migration dynamics underlie evolution and persistence of human influenza A (H3N2). PLoS Pathog 6: e1000918.](http://dx.doi.org/10.1371/journal.ppat.1000918)
2. [Bedford T, Hartl DL. 2009. Optimization of gene expression by natural selection. Proc Natl Acad Sci USA 106: 1133-1138.](http://dx.doi.org/10.1073/pnas.0812009106)
3. [Bedford T, Rambaut A, Pascual M. 2012. Canalization of the evolutionary trajectory of the human influenza virus. BMC Biol 10: 38.](http://dx.doi.org/10.1186/1741-7007-10-38)

## Options

* Specify bibliography format using [Citation Style Language](http://citationstyles.org/) styles.
* Specify reference format, i.e. ^1, [1], or (Bedford et al. 2010).
