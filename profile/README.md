# ELMO Hoops Website Management

Welcome to the GitHub organization for the El Modena Vanguards Boys
Basketball website.

This organization contains the custom web applications used by:

https://www.elmohoops.org/

This document is intended as the starting point for current and future
ELMO Hoops Website Managers.

If you are taking over website maintenance for the first time, start
here before changing any code.

------------------------------------------------------------------------

## Quick Start: What Are You Trying to Change?

Most routine website updates do **not** require programming or GitHub
changes.

  -----------------------------------------------------------------------
  What you need to change             Where to make the change
  ----------------------------------- -----------------------------------
  Game or event schedule              Google Calendar

  Player roster                       Google Sheets

  Coaching staff                      Google Sheets

  Current basketball season for       Google Sheets
  rosters                             

  Booster Board members               Google Sheets

  Current basketball season for       Google Sheets
  Booster Board                       

  Sponsor information                 Wix

  Registration information            Wix

  General page text or images         Wix

  Navigation or page layout           Wix

  Contact information                 Wix

  Schedule application appearance or  GitHub `schedule` repository
  behavior                            

  Roster application appearance or    GitHub `rosters` repository
  behavior                            

  Booster Board application           GitHub `board` repository
  appearance or behavior              
  -----------------------------------------------------------------------

As a general rule:

**Content changes belong in Wix or Google. Code changes belong in
GitHub.**

------------------------------------------------------------------------

## Website Architecture

The ELMOHoops website uses three primary services:

``` text
                    ELMOHoops.org
                         │
                         │
                        Wix
                  Main Website/UI
                         │
             ┌───────────┼───────────┐
             │           │           │
          Schedule    Rosters      Board
             │           │           │
          GitHub       GitHub       GitHub
           Pages        Pages        Pages
             │           │           │
             │           │           │
          Google       Google       Google
         Calendar      Sheets       Sheets
```

Another way to think about the system:

**Wix = Website**

**Google = Data**

**GitHub = Custom Applications**

Keeping these responsibilities separate makes the website easier for
future volunteers to maintain.

------------------------------------------------------------------------

## Wix

Main website:

https://www.elmohoops.org/

Wix is the primary public website and controls:

-   Site navigation
-   Page layout
-   Home page
-   Registration information
-   Sponsor information
-   Physicals and athletic-clearance information
-   Contact information
-   General text and images
-   Other normal website content

The Schedule, Rosters, and Booster Board applications are hosted
separately on GitHub Pages and embedded into Wix using HTML/iframe
elements.

For normal website content changes, start in Wix.

------------------------------------------------------------------------

## GitHub

GitHub organization:

https://github.com/elmohoops

GitHub contains the custom applications that display dynamic information
from Google.

### Schedule

Repository:

https://github.com/elmohoops/schedule

Live application:

https://elmohoops.github.io/schedule/

Purpose:

Displays basketball games and events from multiple Google Calendars in
one responsive schedule.

Data source:

**Google Calendar**

See the repository README for technical details, deployment
instructions, API configuration, and troubleshooting.

### Rosters

Repository:

https://github.com/elmohoops/rosters

Live application:

https://elmohoops.github.io/rosters/

Purpose:

Displays team rosters and coaching staffs.

Data source:

**Google Sheets**

One application supports multiple team pages using a URL query
parameter.

Examples:

``` text
https://elmohoops.github.io/rosters/?team=Varsity
https://elmohoops.github.io/rosters/?team=Junior%20Varsity
https://elmohoops.github.io/rosters/?team=Frosh%2FSoph
https://elmohoops.github.io/rosters/?team=Freshman
```

See the repository README for spreadsheet structure, season rollover,
team configuration, and troubleshooting.

### Booster Board

Repository:

https://github.com/elmohoops/board

Live application:

https://elmohoops.github.io/board/

Purpose:

Displays current Booster Board members, positions, and available email
addresses.

Data source:

**Google Sheets**

See the repository README for spreadsheet structure, season rollover,
Wix iframe sizing, and troubleshooting.

------------------------------------------------------------------------

## Google

The ELMO Hoops Google account provides the routine data used by the
custom applications.

### Google Calendar

Google Calendar is the source of schedule information.

Use Google Calendar to:

-   Add games
-   Change game dates or times
-   Change locations
-   Add tournaments or other events
-   Correct event descriptions
-   Remove cancelled events

Schedule changes normally require **no GitHub changes**.

### Google Sheets

Google Sheets provides data for:

-   Team rosters
-   Coaching staffs
-   Booster Board members
-   Current-season configuration

Use the appropriate spreadsheet rather than editing application code for
routine personnel changes.

Historical seasons can remain in the spreadsheets.

The applications use a `CurrentSeason` configuration value to determine
which season to display.

------------------------------------------------------------------------

## Google Cloud / Calendar API

The Schedule application uses the Google Calendar API.

The API key is configured in the Schedule repository.

The Google Cloud API key uses website/HTTP-referrer restrictions.

The production GitHub Pages domain must be allowed:

``` text
https://elmohoops.github.io/*
```

If the Schedule application becomes stuck on `Loading...`, check the
browser developer console for Google Calendar API errors.

A `403 Forbidden` response can indicate that the GitHub Pages URL is not
included in the API key's allowed HTTP referrers.

Do **not** solve API errors by removing security restrictions from the
API key.

See the Schedule repository README for additional troubleshooting
information.

------------------------------------------------------------------------

## Normal Season-to-Season Maintenance

### Schedule

Continue using the appropriate Google Calendars.

No annual GitHub reset should be necessary.

### Rosters

Add the new season's players and coaches to the roster Google Sheet.

Then update:

``` text
CurrentSeason
```

