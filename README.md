# Rex: Shiny R/exams Dashboard <img src="https://raw.githubusercontent.com/guesswho1234/Rex/main/www/logo.svg" align="right" alt="Rex logo" width="180" />

This repository provides an interactive [shiny](https://shiny.posit.co/) dashboard
for creating and evaluating written single and multiple-choice exams. The underlying workhorse
is [R/exams](https://www.R-exams.org/), in particular the so-called
[NOPS exams](https://www.R-exams.org/tutorials/exams2nops/) functions which support both
single-choice and multiple-choice exercises along with automatic evaluation.

The dashboard provides:

- Import/export of R/exams exercises with type "schoice" or "mchoice"
- Creation of an exam by combining (blocks of) exercises and exporting (randomized) PDF files
- Evaluation of scanned exercises
- [optional / addon] Management of participants and grades, connecting with other tools at [Universität Innsbruck](https://www.uibk.ac.at/)

Rex is developed by [Sebastian Bachler](https://www.uibk.ac.at/ibf/team/bachler.html.en)
and is still work-in-progress.

## Run

There are multiple ways to get this applications running:

### Localhost

Install all the necessary R packages (see `init.R`) including their dependencies.

Start up via `shiny::runApp(appDir = 'base directory containing app.R', host = '127.0.0.1', port = 8180);` or, alternatively, via RStudio by 
opening and running `app.R`.

### Heroku
This setup was tested on the `heroku-22` stack.

Install the following buildpacks in the following order on your heroku app:
- https://github.com/rricard/heroku-buildpack-dpkg.git
- https://github.com/virtualstaticvoid/heroku-buildpack-r

Set the following environment variables (called "*Config Vars*" on Heroku):
- `INCLUDE_DIR`: `/app/.dpkg/usr/include/poppler/cpp/`
- `LD_LIBRARY_PATH`: `/app/.dpkg/usr/lib/x86_64-linux-gnu/:/app/R/lib/R/lib:/app/tcltk/lib`
- `LIB_DIR`: `/app/.dpkg/usr/lib/x86_64-linux-gnu/`

Deploy this repository to your Heroku app.

Make sure the web dyno is turned on.

> [!NOTE]
Heroku shuts down your application if you exceed the memory allocated to your dyno type.
If you are using the `Eco` dyno type, the application also shuts down when there is no traffic for 30 minutes.

> [!WARNING]
While most features of Rex can be used with the low tier dyno types Heroku offers, evaluating exams cannot.
Therefore, make sure to switch to high performance dyno types if you wish to evaluate exams with Rex hosted on Heroku.  

### Docker

Build your image with the supplied docker file: `docker build --platform linux/x86_64 -t shiny-docker-rex .`.

Run your image: `docker run -p 8180:8180 shiny-docker-rex`. 

## Usage

Once you got the application running, authenticate using `rex` as both login and password.

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what 
you would like to change.
