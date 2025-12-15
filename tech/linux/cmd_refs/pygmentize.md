# pygmentize

## See also
- [pip](./pip.md)
- [python](./python.md)
- [pytest](./pytest.md)

###### Syntax highlighted cat output using pygmentize
```bash
alias ccat='pygmentize -g -O style=manni'
```

###### And if you want line numbers (ugly):
```bash
alias ccat='pygmentize -g -O style=manni,linenos=1'
```

###### List available lexers
```bash
pygmentize -L
```

###### Force use a specific lexer
Usually this isn't necessary, as `-g` is pretty good at guessing. It even correctly guesses `bash` given a bash script with no file extension.
````bash
pygmentize -l bash -O style=manni
````

## pygmentize -h (help)
```
usage: pygmentize [-l LEXER | -g] [-F FILTER[:options]] [-f FORMATTER]
                  [-O OPTION=value[,OPTION=value,...]] [-P OPTION=value]
                  [-o OUTPUTFILE] [-v] [-s] [-x]
                  [-S STYLE -f formatter | -L [WHAT ...] | -N FILENAME | -C |
                  -H NAME TYPE | -V | -h] [-a ARG]
                  [INPUTFILE]

Highlight an input file and write the result to an output file.

Main operation:
  -l LEXER      Specify the lexer to use. (Query names with -L.) If not given
                and -g is not present, the lexer is guessed from the filename.
  -g            Guess the lexer from the file contents, or pass through as
                plain text if nothing can be guessed.
  -F FILTER[:options]
                Add a filter to the token stream. (Query names with -L.)
                Filter options are given after a colon if necessary.
  -f FORMATTER  Specify the formatter to use. (Query names with -L.) If not
                given, the formatter is guessed from the output filename, and
                defaults to the terminal formatter if the output is to the
                terminal or an unknown file extension.
  -O OPTION=value[,OPTION=value,...]
                Give options to the lexer and formatter as a comma-separated
                list of key-value pairs. Example: `-O bg=light,python=cool`.
  -P OPTION=value
                Give a single option to the lexer and formatter - with this
                you can pass options whose value contains commas and equal
                signs. Example: `-P "heading=Pygments, the Python
                highlighter"`.
  -o OUTPUTFILE
                Where to write the output. Defaults to standard output.
  INPUTFILE     Where to read the input. Defaults to standard input.

Operation flags:
  -v            Print a detailed traceback on unhandled exceptions, which is
                useful for debugging and bug reports.
  -s            Process lines one at a time until EOF, rather than waiting to
                process the entire file. This only works for stdin, only for
                lexers with no line-spanning constructs, and is intended for
                streaming input such as you get from `tail -f`. Example usage:
                `tail -f sql.log | pygmentize -s -l sql`.
  -x            Allow custom lexers and formatters to be loaded from a .py
                file relative to the current working directory. For example,
                `-l ./customlexer.py -x`. By default, this option expects a
                file with a class named CustomLexer or CustomFormatter; you
                can also specify your own class name with a colon (`-l
                ./lexer.py:MyLexer`). Users should be very careful not to use
                this option with untrusted files, because it will import and
                run them.

Special modes - do not do any highlighting:
  -S STYLE -f formatter
                Print style definitions for STYLE for a formatter given with
                -f. The argument given by -a is formatter dependent.
  -L [WHAT ...]
                List lexers, formatters, styles or filters -- give additional
                arguments for the thing(s) you want to list (e.g. "styles"),
                or omit them to list everything.
  -N FILENAME   Guess and print out a lexer name based solely on the given
                filename. Does not take input or highlight anything. If no
                specific lexer can be determined, "text" is printed.
  -C            Like -N, but print out a lexer name based solely on a given
                content from standard input.
  -H NAME TYPE  Print detailed help for the object <name> of type <type>,
                where <type> is one of "lexer", "formatter" or "filter".
  -V            Print the package version.
  -h, --help    Print this help.
  -a ARG        Formatter-specific additional argument for the -S (print style
                sheet) mode.

```

## pygementize -L (list lexers)
```
Pygments version 2.9.0, (c) 2006-2021 by Georg Brandl, Matthäus Chajdas and contributors.

Filters:
~~~~~~~~
* codetagify:
    Highlight special code tags in comments and docstrings.
* keywordcase:
    Convert keywords to lowercase or uppercase or capitalize them, which means first letter uppercase, rest lowercase.
* highlight:
    Highlight a normal Name (and Name.*) token with a different token type.
* raiseonerror:
    Raise an exception when the lexer generates an error token.
* whitespace:
    Convert tabs, newlines and/or spaces to visible characters.
* gobble:
    Gobbles source code lines (eats initial characters).
* tokenmerge:
    Merges consecutive tokens with the same token type in the output stream of a lexer.
* symbols:
    Convert mathematical symbols such as \<longrightarrow> in Isabelle or \longrightarrow in LaTeX into Unicode characters.

Formatters:
~~~~~~~~~~~
* bbcode, bb:
    Format tokens with BBcodes. These formatting codes are used by many bulletin boards, so you can highlight your sourcecode with pygments before posting it there. 
* bmp, bitmap:
    Create a bitmap image from source code. This uses the Python Imaging Library to generate a pixmap from the source code. (filenames *.bmp)
* gif:
    Create a GIF image from source code. This uses the Python Imaging Library to generate a pixmap from the source code. (filenames *.gif)
* html:
    Format tokens as HTML 4 ``<span>`` tags within a ``<pre>`` tag, wrapped in a ``<div>`` tag. The ``<div>``'s CSS class can be set by the `cssclass` option. (filenames *.html, *.htm)