in the spreadsheet's `Configuration` tab.

Previous seasons can remain in the spreadsheet for historical reference.

### Booster Board

Add the new season's Board members to the Board Google Sheet.

Then update:

``` text
CurrentSeason
```

in the spreadsheet's `Configuration` tab.

Previous Board seasons can remain in the spreadsheet.

------------------------------------------------------------------------

## GitHub Pages

The three custom applications are hosted using GitHub Pages.

Production applications:

``` text
https://elmohoops.github.io/schedule/
https://elmohoops.github.io/rosters/
https://elmohoops.github.io/board/
```

The Wix website embeds these applications.

If an organization name, repository name, or GitHub Pages URL is ever
changed:

1.  Verify the new GitHub Pages application works first.
2.  Update the corresponding Wix iframe URL.
3.  Check desktop and mobile Wix layouts.
4.  For Schedule, also verify the Google Calendar API HTTP-referrer
    restrictions.

Do not change a production Wix iframe until the replacement GitHub Pages
URL has been tested.

------------------------------------------------------------------------

## Making Code Changes

GitHub should normally only be changed when modifying application:

-   Appearance
-   Layout
-   Behavior
-   Features
-   Data-source configuration
-   API configuration

Before modifying an application, read that repository's README.

For significant changes:

1.  Make the change.
2.  Test it before replacing the production version.
3.  Verify desktop behavior.
4.  Verify mobile behavior.
5.  Commit the tested changes.
6.  Allow GitHub Pages to deploy.
7.  Test the GitHub Pages URL directly.
8.  Test the embedded version on ELMOHoops.org.
9.  Create a Git tag/release for significant stable versions when
    appropriate.

The Schedule application includes a development area intended for
testing changes before promotion to production.

------------------------------------------------------------------------

## Visual Design

The custom applications are designed to visually integrate with the Wix
website.

General design language includes:

-   El Modena cardinal
-   Gold accents
-   White content cards
-   Dark charcoal text
-   Basketball/court visual elements
-   Transparent application backgrounds where appropriate
-   Responsive desktop and mobile layouts

Important information should not rely on color alone.

When changing application styling, preserve consistency across the
website whenever practical.

------------------------------------------------------------------------

## Website Manager Access and Handoff

The GitHub applications are owned by the **ELMO Hoops GitHub
Organization**, not by an individual volunteer's personal GitHub
account.

Each Website Manager should use their own GitHub account.

Do **not** create or share a common GitHub username/password.

When a new Website Manager takes over, the outgoing manager should
verify that the incoming manager has appropriate access to:

-   ELMO Hoops Wix website
-   ELMO Hoops GitHub organization
-   ELMO Hoops Google account
-   Required Google Calendars
-   Roster Google Sheet
-   Booster Board Google Sheet
-   Google Cloud project used by the Schedule application
-   Any other program-owned website services

The new Website Manager should be added to the GitHub organization using
their own GitHub account.

Once the handoff is complete, organization permissions can be adjusted
as appropriate.

------------------------------------------------------------------------

## Important Ownership Principle

Whenever possible, ELMO Hoops website infrastructure should be owned by
program-controlled accounts or organizations rather than a volunteer's
personal account.

This helps prevent future access problems when Website Managers change.

The GitHub repositories are therefore owned by:

``` text
github.com/elmohoops
```

rather than by an individual Website Manager.

The same principle should be followed for other website services
whenever practical.

------------------------------------------------------------------------

## Troubleshooting: Where Should I Start?

### The schedule is wrong, but the page works

Check Google Calendar.

### The roster information is wrong, but the page works

Check the roster Google Sheet.

### The Booster Board information is wrong, but the page works

Check the Board Google Sheet.

### A GitHub application will not load

Open the application's GitHub repository and read its README
troubleshooting section.

Also verify that GitHub Pages is successfully deployed.

### Schedule is stuck on "Loading..."

Check the browser developer console.

If Google Calendar requests return `403 Forbidden`, check the Google
Cloud API key's HTTP-referrer restrictions.

### An embedded application works directly on GitHub Pages but not in Wix

Check the Wix iframe URL and iframe dimensions.

Verify both desktop and mobile Wix layouts.

### Board members were added but cards are cut off

Increase the Booster Board iframe height in Wix.

Mobile and desktop iframe heights may need to be adjusted independently.

### A new roster season does not appear

Check `CurrentSeason` in the roster spreadsheet's Configuration tab and
make sure it exactly matches the Season value in the new player and
coach rows.

### A new Booster Board season does not appear

Check `CurrentSeason` in the Board spreadsheet's Configuration tab and
make sure it exactly matches the Season value in the new Board rows.

------------------------------------------------------------------------

## Repository Documentation

Each application contains its own detailed README.

Use those documents for technical maintenance:

-   [`schedule`](https://github.com/elmohoops/schedule) - Google
    Calendar integration, Calendar API, development/production workflow
-   [`rosters`](https://github.com/elmohoops/rosters) - roster
    spreadsheet structure, team URLs, season management
-   [`board`](https://github.com/elmohoops/board) - Board spreadsheet
    structure, season management, Wix iframe behavior

This organization-level README explains the overall system.

The individual repository READMEs explain how each application works.

------------------------------------------------------------------------

## Maintenance Philosophy

The ELMO Hoops website is intentionally designed so that routine
basketball-program maintenance does not require programming knowledge.

Remember:

**Google Calendar = Schedule**

**Google Sheets = Rosters, Coaches, and Booster Board**

**Wix = Main Website Content**

**GitHub = Custom Application Code**

If a routine content update can be made in Wix, Google Calendar, or
Google Sheets, it generally should be made there rather than by
modifying application code.

This separation is intentional and should be preserved whenever
practical.
