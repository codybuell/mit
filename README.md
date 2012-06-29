MIT (Most Important Task)
=========================

Overview
--------

Most Important Tasks addon for todo.txt-cli.

MIT adds functionality to Gina Trapani's [todo.txt-cli](https://github.com/ginatrapani/todo.txt-cli).  MITs are intended to be critical tasks that need to be accomplished on a particular day.  You can read more about MITs here:

* [zenhabits](http://zenhabits.net/purpose-your-day-most-important-task/)
* [lifehacker](http://lifehacker.com/software/top/geek-to-live--control-your-workday-187074.php)

Installation
------------

1. Install and configure [todo.txt-cli](https://github.com/ginatrapani/todo.txt-cli).
2. Ensure TODO_ACTIONS_DIR is defined in todo.cfg or in your profile.
3. Place mit in your actions directory.
4. Ensure mit is executable.

Usage
-----

The mit addon can be used to both view and add MITs.

To add mits:

    todo.sh mit [DATE|DAY] [task]

A date or day is required along with the task.  Dates must be in the format of YYYY.MM.DD.  Days can be days of the week (Monday, Tuesday, etc.), or abbreviated days of the week (Mon, Tue, etc.).  "Today" or "Tomorrow" are also accepted.

To view mits:

    todo.sh mit [@context]

Specifying a context is optional but can be helpful if you define MITs for multiple contexts.  MITs will be grouped by day with any old incomplete MITs listed under "Past Due:".

Format
------

MITs are stored directly in the todo.txt file with the following format:

    {YYYY.MM.DD} task information @context
