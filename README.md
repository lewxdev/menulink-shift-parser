# MenuLink Shift Parser #

## Purpose ##
The following is an as-is command-line utility built with python for parsing schedules (PDF) from the MenuLink software and export weekly employee shifts to their calendar ([IFTTT](https://ifttt.com/about)). Intended to automate the process of personally keeping track of scheduled shifts—e.g. by hooking into a server which reads filtered emails (if the employer sends out the schedule to be interpreted via email).

## Dependencies ##
* [`pandas`](https://pypi.org/project/pandas/) - provides methods and typing for interfacing with the resulting `pandas.DataFrame`
* [`python-dotenv`](https://pypi.org/project/python-dotenv/) - provides methods for interpreting .env files (keep your [IFTTT webhook key](https://ifttt.com/maker_webhooks) secret)
* [`requests`](https://pypi.org/project/requests/) – provides a method for making HTTP requests for triggering IFTTT webhook events
* [`tabula-py`](https://pypi.org/project/tabula-py/) – provides a method for converting tabular data from the provided PDF to a `pandas.DataFrame`

## Usage ##
### Setup ###
1. After cloning/forking the repository [install `pipenv`](https://pipenv.pypa.io/en/latest/install/) if not already installed
2. Install dependencies to the virtual environment with `pipenv install`
3. Prepend commands with `pipenv run python main.py`

### Arguments ###
* `DATE` – the date identifier of the schedule file, conventionally formatted as "%Y-%m-%d"
* `EMPLOYEE` - the name of the employee to retrieve shifts for. Can be formatted as "last, first" (as it appears) or "first last"

## Caveats ##
As implemented, the `area` argument of `tabula.read_pdf()` is required for the schedule to be parsed correctly, and the exact column positions may not be consistent in all use cases. A potential solution is to [determine these positions](https://tabula-py.readthedocs.io/en/latest/faq.html#how-to-use-area-option) before using the utility (though this may not be consistent weekly if the employee roster changes in a way that moves the first column position significantly). Alternatively, a method could be implemented that determines the first column position at runtime and the other positions are generated programmatically based on the page margins (given equidistance).