* img, IMG, png:
    Create a PNG image from source code. This uses the Python Imaging Library to generate a pixmap from the source code. (filenames *.png)
* irc, IRC:
    Format tokens with IRC color sequences 
* jpg, jpeg:
    Create a JPEG image from source code. This uses the Python Imaging Library to generate a pixmap from the source code. (filenames *.jpg)
* latex, tex:
    Format tokens as LaTeX code. This needs the `fancyvrb` and `color` standard packages. (filenames *.tex)
* pango, pangomarkup:
    Format tokens as Pango Markup code. It can then be rendered to an SVG. 
* raw, tokens:
    Format tokens as a raw representation for storing token streams. (filenames *.raw)
* rtf:
    Format tokens as RTF markup. This formatter automatically outputs full RTF documents with color information and other useful stuff. Perfect for Copy and Paste into Microsoft(R) Word(R) documents. (filenames *.rtf)
* svg:
    Format tokens as an SVG graphics file.  This formatter is still experimental. Each line of code is a ``<text>`` element with explicit ``x`` and ``y`` coordinates containing ``<tspan>`` elements with the individual token styles. (filenames *.svg)
* terminal, console:
    Format tokens with ANSI color sequences, for output in a text console. Color sequences are terminated at newlines, so that paging the output works correctly. 
* terminal16m, console16m, 16m:
    Format tokens with ANSI color sequences, for output in a true-color terminal or console.  Like in `TerminalFormatter` color sequences are terminated at newlines, so that paging the output works correctly. 
* terminal256, console256, 256:
    Format tokens with ANSI color sequences, for output in a 256-color terminal or console.  Like in `TerminalFormatter` color sequences are terminated at newlines, so that paging the output works correctly. 
* testcase:
    Format tokens as appropriate for a new testcase. 
* text, null:
    Output the text unchanged without any formatting. (filenames *.txt)

Lexers:
~~~~~~~
* :
    JSONBareObject 
* :
    Raw token data 
* abap:
    ABAP (filenames *.abap, *.ABAP)
* abnf:
    ABNF (filenames *.abnf)
* actionscript, as:
    ActionScript (filenames *.as)
* actionscript3, as3:
    ActionScript 3 (filenames *.as)
* ada, ada95, ada2005:
    Ada (filenames *.adb, *.ads, *.ada)
* adl:
    ADL (filenames *.adl, *.adls, *.adlf, *.adlx)
* agda:
    Agda (filenames *.agda)
* aheui:
    Aheui (filenames *.aheui)
* alloy:
    Alloy (filenames *.als)
* ambienttalk, ambienttalk/2, at:
    AmbientTalk (filenames *.at)
* amdgpu:
    AMDGPU (filenames *.isa)
* ampl:
    Ampl (filenames *.run)
* ansys, apdl:
    ANSYS parametric design language (filenames *.ans)
* antlr-actionscript, antlr-as:
    ANTLR With ActionScript Target (filenames *.G, *.g)
* antlr-cpp:
    ANTLR With CPP Target (filenames *.G, *.g)
* antlr-csharp, antlr-c#:
    ANTLR With C# Target (filenames *.G, *.g)
* antlr-java:
    ANTLR With Java Target (filenames *.G, *.g)
* antlr-objc:
    ANTLR With ObjectiveC Target (filenames *.G, *.g)
* antlr-perl:
    ANTLR With Perl Target (filenames *.G, *.g)
* antlr-python:
    ANTLR With Python Target (filenames *.G, *.g)
* antlr-ruby, antlr-rb:
    ANTLR With Ruby Target (filenames *.G, *.g)
* antlr:
    ANTLR 
* apacheconf, aconf, apache:
    ApacheConf (filenames .htaccess, apache.conf, apache2.conf)
* apl:
    APL (filenames *.apl, *.aplf, *.aplo, *.apln, *.aplc, *.apli, *.dyalog)
* applescript:
    AppleScript (filenames *.applescript)
* arduino:
    Arduino (filenames *.ino)
* arrow:
    Arrow (filenames *.arw)
* aspectj:
    AspectJ (filenames *.aj)
* aspx-cs:
    aspx-cs (filenames *.aspx, *.asax, *.ascx, *.ashx, *.asmx, *.axd)
* aspx-vb:
    aspx-vb (filenames *.aspx, *.asax, *.ascx, *.ashx, *.asmx, *.axd)
* asymptote, asy:
    Asymptote (filenames *.asy)
* augeas:
    Augeas (filenames *.aug)
* autohotkey, ahk:
    autohotkey (filenames *.ahk, *.ahkl)
* autoit:
    AutoIt (filenames *.au3)
* awk, gawk, mawk, nawk:
    Awk (filenames *.awk)
* bare:
    BARE (filenames *.bare)
* basemake:
    Base Makefile 
* bash, sh, ksh, zsh, shell:
    Bash (filenames *.sh, *.ksh, *.bash, *.ebuild, *.eclass, *.exheres-0, *.exlib, *.zsh, .bashrc, bashrc, .bash_*, bash_*, zshrc, .zshrc, PKGBUILD)
* batch, bat, dosbatch, winbatch:
    Batchfile (filenames *.bat, *.cmd)
* bbcbasic:
    BBC Basic (filenames *.bbc)
* bbcode:
    BBCode 
* bc:
    BC (filenames *.bc)
* befunge:
    Befunge (filenames *.befunge)
* bibtex, bib:
    BibTeX (filenames *.bib)
* blitzbasic, b3d, bplus:
    BlitzBasic (filenames *.bb, *.decls)
