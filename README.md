# ws-choice: _choiceMulti.bat & _choiceYN.bat

Sub-scripts for automatic fallback to `set /p` for systems without choice.exe.

Two flavours:

1. `_choiceMulti.bat` gives a customizable number of choices
2. `_choiceYN.bat` gives Y or N as choices

![](https://1.bp.blogspot.com/--Y3D3svk1l4/XpGVLuSRWGI/AAAAAAAACQk/zjxCKaKv5tQ1UPyain_r_MF0ODuJ3xMpQCLcBGAsYHQ/s1600/ws-choice.png "Accessing Windows Magnifier functions from AeroZoom panel")

## _choiceMulti.bat

```
:: ------------------------------------------------------------------------

:: Sub-script: _choiceMulti.bat
:: Version: 1.1
:: Creation Date: 2/11/2009
:: Last Modified: 20/01/2010

:: Supported OS: Windows 2000 or later

:: Description: Automatically fall back to set /p for systems without choice.exe
::              Differentiate choice.exe from Win 9x and 2003/Vista/7
::              Set /p also returns errorlevels
::              Definable number of choices; for YN choices, use ChoiceYN
::              v1.1 adds support of sed and tr to filter inputs

:: For a list of supported parameters, refer to paramter /?

:: ------------------------------------------------------------------------
```

## _choiceMulti.bat - README

```
 :: _choiceMulti.bat

  [Usage]

  call _choiceMulti /msg "description" [/button "choices"] [/time "sec"]
                   [/default "choice"] [/errorlevel 1-9] 
                   [/choice "1" ["2"] ["3"] ["4"]...["9"]]

  /msg        - the line users see when they are asked for input
  /button     - instead of ascending numbers, users can enter any of these
                specified to go to the choice. *1 *2
  /time       - timeout after specified seconds (used with /default) *1 *2
  /default    - default answer (used with /time) *1 *2
  /errorlevel - outputs errorlevels just as choice.exe. Either this or
                /choice has to be set *1 *4
  /choice     - when users makes a choice, what is carried out. Either this or
                /errorlevel has to be set *1 *3 *4

  *1 optional
  *2 not applicable for "set /p" (you give up set /p support by setting it)
  *3 /choice must be the last switch, otherwise it would not run Automatically
  *4 maximum supported choices: 9
  
  :: due to arguments being %1-%9 without shift (may add more in the future)

  [Examples]

  1) "1" performs "echo 1", "2" performs "echo 2":

     :: call _choiceMulti /msg "Choose: [1,2]" /choice "echo 1" "echo 2"

  2) Same as 1st, except that after 5 seconds, default answer "1" is supplied

     :: call _choiceMulti /msg "Choose: [1,2]" /Default 1 /Time 5 /choice
        "echo 1" "echo 2"

  3) Same as 1st, except button of choice 1,2 is swapped with A,B.
     "Set /p" would fail here; ensure the target system has choice.exe.

     :: call _choiceMulti /msg "Choose: [A,B]" /button AB /choice "echo 1"
        "echo 2"

  * /button is [optional]. when not set, numbering and ascending order,
    e.g. 123456789 are assumed to keep compatibility with set /p. If set /p
    is unneeded, then anything can be set, e.g. letters and descending order

  4) This is the most common. Do nothing but errorlevels just as choice.exe

     :: call _choiceMulti /msg "Choose: [1,2]" /errorlevel 2

  [Returns]

  %errorlevel% 0-9, depends on user choice

```

## _choiceYN.bat

```
:: ------------------------------------------------------------------------

:: Sub-script: _choiceYN.bat
:: Version: 1.1
:: Creation Date: 2/11/2009
:: Last Modified: 20/01/2010

:: Supported OS: Windows 2000 or later

:: Description: Automatically fall back to set /p for systems without choice.exe
::              Differentiate choice.exe from Win 9x and 2003/Vista/7
::              Set /p also returns errorlevels
::              Gives 2 choices, YN; for other choices, use ChoiceMulti
::              v1.1 adds support of sed and tr to filter inputs

:: For a list of supported parameters, refer to paramter /?

:: ------------------------------------------------------------------------
```

## _ChoiceYN.bat - README

```
 :: _ChoiceYN.bat

  [Usage]

  call _choiceYN "Message" [Default Choice] [Timeout]

  %1 = message shown for choice.exe
  %2 = optional default choice, e.g. %defErrAct% * 
  %3 = optional time in seconds before applying default choice *

   * not applicable to "set /p"

  [Examples]

  1) Displays "An update is available. Get it now? [Y,N]"

     :: call _choiceYn "An update is available. Get it now? [Y,N]"

  2) Same as 1st, except that after 5 seconds, default answer "N" is supplied.

     :: call _choiceYn "An update is available. Get it now? [Y,N]" N 5

  [Returns]

  %errorlevel% EQU 0 means Y
  %errorlevel% NEQ 0 means N
```

## Release History

| Ver | Date | Changes |
| --- | --- | --- |
| 1.1 | 20100120 | Support `sed` and `tr` for filtering inputs |
| 1.0 | 20091102 | First released in 2009 |
