MIT (Most Important Task)
=========================

![Version](https://img.shields.io/badge/version-2.0-green.svg)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](http://opensource.org/licenses/MIT)

Overview
--------

Most Important Tasks addon for todo.txt-cli.

MIT adds functionality to Gina Trapani's [todo.txt-cli](https://github.com/ginatrapani/todo.txt-cli).  MITs are intended to be critical tasks that need to be accomplished on a particular day.  You can read more about MITs here:

* [zenhabits](http://zenhabits.net/purpose-your-day-most-important-task/)
* [lifehacker](http://lifehacker.com/software/top/geek-to-live--control-your-workday-187074.php)

The MIT plugin also supports assigning tasks to a year, quarter or month.

Installation
------------

1. Install and configure [todo.txt-cli](https://github.com/ginatrapani/todo.txt-cli).
2. Ensure TODO_ACTIONS_DIR is defined in todo.cfg or in your profile.
3. Place mit in your actions directory.
4. Ensure mit is executable.

Bash Completion
---------------

If you would like to add some auto completion to MIT as well as for your todo.sh contexts and projects, add the following to your `~/.bash_rc`.  This assumes you have aliased `todo.sh` to `t`.

    # todo-txt completion
    _todotxtcli() {
      local cur=${COMP_WORDS[COMP_CWORD]}
      local pre=${COMP_WORDS[COMP_CWORD-1]}
      case $pre in
        mit )
          COMPREPLY=( $(compgen -W "today tomorrow monday tuesday wednesday thursday friday saturday sunday january february march april may june july august september october november december" -- $cur) )
          ;;
        * )
          COMPREPLY=( $(compgen -W "mit `eval todo.sh lsprj` `eval todo.sh lsc`" -- $cur) )
          ;;
      esac
    }
    complete -F _todotxtcli t

Usage
-----

The mit addon can be used to both view and add MITs.

__To add mits:__

    todo.sh mit [DATE|DAY] [task]

    $ todo.sh mit tue buy dog food @chores
    113 {2013.06.04} buy dog food @chores
    TODO: 113 added.
    $

A date or day is required along with the task.  The DATE|DAY format is as follows:

    for daily mit's
    ---------------
      'today'
      'tomorrow'
      day of the week or abbreviation**     i.e. monday|mon
      YYYY.MM.DD                            i.e. 2080.01.15
    
    for yearly mit's
    ----------------
      YYYY                                  i.e. 2080
      YYYY.00.00                            i.e. 2080.00.00

    for quarterly mit's
    -------------------
      QN **                                 i.e. q1 | q4
      YYYYQN                                i.e. 2080q4
      YYYY.QN                               i.e. 2080.Q1

    for monthly mit's
    -----------------
      month name ore abbreviation**         i.e. january|jan
      YYYY.MM.00                            i.e. 2080.01.00
      YYYYMM                                i.e. 208001
      YYYY.MM                               i.e. 2080.01

    ** Assumes current week|or year, if chosen day|date has already
       passed then it will roll to the next upcoming day|date.

__To view mits:__

    todo.sh mit [not @context|@context]

    $ todo.sh mit @chores
    Tuesday, June 04:
      buy dog food @chores (113)

    $

Specifying a context to filter by is optional but can be helpful if you define MITs for multiple contexts.  MITs will be grouped by day with any old incomplete MITs listed under "Past Due:".

__To move mits:__

    todo.sh mit mv [ID] [DATE|DAY]

    $ todo.sh mit mv 113 tomorrow
    TODO: MIT 'buy dog food @chores' moved to tomorrow.
    $

As with adding mits dates must be in the format of YYYY.MM.DD, day names are accepted, or you can specify "Today" or "Tomorrow".  Thanks to [rcraggs](https://github.com/rcraggs) you can now convert non-mit tasks to mits with the move command as well, the usage is the same.

__To convert mits to normal tasks:__

    todo.sh mit rm [ID]

    $ todo.sh mit rm 113
    Removed MIT from task 113
    $

  Another bit of functionality provided by [rcraggs](https://github.com/rcraggs) that allows you to convert a mit to a normal task.

Format
------

MITs are stored directly in the todo.txt file with the following format:

    {YYYY.MM.DD} task info @context         # standard mit with set context
    {YYYY.QN.DD} task info                  # a quarterly mit
    {YYYY.00.00} task info                  # a yearly mit
    {YYYY.MM.00} task info                  # a monthly mit
    {YYYY.MM.DD} (A) task info @context     # prioritized mit with set context
    {YYYY.MM.DD} (A) 2013-05-29 task info   # mit with priority and date added (-t option)


MITs are displayed as follows:

    --------------------------------------------------------------------------------
    .                                                                              .
    .                                 Daily MIT's                                  .
    .                                                                              .
    --------------------------------------------------------------------------------

    Past Due:                               # all past due items displayed here
      mow the lawn @home (13)               # task numbers displayed on the end

    Today:
      change oil in car (23)
      prepare tps report @work (15)

    Wednesday:
      buy groceries @shopping (28)

    Monday, December 17:                    # anything a week out or more gets a date
      call mother (30)

License
-------

MIT is open-sourced software licensed under the [MIT license](http://opensource.org/licenses/MIT).