* blitzmax, bmax:
    BlitzMax (filenames *.bmx)
* bnf:
    BNF (filenames *.bnf)
* boa:
    Boa (filenames *.boa)
* boo:
    Boo (filenames *.boo)
* boogie:
    Boogie (filenames *.bpl)
* brainfuck, bf:
    Brainfuck (filenames *.bf, *.b)
* bst, bst-pybtex:
    BST (filenames *.bst)
* bugs, winbugs, openbugs:
    BUGS (filenames *.bug)
* c-objdump:
    c-objdump (filenames *.c-objdump)
* c:
    C (filenames *.c, *.h, *.idc)
* ca65:
    ca65 assembler (filenames *.s)
* cadl:
    cADL (filenames *.cadl)
* camkes, idl4:
    CAmkES (filenames *.camkes, *.idl4)
* capdl:
    CapDL (filenames *.cdl)
* capnp:
    Cap'n Proto (filenames *.capnp)
* cbmbas:
    CBM BASIC V2 (filenames *.bas)
* cddl:
    CDDL (filenames *.cddl)
* ceylon:
    Ceylon (filenames *.ceylon)
* cfc:
    Coldfusion CFC (filenames *.cfc)
* cfengine3, cf3:
    CFEngine3 (filenames *.cf)
* cfm:
    Coldfusion HTML (filenames *.cfm, *.cfml)
* cfs:
    cfstatement 
* chaiscript, chai:
    ChaiScript (filenames *.chai)
* chapel, chpl:
    Chapel (filenames *.chpl)
* charmci:
    Charmci (filenames *.ci)
* cheetah, spitfire:
    Cheetah (filenames *.tmpl, *.spt)
* cirru:
    Cirru (filenames *.cirru)
* clay:
    Clay (filenames *.clay)
* clean:
    Clean (filenames *.icl, *.dcl)
* clojure, clj:
    Clojure (filenames *.clj)
* clojurescript, cljs:
    ClojureScript (filenames *.cljs)
* cmake:
    CMake (filenames *.cmake, CMakeLists.txt)
* cobol:
    COBOL (filenames *.cob, *.COB, *.cpy, *.CPY)
* cobolfree:
    COBOLFree (filenames *.cbl, *.CBL)
* coffeescript, coffee-script, coffee:
    CoffeeScript (filenames *.coffee)
* common-lisp, cl, lisp:
    Common Lisp (filenames *.cl, *.lisp)
* componentpascal, cp:
    Component Pascal (filenames *.cp, *.cps)
* console, shell-session:
    Bash Session (filenames *.sh-session, *.shell-session)
* coq:
    Coq (filenames *.v)
* cpp, c++:
    C++ (filenames *.cpp, *.hpp, *.c++, *.h++, *.cc, *.hh, *.cxx, *.hxx, *.C, *.H, *.cp, *.CPP)
* cpp-objdump, c++-objdumb, cxx-objdump:
    cpp-objdump (filenames *.cpp-objdump, *.c++-objdump, *.cxx-objdump)
* cpsa:
    CPSA (filenames *.cpsa)
* cr, crystal:
    Crystal (filenames *.cr)
* crmsh, pcmk:
    Crmsh (filenames *.crmsh, *.pcmk)
* croc:
    Croc (filenames *.croc)
* cryptol, cry:
    Cryptol (filenames *.cry)
* csharp, c#:
    C# (filenames *.cs)
* csound, csound-orc:
    Csound Orchestra (filenames *.orc, *.udo)
* csound-document, csound-csd:
    Csound Document (filenames *.csd)
* csound-score, csound-sco:
    Csound Score (filenames *.sco)
* css+django, css+jinja:
    CSS+Django/Jinja 
* css+genshitext, css+genshi:
    CSS+Genshi Text 
* css+lasso:
    CSS+Lasso 
* css+mako:
    CSS+Mako 
* css+mako:
    CSS+Mako 
* css+mozpreproc:
    CSS+mozpreproc (filenames *.css.in)
* css+myghty:
    CSS+Myghty 
* css+php:
    CSS+PHP 
* css+ruby, css+erb:
    CSS+Ruby 
* css+smarty:
    CSS+Smarty 
* css:
    CSS (filenames *.css)
* cuda, cu:
    CUDA (filenames *.cu, *.cuh)
* cypher:
    Cypher (filenames *.cyp, *.cypher)
* cython, pyx, pyrex:
    Cython (filenames *.pyx, *.pxd, *.pxi)
* d-objdump:
    d-objdump (filenames *.d-objdump)
* d:
    D (filenames *.d, *.di)
* dart:
    Dart (filenames *.dart)
* dasm16:
    DASM16 (filenames *.dasm16, *.dasm)
* debcontrol, control:
    Debian Control file (filenames control)
* debsources, sourceslist, sources.list:
    Debian Sourcelist (filenames sources.list)
* delphi, pas, pascal, objectpascal:
    Delphi (filenames *.pas, *.dpr)
* devicetree, dts:
    Devicetree (filenames *.dts, *.dtsi)
* dg:
    dg (filenames *.dg)
* diff, udiff:
    Diff (filenames *.diff, *.patch)
* django, jinja:
    Django/Jinja 
* docker, dockerfile:
    Docker (filenames Dockerfile, *.docker)
* doscon:
    MSDOS Session 
* dpatch:
    Darcs Patch (filenames *.dpatch, *.darcspatch)
* dtd:
    DTD (filenames *.dtd)
* duel, jbst, jsonml+bst:
    Duel (filenames *.duel, *.jbst)
* dylan-console, dylan-repl:
    Dylan session (filenames *.dylan-console)
