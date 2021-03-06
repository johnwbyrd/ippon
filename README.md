<link rel="stylesheet" href="http://jasonm23.github.io/markdown-css-themes/foghorn.css">
</link>

![Superpawn logo designed by Angela M. Eads](http://chess.johnbyrd.org/logo/logo-medium.jpg "Superpawn logo designed by Angela M. Eads")

Superpawn
=========

Superpawn is an experimental C++ [chess engine](http://en.wikipedia.org/wiki/Chess_engine) 
which should not be taken very seriously.  Superpawn uses the [Universal Chess Interface](http://en.wikipedia.org/wiki/Universal_Chess_Interface)
protocol in order to communicate with a [compatible graphical user interface](http://www.playwitharena.com/) of 
your choice.

The latest build of [Superpawn](http://chess.johnbyrd.org) can always be downloaded
from [http://chess.johnbyrd.org](http://chess.johnbyrd.org) .

Downloads
---------

[Windows x86 executable](http://chess.johnbyrd.org/build/win/x86/superpawn-windows-x32.zip).  If
you don't know which file to download, this one is probably it.

[Windows x64 executable](http://chess.johnbyrd.org/build/win/x64/superpawn-windows-x64.zip).  Slightly 
faster for x64 machines.

[Source code](http://www.github.com/johnwbyrd/superpawn).  For building on arbitrary Macintosh and 
Linux boxes.  The [Travis](https://travis-ci.org/johnwbyrd/superpawn) build system currently reports
Superpawn's build status as:
[![Build Status](https://travis-ci.org/johnwbyrd/superpawn.svg?branch=master)](https://travis-ci.org/johnwbyrd/superpawn)

Description
-----------

Superpawn is capable of making many fascinating chess moves, many
of which are legal.  It beats its author handily at the game,
which is not terribly surprising since its author is a lifelong patzer.

Superpawn is an excellent example of the "objects gone wild" style of
programming, in which Everything Is An Object.  Even the pieces themselves
are objects; they know how to move, capture, etc.  This of course slows 
down the move generation and evaluation process immensely, making this 
program irredeemably slow in tournament conditions.  However, its logic
is easy to follow and extend as you see fit.

Superpawn requires a [C++11](http://en.wikipedia.org/wiki/C%2B%2B11) compiler
with support for threading.  It builds and runs on Windows, Linux and MacOS systems, 
and  compiles under Microsoft, gcc and clang compilers.  A [CMake](http://www.cmake.org/)
implementation is provided to ease compilation on arbitrary targets.

If you are compiling with gcc, Superpawn requires gcc 3.8.2 or higher to compile.
Earlier versions don't support all C++11 features, and your compilation will fail.

Building on Windows
-------------------

To attempt a Windows build, from the root directory of the installation type:

    tools\win32\make\build.bat

Test suite
----------

Superpawn includes a simple test suite that uses the [cutechess-cli](https://chessprogramming.wikispaces.com/Cutechess-cli) application
to run a series of tests against existing chess engines.  Superpawn currently
loses handily to most of them.  The test suite currently runs on Windows
platforms only but could be modified to run on other platforms.

The core of the test suite is a Lua script that enumerates all currently
existing chess engines in the tools\engines subdirectory, and uses
the cutechess-cli application to launch a gauntlet test against Superpawn.
The results of the gauntlet are automatically stored in the build\tests
subdirectory.

To build and run against the test gauntlet, run the following on a Windows 
box from the root directory:

    tools\win32\make\build --TESTS

As of this writing, I test against specific Windows builds of the following engines:

- [ACE](https://code.google.com/p/ace-chess/)
- [DesasterArea](http://desasterarea.jimdo.com/)
- [Dika](http://kirr.homeunix.org/chess/engines/Norbert%27s%20collection/Dika%20v0.4209/)
- [GiuChess](https://chessprogramming.wikispaces.com/GiuChess)
- [Piranha](http://www.villwock.com/piranha/)
- [Senpai](https://chessprogramming.wikispaces.com/Senpai)
- [Stockfish](https://stockfishchess.org/)
- [Tarrasch Toy Engine](http://www.triplehappy.com/)
- [Testina](http://www.g-sei.org/testina/) 
- [TSCP](http://www.tckerrigan.com/chess/tscp) 

I make no proprietary claim for cutechess-cli or any of the included chess engines except Superpawn.  If you don't want me to test against your engine or include it in github, let me know and I'll happily delete it from the repository.

Information on recent gauntlet results, including 
[PGN](http://en.wikipedia.org/wiki/Portable_Game_Notation) format games
and their [elostat](http://www.playwitharena.com/?User_Files%2C_Engines:Axon%2C_EloStat%2C_Nalimov:EloStat) analyses, may be online
[here](http://chess.johnbyrd.org/tests).

Raspberry Pi
------------

Superpawn has been demonstrated to work, excruciatingly slowly, on the 
[Raspberry Pi](http://www.raspberrypi.org) embeddable computer.  However, most graphical user interfaces for 
chess on the Pi utilize the older [xboard](http://www.gnu.org/software/xboard/engine-intf.html)
protocol, while Superpawn uses the [Universal Chess Interface](http://en.wikipedia.org/wiki/Universal_Chess_Interface)
protocol.  This can be worked around by installing and using [Polyglot](http://wbec-ridderkerk.nl/html/details1/PolyGlot.html) to launch Superpawn.
A sample polyglot.ini for the Raspberry Pi is included with this 
distribution.  This configuration works well with the eboard graphical
user interface on the Pi.
 
You will need to have gcc 3.8.2 or higher installed on the Pi.  As of this
writing, instructions for updating the Pi from older compilers are [here](http://somewideopenspace.wordpress.com/2014/02/28/gcc-4-8-on-raspberry-pi-wheezy/).

Genesis
-------

When my wife Amanda was very small, her older sister made her play chess.
Although her older sister was quite serious at the chessboard, Amanda quickly tired
of the slow game.  Eventually Amanda would grab a pawn and yell 
"It's SUUUUPERPAWWWWWN!" and whoosh it around, knocking all the other
pieces off the board.  This is the basic strategic and evaluation methodology that 
I have attempted to incorporate into this chess engine.

Features
--------

- ANSI C++11 code
- Compiles under Microsoft Visual Studio 2013, gcc 3.8.2, AppleClang 5.1.0,
  and clang 3.3
- Implements a subset of UCI protocol sufficient to permit play 
  with Arena 3.0+, Tarrasch Chess GUI, Fritz GUI, cutechess-cli and others
- Pluggable architecture permits easy experimentation with 
  new algorithms for search and evaluation  
- Principal variation search
- Basic material evaluator
- Basic mobility evaluator
- Gratuitous functional programming
- All the code exists within a single C++ source file
- Vaguely sort of const-correct
- Compiles cleanly in 32-bit and 64-bit modes
- Compatible with cmake build systems
- Simple test framework based on [cutechess-cli](http://cutechess.com/)
- Castling, stalemate, fifty move rule, and draw by repetition
- Reports distance to mate
- Basic time management controls
- Basic transposition table

Things it doesn't do
--------------------

- Take castling into account in computing hashes
- Understand pawn structure
- Better endgame logic for say KRK and KQK.  Superpawn is currently perfectly capable
  of throwing easily winnable endgames.
- Play chess well

License
-------

Source code is provided under the [Creative Commons 3.0 Attribution 
Unported](http://creativecommons.org/licenses/by/3.0/deed.en_US) license.  Please
don't pass off this chess engine as your own work.

Feel free to contact or ridicule the author at <mailto:johnwbyrdatgmaildotcom>.