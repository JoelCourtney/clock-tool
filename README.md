# clock-tool
Small command line tool for logging hours worked

## Installation

Simply link, copy, or move `clock` to somewhere in your path.

```sh
$ ln -s ./clock <dest>
```

## Usage

Use `clock init` to start a new `hours` directory.

```sh
$ clock init
MAKING DIRECTORY: hours/
MAKING ACTIVE LOG FILE: hours/current_period.json
```
Use `clock in` when you start working.

```sh
$ clock in
CLOCKING IN AT: <current local time>
```

Use `clock out` when you stop, and follow the prompt.

```sh
$ clock out
SHORT DESCRIPTION OF WORK DONE: procrastinated by making a stupid script
CLOCKING OUT AT: <current local time>
```

Use `clock status` to view hours logged for this pay period.

```sh
$ clock status
HOURS FROM Mon, 22 Jun 2020 TO Mon, 22 Jun 2020
================================================

Mon, 22 Jun 2020: 06:31 PM to 06:34 PM
procrastinated by making a stupid script
0.05 HOURS


TOTAL HOURS: 0.05
```

Use `clock edit` if you messed up and need to change something you already input. This will open the json log file according to your `$EDITOR` env variable, or in `vi` if it is not set. A sample file is below:

```json
{
	"start_time":null,
	"entries":[
		{
			"in":[
				2020,
				6,
				22,
				18,
				31,
				43,
				0,
				174,
				1
			],
			"out":[
				2020,
				6,
				22,
				18,
				34,
				47,
				0,
				174,
				1
			],
			"desc":"procrastinated by making a stupid script"
		}
	]
}
```

The 9-element lists are python time.struct_time objects, of the form:

```
[
	year,
	month,
	day,
	hour (24-hour time),
	minute,
	second,
	# day of week (Monday is 0),
	# day of year,
	daylight savings flag (1 = DLS in effect, 0 = DLS not in effect, -1 = unknown)
]
```

Use `clock commit` when ready to submit your timesheet.

```sh
$ clock commit
HOURS FROM Mon, 22 Jun 2020 TO Mon, 22 Jun 2020
================================================

Mon, 22 Jun 2020: 06:31 PM to 06:34 PM
procrastinated by making a stupid script
0.05 HOURS


TOTAL HOURS: 0.05

ARE YOU SURE YOU WANT TO COMMIT? [y/N]: y

WRITING TO FILE: hours/22-Jun-20__22-Jun-20.txt
```