* dylan-lid, lid:
    DylanLID (filenames *.lid, *.hdp)
* dylan:
    Dylan (filenames *.dylan, *.dyl, *.intr)
* earl-grey, earlgrey, eg:
    Earl Grey (filenames *.eg)
* easytrieve:
    Easytrieve (filenames *.ezt, *.mac)
* ebnf:
    EBNF (filenames *.ebnf)
* ec:
    eC (filenames *.ec, *.eh)
* ecl:
    ECL (filenames *.ecl)
* eiffel:
    Eiffel (filenames *.e)
* elixir, ex, exs:
    Elixir (filenames *.ex, *.eex, *.exs, *.leex)
* elm:
    Elm (filenames *.elm)
* emacs-lisp, elisp, emacs:
    EmacsLisp (filenames *.el)
* email, eml:
    E-mail (filenames *.eml)
* erb:
    ERB 
* erl:
    Erlang erl session (filenames *.erl-sh)
* erlang:
    Erlang (filenames *.erl, *.hrl, *.es, *.escript)
* evoque:
    Evoque (filenames *.evoque)
* execline:
    execline (filenames *.exec)
* extempore:
    xtlang (filenames *.xtm)
* ezhil:
    Ezhil (filenames *.n)
* factor:
    Factor (filenames *.factor)
* fan:
    Fantom (filenames *.fan)
* fancy, fy:
    Fancy (filenames *.fy, *.fancypack)
* felix, flx:
    Felix (filenames *.flx, *.flxh)
* fennel, fnl:
    Fennel (filenames *.fnl)
* fish, fishshell:
    Fish (filenames *.fish, *.load)
* flatline:
    Flatline 
* floscript, flo:
    FloScript (filenames *.flo)
* forth:
    Forth (filenames *.frt, *.fs)
* fortran:
    Fortran (filenames *.f03, *.f90, *.F03, *.F90)
* fortranfixed:
    FortranFixed (filenames *.f, *.F)
* foxpro, vfp, clipper, xbase:
    FoxPro (filenames *.PRG, *.prg)
* freefem:
    Freefem (filenames *.edp)
* fsharp, f#:
    F# (filenames *.fs, *.fsi)
* fstar:
    FStar (filenames *.fst, *.fsti)
* futhark:
    Futhark (filenames *.fut)
* gap:
    GAP (filenames *.g, *.gd, *.gi, *.gap)
* gas, asm:
    GAS (filenames *.s, *.S)
* gcode:
    g-code (filenames *.gcode)
* gdscript, gd:
    GDScript (filenames *.gd)
* genshi, kid, xml+genshi, xml+kid:
    Genshi (filenames *.kid)
* genshitext:
    Genshi Text 
* gherkin, cucumber:
    Gherkin (filenames *.feature)
* glsl:
    GLSL (filenames *.vert, *.frag, *.geo)
* gnuplot:
    Gnuplot (filenames *.plot, *.plt)
* go:
    Go (filenames *.go)
* golo:
    Golo (filenames *.golo)
* gooddata-cl:
    GoodData-CL (filenames *.gdc)
* gosu:
    Gosu (filenames *.gs, *.gsx, *.gsp, *.vark)
* graphviz, dot:
    Graphviz (filenames *.gv, *.dot)
* groff, nroff, man:
    Groff (filenames *.[1234567], *.man)
* groovy:
    Groovy (filenames *.groovy, *.gradle)
* gst:
    Gosu Template (filenames *.gst)
* haml:
    Haml (filenames *.haml)
* handlebars:
    Handlebars 
* haskell, hs:
    Haskell (filenames *.hs)
* haxe, hxsl, hx:
    Haxe (filenames *.hx, *.hxsl)
* haxeml, hxml:
    Hxml (filenames *.hxml)
* hexdump:
    Hexdump 
* hlsl:
    HLSL (filenames *.hlsl, *.hlsli)
* hsail, hsa:
    HSAIL (filenames *.hsail)
* hspec:
    Hspec 
* html+cheetah, html+spitfire, htmlcheetah:
    HTML+Cheetah 
* html+django, html+jinja, htmldjango:
    HTML+Django/Jinja 
* html+evoque:
    HTML+Evoque (filenames *.html)
* html+genshi, html+kid:
    HTML+Genshi 
* html+handlebars:
    HTML+Handlebars (filenames *.handlebars, *.hbs)
* html+lasso:
    HTML+Lasso 
* html+mako:
    HTML+Mako 
* html+mako:
    HTML+Mako 
* html+myghty:
    HTML+Myghty 
* html+ng2:
    HTML + Angular2 (filenames *.ng2)
* html+php:
    HTML+PHP (filenames *.phtml)
* html+smarty:
    HTML+Smarty 
* html+twig:
    HTML+Twig (filenames *.twig)
* html+velocity:
    HTML+Velocity 
* html:
    HTML (filenames *.html, *.htm, *.xhtml, *.xslt)
* http:
    HTTP 
* hybris, hy:
    Hybris (filenames *.hy, *.hyb)
* hylang:
    Hy (filenames *.hy)
* i6t:
    Inform 6 template (filenames *.i6t)
* icon:
    Icon (filenames *.icon, *.ICON)
* idl:
    IDL (filenames *.pro)
* idris, idr:
    Idris (filenames *.idr)
* iex:
    Elixir iex session 
* igor, igorpro:
    Igor (filenames *.ipf)
* inform6, i6:
    Inform 6 (filenames *.inf)
* inform7, i7:
    Inform 7 (filenames *.ni, *.i7x)
