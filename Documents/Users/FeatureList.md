# Feature List

We try to keep this up to date, but sometimes implementation can get ahead of
documentation. If a command is missing, just try it in XVim first - it might
already be there!

If you've tried a command and it really is missing, feel free to create an issue and a
friendly contributor will pick it up eventually.

## Motion
b, B, f, F, gg, G, h, j, k, l, w, W, t, T, 0, $, ^, %, +, -, {, }, (, ), n, N, ', `, M, H, L

Comma and semicolon are supported. Toggle inclusive/exclusive by v is supported.

## Mark

File-local and Global marks are supported.

The '^' mark (last insertion point) and '.' mark (last change point) are also supported.
gi (insert mode at last insertion point) is supported.

Known issue: When deleting a line before a mark the mark position should go up along with the line marked but currently XVim does not follow the line. It stays at the absolution position as it was marked.

## Scroll

C-d, C-f, C-e, C-u, C-b, C-y, zz, zb, zt

## Jumps
C-o, C-i, gd

C-i is defined as 'Editor-Structure-Re Indent' in default Xcode key bindings.
If you want to use C-i as jump, you need to clear ^I in Xcode settings 'Xcode-Preference-Key bindings'.

If you want to open the file under the cursor you can use 'gd' instead of 'gf' in XVim environment.

## Insert
a, A, i, I, o, O

You can use Ctrl-o to enter to temporary normal mode during insert mode.

Ctrl-w,Ctrl-y,Ctrl-e commands in insert mode are supported. If you want to use Ctrl-e as "move to end of line" in insert mode (which is default Xcode behaviour),
you can specify following line in .xvimrc.

     inoremap <C-e> <C-o>$

## Navigation
C-], C-t

C-] is mapped to "Jump To Definition".
C-t is mapped to "Go Back" (as it is the closest thing Xcode has to vims behavior).

## Yank, put and change

d, dd(d_), D, y, yy(y_), Y, c, cc(c_), C, r, s, S, x, X

## Line join

J

## Shift block

Normal mode: >, >>, <, <<

## Case change operations

Normal mode: ~, gu, gU, g~

Visual mode: u, U, ~, gu, gU

## Undo

u, C-r

## Folds

zc, zC, zm, zM, zo, zO, zr, zR

zc - fold
(Note: zC is mapped to zc as Xcode does not have similar vim behavior.)

zM - fold all
(Note: zm is mapped to zM as Xcode does not have similar vim behavior.)

zo - unfold
(Note: zO is mapped to zo as Xcode does not have similar vim behavior.)

zR - unfold all
(Note: zr is mapped to zR as Xcode does not have similar vim behavior.)

## Visual
v, V, Ctrl-v

(v, V in visual mode to toggle or escape from visual mode is supported)

Inserting with visual block is also supported.

## Operation in Visual

## Window manipulation

 Input     | Operation
-----------|---------------------------
  C-w c    | Close current editor.
  C-w n    | Add new assistant (Use layout of the last)
  C-w o    | Delete all assistant editors.
  C-w q    | Delete one assistant editor
  C-w s    | Add new assistant editor. Assistant editors are laid out horizontally.
  C-w v    | Add new assistant editor. Assistant editors are laid out vertically.
C-w h,j,k,l| Move focus between editors
  C-w w    | Jump to the next editor
  C-w W    | Jump to the previous editor

  Alias    | Operation
-----------|---------------------------
  C-w C-c  | Same as "C-w c"
  C-w C-n  | Same as "C-w n"
  C-w C-o  | Same as "C-w o"
  C-w C-q  | Same as "C-w q"
  C-w C-s  | Same as "C-w s"
  C-w C-v  | Same as "C-w v"
  C-w C-h  | Same as "C-w h"
  C-w C-j  | Same as "C-w j"
  C-w C-k  | Same as "C-w k"
  C-w C-l  | Same as "C-w l"
  C-w C-w  | Same as "C-w w"
  C-w C-W  | Same as "C-w W"

The behaviour of window manipulations is slightly different from Vim's one. This is because that Xcode doesn't have a concept of multiple equivalent text views in a window.
Instead, Xcode has a concept of a main editor and assistant editors. A main editor always stays in a window and you can add/remove multiple assistant editors.
You can NOT split a main editor but just can add assistant editors.
All the manipulations XVim does is add/split assistant editors.
The layout is forced to change with Ctrl-w,s or Ctrl-w,v .

## Search and Replace

/, ?, #, \*, g*, g#, :s, n, N