* ini, cfg, dosini:
    INI (filenames *.ini, *.cfg, *.inf)
* io:
    Io (filenames *.io)
* ioke, ik:
    Ioke (filenames *.ik)
* ipython2, ipython:
    IPython 
* ipython3:
    IPython3 
* ipythonconsole:
    IPython console session 
* irc:
    IRC logs (filenames *.weechatlog)
* isabelle:
    Isabelle (filenames *.thy)
* j:
    J (filenames *.ijs)
* jags:
    JAGS (filenames *.jag, *.bug)
* jasmin, jasminxt:
    Jasmin (filenames *.j)
* java:
    Java (filenames *.java)
* javascript+cheetah, js+cheetah, javascript+spitfire, js+spitfire:
    JavaScript+Cheetah 
* javascript+django, js+django, javascript+jinja, js+jinja:
    JavaScript+Django/Jinja 
* javascript+lasso, js+lasso:
    JavaScript+Lasso 
* javascript+mako, js+mako:
    JavaScript+Mako 
* javascript+mozpreproc:
    Javascript+mozpreproc (filenames *.js.in)
* javascript+myghty, js+myghty:
    JavaScript+Myghty 
* javascript+php, js+php:
    JavaScript+PHP 
* javascript+ruby, js+ruby, javascript+erb, js+erb:
    JavaScript+Ruby 
* javascript+smarty, js+smarty:
    JavaScript+Smarty 
* javascript, js:
    JavaScript (filenames *.js, *.jsm, *.mjs, *.cjs)
* jcl:
    JCL (filenames *.jcl)
* jlcon, julia-repl:
    Julia console 
* js+genshitext, js+genshi, javascript+genshitext, javascript+genshi:
    JavaScript+Genshi Text 
* js+mako, javascript+mako:
    JavaScript+Mako 
* jsgf:
    JSGF (filenames *.jsgf)
* json, json-object:
    JSON (filenames *.json, Pipfile.lock)
* jsonld, json-ld:
    JSON-LD (filenames *.jsonld)
* jsp:
    Java Server Page (filenames *.jsp)
* julia, jl:
    Julia (filenames *.jl)
* juttle:
    Juttle (filenames *.juttle)
* kal:
    Kal (filenames *.kal)
* kconfig, menuconfig, linux-config, kernel-config:
    Kconfig (filenames Kconfig*, *Config.in*, external.in*, standard-modules.in)
* kmsg, dmesg:
    Kernel log (filenames *.kmsg, *.dmesg)
* koka:
    Koka (filenames *.kk, *.kki)
* kotlin:
    Kotlin (filenames *.kt, *.kts)
* kuin:
    Kuin (filenames *.kn)
* lasso, lassoscript:
    Lasso (filenames *.lasso, *.lasso[89])
* lean:
    Lean (filenames *.lean)
* less:
    LessCss (filenames *.less)
* lighttpd, lighty:
    Lighttpd configuration file (filenames lighttpd.conf)
* limbo:
    Limbo (filenames *.b)
* liquid:
    liquid (filenames *.liquid)
* literate-agda, lagda:
    Literate Agda (filenames *.lagda)
* literate-cryptol, lcryptol, lcry:
    Literate Cryptol (filenames *.lcry)
* literate-haskell, lhaskell, lhs:
    Literate Haskell (filenames *.lhs)
* literate-idris, lidris, lidr:
    Literate Idris (filenames *.lidr)
* livescript, live-script:
    LiveScript (filenames *.ls)
* llvm-mir-body:
    LLVM-MIR Body 
* llvm-mir:
    LLVM-MIR (filenames *.mir)
* llvm:
    LLVM (filenames *.ll)
* logos:
    Logos (filenames *.x, *.xi, *.xm, *.xmi)
* logtalk:
    Logtalk (filenames *.lgt, *.logtalk)
* lsl:
    LSL (filenames *.lsl)
* lua:
    Lua (filenames *.lua, *.wlua)
* make, makefile, mf, bsdmake:
    Makefile (filenames *.mak, *.mk, Makefile, makefile, Makefile.*, GNUmakefile)
* mako:
    Mako (filenames *.mao)
* mako:
    Mako (filenames *.mao)
* maql:
    MAQL (filenames *.maql)
* markdown, md:
    Markdown (filenames *.md, *.markdown)
* mask:
    Mask (filenames *.mask)
* mason:
    Mason (filenames *.m, *.mhtml, *.mc, *.mi, autohandler, dhandler)
* mathematica, mma, nb:
    Mathematica (filenames *.nb, *.cdf, *.nbp, *.ma)
* matlab:
    Matlab (filenames *.m)
* matlabsession:
    Matlab session 
* mime:
    MIME 
* minid:
    MiniD 
* miniscript, ms:
    MiniScript (filenames *.ms)
* modelica:
    Modelica (filenames *.mo)
* modula2, m2:
    Modula-2 (filenames *.def, *.mod)
* monkey:
    Monkey (filenames *.monkey)
* monte:
    Monte (filenames *.mt)
* moocode, moo:
    MOOCode (filenames *.moo)
* moonscript, moon:
    MoonScript (filenames *.moon)
* mosel:
    Mosel (filenames *.mos)
* mozhashpreproc:
    mozhashpreproc 
* mozpercentpreproc:
    mozpercentpreproc 
* mql, mq4, mq5, mql4, mql5:
    MQL (filenames *.mq4, *.mq5, *.mqh)
* mscgen, msc:
    Mscgen (filenames *.msc)
* mupad:
    MuPAD (filenames *.mu)
* mxml:
    MXML (filenames *.mxml)
* myghty:
    Myghty (filenames *.myt, autodelegate)
* mysql:
    MySQL 
* nasm:
    NASM (filenames *.asm, *.ASM)
* ncl:
    NCL (filenames *.ncl)
* nemerle:
    Nemerle (filenames *.n)
* nesc:
    nesC (filenames *.nc)
* nestedtext, nt:
    NestedText (filenames *.nt)
* newlisp:
    NewLisp (filenames *.lsp, *.nl, *.kif)
* newspeak:
    Newspeak (filenames *.ns2)
* ng2:
    Angular2 
* nginx:
    Nginx configuration file (filenames nginx.conf)
* nimrod, nim:
    Nimrod (filenames *.nim, *.nimrod)
* nit:
    Nit (filenames *.nit)
* nixos, nix:
    Nix (filenames *.nix)
* notmuch:
    Notmuch 
* nsis, nsi, nsh:
    NSIS (filenames *.nsi, *.nsh)
* numpy:
    NumPy 
* nusmv:
    NuSMV (filenames *.smv)
* objdump-nasm:
    objdump-nasm (filenames *.objdump-intel)
* objdump:
    objdump (filenames *.objdump)
* objective-c++, objectivec++, obj-c++, objc++:
    Objective-C++ (filenames *.mm, *.hh)
* objective-c, objectivec, obj-c, objc:
    Objective-C (filenames *.m, *.h)
* objective-j, objectivej, obj-j, objj:
    Objective-J (filenames *.j)
* ocaml:
    OCaml (filenames *.ml, *.mli, *.mll, *.mly)
* octave:
    Octave (filenames *.m)
* odin:
    ODIN (filenames *.odin)
* omg-idl:
    OMG Interface Definition Language (filenames *.idl, *.pidl)
* ooc:
    Ooc (filenames *.ooc)
* opa:
    Opa (filenames *.opa)
* openedge, abl, progress:
    OpenEdge ABL (filenames *.p, *.cls)
* pacmanconf:
    PacmanConf (filenames pacman.conf)
* pan:
    Pan (filenames *.pan)
* parasail:
    ParaSail (filenames *.psi, *.psl)
* pawn:
    Pawn (filenames *.p, *.pwn, *.inc)
* peg:
    PEG (filenames *.peg)
* perl, pl:
    Perl (filenames *.pl, *.pm, *.t, *.perl)
* perl6, pl6, raku:
    Perl6 (filenames *.pl, *.pm, *.nqp, *.p6, *.6pl, *.p6l, *.pl6, *.6pm, *.p6m, *.pm6, *.t, *.raku, *.rakumod, *.rakutest, *.rakudoc)
* php, php3, php4, php5:
    PHP (filenames *.php, *.php[345], *.inc)
* pig:
    Pig (filenames *.pig)
* pike:
    Pike (filenames *.pike, *.pmod)
* pkgconfig:
    PkgConfig (filenames *.pc)
* plpgsql:
    PL/pgSQL 
* pointless:
    Pointless (filenames *.ptls)
* pony:
    Pony (filenames *.pony)
* postgresql, postgres:
    PostgreSQL SQL dialect 
* postscript, postscr:
    PostScript (filenames *.ps, *.eps)
* pot, po:
    Gettext Catalog (filenames *.pot, *.po)
* pov:
    POVRay (filenames *.pov, *.inc)
* powershell, posh, ps1, psm1:
    PowerShell (filenames *.ps1, *.psm1)
* praat:
    Praat (filenames *.praat, *.proc, *.psc)
* prolog:
    Prolog (filenames *.ecl, *.prolog, *.pro, *.pl)
* promql:
    PromQL (filenames *.promql)
* properties, jproperties:
    Properties (filenames *.properties)
* protobuf, proto:
    Protocol Buffer (filenames *.proto)
* ps1con:
    PowerShell Session 
* psql, postgresql-console, postgres-console:
    PostgreSQL console (psql) 
* psysh:
    PsySH console session for PHP 
* pug, jade:
    Pug (filenames *.pug, *.jade)
* puppet:
    Puppet (filenames *.pp)
* py2tb:
    Python 2.x Traceback (filenames *.py2tb)
* pycon:
    Python console session 
* pypylog, pypy:
    PyPy Log (filenames *.pypylog)
* pytb, py3tb:
    Python Traceback (filenames *.pytb, *.py3tb)
* python, py, sage, python3, py3:
    Python (filenames *.py, *.pyw, *.jy, *.sage, *.sc, SConstruct, SConscript, *.bzl, BUCK, BUILD, BUILD.bazel, WORKSPACE, *.tac)
* python2, py2:
    Python 2.x 
* qbasic, basic:
    QBasic (filenames *.BAS, *.bas)
* qml, qbs:
    QML (filenames *.qml, *.qbs)
* qvto, qvt:
    QVTO (filenames *.qvto)
* racket, rkt:
    Racket (filenames *.rkt, *.rktd, *.rktl)
* ragel-c:
    Ragel in C Host (filenames *.rl)
* ragel-cpp:
    Ragel in CPP Host (filenames *.rl)
* ragel-d:
    Ragel in D Host (filenames *.rl)
* ragel-em:
    Embedded Ragel (filenames *.rl)
* ragel-java:
    Ragel in Java Host (filenames *.rl)
* ragel-objc:
    Ragel in Objective C Host (filenames *.rl)
* ragel-ruby, ragel-rb:
    Ragel in Ruby Host (filenames *.rl)
* ragel:
    Ragel 
* rbcon, irb:
    Ruby irb session 
* rconsole, rout:
    RConsole (filenames *.Rout)