Regex search is supported using the [ICU regex](https://developer.apple.com/library/ios/documentation/Foundation/Reference/NSRegularExpression_Class/Reference/Reference.html) format.

## Insert mode commands

C-y, C-e

## Print status commands

C-g

## Text Object

ib, iB, i(, i), i{, i}, i[, i], i>, i<, i", i', iw, iW
ab, aB, a(, a), a{, a}, a[, a], a>, a<, a", a', aw, aW

## Recording

q, @

## Dot command

The dot command ('.') is supported.

## Ex commands

 Command   | Note
-----------|-----
  :w[rite] |
  :wq      |
  :q[uit]  |
  :reg[isters]| Show contents of registers
  :s[ubstitute]|
  :set     | See Options for supported variables
  :map     | Show all the current mapping. When with arguments maps globally across XVim, in all modes
  :nmap    | Maps normal mode
  :vmap    | Maps visual mode
  :imap    | Maps insert mode
  :omap    | Maps operator pending mode
  :!       | Execute command with external process
  :jumps   | Show jump list. The current position is represented as '>'.
  :sp[lit] | Add new assistant editor. Assistant editors are laid out horizontally.
  :vsp[lit]| Add new assistant editor. Assistant editors are laid out vertically.

## Ex ranges

 Range     | Note
-----------|-----
  :X,Y     | Multiple line range
  :X-N,Y   | Multiple line range
  :X+N,Y   | Multiple line range
  :X       | Single line range
  :X-N     | Single line range
  :X+N     | Single line range
  :-N      | Single line range, shortened version of X-N where X is '.'
  :+N      | Single line range, shortened version of X+N where X is '.'

In the above table, N can only be a digit, but X and Y can be a digit, a mark reference (EXAMPLE 'a), '.', or '$'.

## Ex range commands

 Command   | Note
-----------|-----
  y[ank]   | Yank lines in range
  d[elete] | Delete lines in range
  copy     | Copy lines in range to new location
  t        | Synonym for copy
  m[ove]   | Move lines in range to new location
  sort     | Sort lines in range
  s[ubstitute]      | Documented in "Search and Replace" above.  '&' and '~' can be used as synonyms for 's'.
  !        | Execute command with external process

Examples:

    :1,.y
    :4,5m$
    :'a,'bd
    :5t10


## Filename modifier for bang

 Modifier  |
-----------| ----
  %        | current file name
  #        | alternate file name
  :p       | full path
  :h       | head of path
  :r       | root of filename
  :t       | tail of filename
  :e       | extension of filename

## XVim original commands

 Command   | Note
-----------|-----
  :run          | Invoke Xcode's 'run' command
  :make         | Invoke Xcode's 'build' command
  :xhelp        | Show quick help for current insertion point
  :xccmd        | (Use :xcmenucmd instead. It is simpler. ) Invoke arbitrary command in Xcode's actions in its menu. Takes one argument as its action to invoke. Actions [here](../Developers/MenuActionList.txt) are available.
  :xcmenucmd    | Invoke arbitrary command in menu. (EXAMPLE: :xcmenucmd Run)
  :nissue       | Invoke "jump to next issue". ":ni" does the same.
  :pissue       | Invoke "jump to previous issue". ":pi" does the same.
  :ncounterpart | Invoke "jump to next counterpart". ":nc" does the same.
  :pcounterpart | Invoke "jump to previous counterpart". ":pc" does the same.
  :njump        | Invoke "go forward". ":nj" does the same.
  :pjump        | Invoke "go back". ":pj" does the same.

## Options

 Command       | Note
---------------|-----
  [no]ignorecase |
  [no]wrap |
  [no]wrapscan |
  [no]errorbells |
  [no]incsearch |
  [no]gdefault |
  [no]smartcase |
  [no]number |
  [no]hlsearch |
  [no]expandtab | Only affects shift operations (e.g. `>>`, `v>`). When set to off, set tab width and insert mode behavior of tab key in XCode preferences (Text Editing -> Indentation). Defaults to on.
  guioptions | See below
  timeoutlen | The time in milliseconds that is waited for mapped key sequence to complete (default 1000)
  laststatus | 0 or 1 : status line is hidden, 2 : status line is displayed  (default 2)
  clipboard | ":set clipboard=unnamed" to share system clipboard with unnamed register
  [no]vimregex | Tells XVim to use Vim's regular expression. Currently support \<,\> for word boundary, \c,\C for specifying case (in)sensitiveness.
  [no]relativenumber |
  [no]alwaysuseinputsource | With this option all the input is first sent to input source of the system. If you are using France, Portugese or Swedish keyboard consider turning this on. When enabling this, also consider running `defaults write com.apple.dt.Xcode ApplePressAndHoldEnabled -bool false` to disable the press and hold character menu in recent OS X releases.  (See issue https://github.com/JugglerShu/XVim/issues/598).
  [no]blinkcursor |
  [no]startofline | Tells XVim to move the cursor to the first non-blank of the line when using jump commands (`gg, G` etc). Defaults to on.


## guioptions

A limited subset of Vim options is implemented.

Option | Effect
-------|--------
r | Show vertical scrollbar
b | Show horizontal scrollbar

These changes take effect after you resizing the view.
So if you cannot see the GUI changes, please resize the view.

## Key mapping

XVim supports five map commands: map, nmap, vmap, imap, omap.
A map command can change one or more keystrokes into one or more key strokes.

Note: The default timeout value for multi-key mapping completion is 1 seconds (1000 milliseconds). You can change it using 'timeoutlen' option.

Examples:

    nmap n e
    imap ' <Esc>
    nmap u 5jiInsert some text<Esc>
    nmap ,w :w<cr>


## .xvimrc

At startup XVim looks for ~/.xvimrc. Each line in this file is executed
as an ex command. This allows you to configure mappings and options.

Example:

    set ignorecase
    set wrapscan
    set guioptions=r
    nmap n e

## Known problems
 See XVim issue page.


## Experimental

### :xctabctrl (Ex command)
:xctabctrl command takes one argument and send message to the current tab workspace window.
A tab workspace window handles a lot of usuful actions provided by Xcode.
For example following command shows/hides a utility area (right side of a window)

      :xctabctrl showUtilitiesArea:
      :xctabctrl hideUtilitiesArea:

The arguments :xctabctrl accepts are method names in IDEWorkspaceTabController class.
See IDEKit.h file in XVim source code and find the class.
It has a lot of  actions (selectors) which takes one argument. These are the methods
we can call directly through the ex command.
Some does work well but some does not. Try using it to find out if it works as you like.
If you once find some useful feature in it you can map it to key input via :map command.

(Note that the argument for :xctabctrl always ends with ":" as shown above)