* rd:
    Rd (filenames *.Rd)
* reasonml, reason:
    ReasonML (filenames *.re, *.rei)
* rebol:
    REBOL (filenames *.r, *.r3, *.reb)
* red, red/system:
    Red (filenames *.red, *.reds)
* redcode:
    Redcode (filenames *.cw)
* registry:
    reg (filenames *.reg)
* resourcebundle, resource:
    ResourceBundle 
* restructuredtext, rst, rest:
    reStructuredText (filenames *.rst, *.rest)
* rexx, arexx:
    Rexx (filenames *.rexx, *.rex, *.rx, *.arexx)
* rhtml, html+erb, html+ruby:
    RHTML (filenames *.rhtml)
* ride:
    Ride (filenames *.ride)
* rng-compact, rnc:
    Relax-NG Compact (filenames *.rnc)
* roboconf-graph:
    Roboconf Graph (filenames *.graph)
* roboconf-instances:
    Roboconf Instances (filenames *.instances)
* robotframework:
    RobotFramework (filenames *.robot)
* rql:
    RQL (filenames *.rql)
* rsl:
    RSL (filenames *.rsl)
* ruby, rb, duby:
    Ruby (filenames *.rb, *.rbw, Rakefile, *.rake, *.gemspec, *.rbx, *.duby, Gemfile)
* rust, rs:
    Rust (filenames *.rs, *.rs.in)
* sarl:
    SARL (filenames *.sarl)
* sas:
    SAS (filenames *.SAS, *.sas)
* sass:
    Sass (filenames *.sass)
* scala:
    Scala (filenames *.scala)
* scaml:
    Scaml (filenames *.scaml)
* scdoc, scd:
    scdoc (filenames *.scd, *.scdoc)
* scheme, scm:
    Scheme (filenames *.scm, *.ss)
* scilab:
    Scilab (filenames *.sci, *.sce, *.tst)
* scss:
    SCSS (filenames *.scss)
* sgf:
    SmartGameFormat (filenames *.sgf)
* shen:
    Shen (filenames *.shen)
* shexc, shex:
    ShExC (filenames *.shex)
* sieve:
    Sieve (filenames *.siv, *.sieve)
* silver:
    Silver (filenames *.sil, *.vpr)
* singularity:
    Singularity (filenames *.def, Singularity)
* slash:
    Slash (filenames *.sla)
* slim:
    Slim (filenames *.slim)
* slurm, sbatch:
    Slurm (filenames *.sl)
* smali:
    Smali (filenames *.smali)
* smalltalk, squeak, st:
    Smalltalk (filenames *.st)
* smarty:
    Smarty (filenames *.tpl)
* sml:
    Standard ML (filenames *.sml, *.sig, *.fun)
* snobol:
    Snobol (filenames *.snobol)
* snowball:
    Snowball (filenames *.sbl)
* solidity:
    Solidity (filenames *.sol)
* sp:
    SourcePawn (filenames *.sp)
* sparql:
    SPARQL (filenames *.rq, *.sparql)
* spec:
    RPMSpec (filenames *.spec)
* splus, s, r:
    S (filenames *.S, *.R, .Rhistory, .Rprofile, .Renviron)
* sql:
    SQL (filenames *.sql)
* sqlite3:
    sqlite3con (filenames *.sqlite3-console)
* squidconf, squid.conf, squid:
    SquidConf (filenames squid.conf)
* ssp:
    Scalate Server Page (filenames *.ssp)
* stan:
    Stan (filenames *.stan)
* stata, do:
    Stata (filenames *.do, *.ado)
* supercollider, sc:
    SuperCollider (filenames *.sc, *.scd)
* swift:
    Swift (filenames *.swift)
* swig:
    SWIG (filenames *.swg, *.i)
* systemverilog, sv:
    systemverilog (filenames *.sv, *.svh)
* tads3:
    TADS 3 (filenames *.t)
* tap:
    TAP (filenames *.tap)
* tasm:
    TASM (filenames *.asm, *.ASM, *.tasm)
* tcl:
    Tcl (filenames *.tcl, *.rvt)
* tcsh, csh:
    Tcsh (filenames *.tcsh, *.csh)
* tcshcon:
    Tcsh Session 
* tea:
    Tea (filenames *.tea)
* teal:
    teal (filenames *.teal)
* teratermmacro, teraterm, ttl:
    Tera Term macro (filenames *.ttl)
* termcap:
    Termcap (filenames termcap, termcap.src)
* terminfo:
    Terminfo (filenames terminfo, terminfo.src)
* terraform, tf:
    Terraform (filenames *.tf)
* tex, latex:
    TeX (filenames *.tex, *.aux, *.toc)
* text:
    Text only (filenames *.txt)
* thrift:
    Thrift (filenames *.thrift)
* ti, thingsdb:
    ThingsDB (filenames *.ti)
* tid:
    tiddler (filenames *.tid)
* tnt:
    Typographic Number Theory (filenames *.tnt)
* todotxt:
    Todotxt (filenames todo.txt, *.todotxt)
* toml:
    TOML (filenames *.toml, Pipfile, poetry.lock)
* trac-wiki, moin:
    MoinMoin/Trac Wiki markup 
* trafficscript, rts:
    TrafficScript (filenames *.rts)
* treetop:
    Treetop (filenames *.treetop, *.tt)
* tsql, t-sql:
    Transact-SQL (filenames *.sql)
* turtle:
    Turtle (filenames *.ttl)
* twig:
    Twig 
* typescript, ts:
    TypeScript (filenames *.ts, *.tsx)
* typoscript:
    TypoScript (filenames *.typoscript)
* typoscriptcssdata:
    TypoScriptCssData 
* typoscripthtmldata:
    TypoScriptHtmlData 
* ucode:
    ucode (filenames *.u, *.u1, *.u2)
* unicon:
    Unicon (filenames *.icn)
* urbiscript:
    UrbiScript (filenames *.u)
* usd, usda:
    USD (filenames *.usd, *.usda)
* vala, vapi:
    Vala (filenames *.vala, *.vapi)
* vb.net, vbnet:
    VB.net (filenames *.vb, *.bas)
* vbscript:
    VBScript (filenames *.vbs, *.VBS)
* vcl:
    VCL (filenames *.vcl)
* vclsnippets, vclsnippet:
    VCLSnippets 
* vctreestatus:
    VCTreeStatus 
* velocity:
    Velocity (filenames *.vm, *.fhtml)
* verilog, v:
    verilog (filenames *.v)
* vgl:
    VGL (filenames *.rpf)
* vhdl:
    vhdl (filenames *.vhdl, *.vhd)
* vim:
    VimL (filenames *.vim, .vimrc, .exrc, .gvimrc, _vimrc, _exrc, _gvimrc, vimrc, gvimrc)
* wast, wat:
    WebAssembly (filenames *.wat, *.wast)
* wdiff:
    WDiff (filenames *.wdiff)
* webidl:
    Web IDL (filenames *.webidl)
* whiley:
    Whiley (filenames *.whiley)
* x10, xten:
    X10 (filenames *.x10)
* xml+cheetah, xml+spitfire:
    XML+Cheetah 
* xml+django, xml+jinja:
    XML+Django/Jinja 
* xml+evoque:
    XML+Evoque (filenames *.xml)
* xml+lasso:
    XML+Lasso 
* xml+mako:
    XML+Mako 
* xml+mako:
    XML+Mako 
* xml+myghty:
    XML+Myghty 
* xml+php:
    XML+PHP 
* xml+ruby, xml+erb:
    XML+Ruby 
* xml+smarty:
    XML+Smarty 
* xml+velocity:
    XML+Velocity 
* xml:
    XML (filenames *.xml, *.xsl, *.rss, *.xslt, *.xsd, *.wsdl, *.wsf)
* xorg.conf:
    Xorg (filenames xorg.conf)
* xquery, xqy, xq, xql, xqm:
    XQuery (filenames *.xqy, *.xquery, *.xq, *.xql, *.xqm)
* xslt:
    XSLT (filenames *.xsl, *.xslt, *.xpl)
* xtend:
    Xtend (filenames *.xtend)
* xul+mozpreproc:
    XUL+mozpreproc (filenames *.xul.in)
* yaml+jinja, salt, sls:
    YAML+Jinja (filenames *.sls)
* yaml:
    YAML (filenames *.yaml, *.yml)
* yang:
    YANG (filenames *.yang)
* zeek, bro:
    Zeek (filenames *.zeek, *.bro)
* zephir:
    Zephir (filenames *.zep)
* zig:
    Zig (filenames *.zig)

Styles:
~~~~~~~
* default:
    The default style (inspired by Emacs 22).
* emacs:
    The default style (inspired by Emacs 22).
* friendly:
    A modern style based on the VIM pyte theme.
* colorful:
    A colorful style, inspired by CodeRay.
* autumn:
    A colorful style, inspired by the terminal highlighting style.
* murphy:
    Murphy's style from CodeRay.
* manni:
    A colorful style, inspired by the terminal highlighting style.
* material:
    This style mimics the Material Theme color scheme.
* monokai:
    This style mimics the Monokai color scheme.
* perldoc:
    Style similar to the style used in the perldoc code blocks.
* pastie:
    Style similar to the pastie default style.
* borland:
    Style similar to the style used in the borland IDEs.
* trac:
    Port of the default trac highlighter design.
* native:
    Pygments version of the "native" vim theme.
* fruity:
    Pygments version of the "native" vim theme.
* bw:
    
* vim:
    Styles somewhat like vim 7.0
* vs:
    
* tango:
    The Crunchy default Style inspired from the color palette from the Tango Icon Theme Guidelines.
* rrt:
    Minimalistic "rrt" theme, based on Zap and Emacs defaults.
* xcode:
    Style similar to the Xcode default colouring theme.
* igor:
    Pygments version of the official colors for Igor Pro procedures.
* paraiso-light:
    
* paraiso-dark:
    
* lovelace:
    The style used in Lovelace interactive learning environment. Tries to avoid the "angry fruit salad" effect with desaturated and dim colours.
* algol:
    
* algol_nu:
    
* arduino:
    The Arduino® language style. This style is designed to highlight the Arduino source code, so exepect the best results with it.
* rainbow_dash:
    A bright and colorful syntax highlighting theme.
* abap:
    
* solarized-dark:
    The solarized style, dark.
* solarized-light:
    The solarized style, light.
* sas:
    Style inspired by SAS' enhanced program editor. Note This is not meant to be a complete style. It's merely meant to mimic SAS' program editor syntax highlighting.
* stata:
    Light mode style inspired by Stata's do-file editor. This is not meant to be a complete style, just for use with Stata.
* stata-light:
    Light mode style inspired by Stata's do-file editor. This is not meant to be a complete style, just for use with Stata.
* stata-dark:
    
* inkpot:
    
* zenburn:
    Low contrast Zenburn style.
* gruvbox-dark:
    Pygments version of the "gruvbox" dark vim theme.
* gruvbox-light:
    Pygments version of the "gruvbox" Light vim theme.

```