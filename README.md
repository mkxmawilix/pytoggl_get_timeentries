pytoggl_get_timeentries
===================

A small python script to get your current work week Toggl time entries (or for a specific dates range)

Requirements
===================
python-redmine : https://pypi.python.org/pypi/python-redmine/


How to use : 
===================
$ python main.py 'YOU_API_TOKEN'

(python main.py -h for more option : workhours, specific dates range, send_by_mail, etc.)

/!\ For a specific dates range the limit of the return is 1000. So only the first 1000 found time entries are returned /!\ (view Toggl API : https://github.com/toggl/toggl_api_docs/blob/master/chapters/time_entries.md#get-time-entries-started-in-a-specific-time-range)


Redmine time entry :
===================
You can auto create time entries if the "Redmine" option is set (--redmine option)
You have to set the "Redmine URL" and the "Redmine API key" options (--rurl and --rkey options)

You need to specify the ticket number in the TOGGL time entrie's description (ie : #12345 - TEST TOGGL TO REDMINE)
If many ticket number found in the description, a time entry will be created by ticket. The duration will be divided by the number of ticket

If you want to display the time entrie's tracker for a better issue tracking can add the --rtracker option
It will display the tracker for each issue in the toggl time entrie's description.

Exemple without --redmine option: 
===================
The script is started the 2014-01-04, the current work week will be 2014-12-29 - 2015-01-04

Output : 
    
    ------------------------------------------------
    |              TOGGL TIME ENTRIES              |
    ------------------------------------------------
    Here are your Toggl's time entries.
    From : 2014-12-29
    To : 2015-01-04
    
    
    # Date : 2014-12-29
        * Project : None
        |   Name : TIME ENTRY 1
        |         Duration (H:M:S) : 8:45:00
        |         Duration (Hours) : 8.75
        |         Duration (Days) : 1.094
        > Duration total (Hours) : 8.75
        > Duration total (Days) : 1.094
    > Total (Hours) : 8.75
    > Total (Days) : 1.094
    ------------------------------------------------
    # Date : 2014-12-30
        * Project : PROJECT1
        |   Name : TIME ENTRY 2
        |         Duration (H:M:S) : 8:35:07
        |         Duration (Hours) : 8.585
        |         Duration (Days) : 1.073
        > Duration total (Hours) : 8.585
        > Duration total (Days) : 1.073
    > Total (Hours) : 8.585
    > Total (Days) : 1.073
    ------------------------------------------------
    # Date : 2014-12-31
        * Project : PROJECT1
        |   Name : TIME ENTRY 3
        |         Duration (H:M:S) : 8:23:20
        |         Duration (Hours) : 8.389
        |         Duration (Days) : 1.049
        > Duration total (Hours) : 8.389
        > Duration total (Days) : 1.049
    > Total (Hours) : 8.389
    > Total (Days) : 1.049
    ------------------------------------------------
    # Date : 2015-01-02
        * Project : PROJECT4
        |   Name : TIME ENTRY 4
        |         Duration (H:M:S) : 7:50:44
        |         Duration (Hours) : 7.846
        |         Duration (Days) : 0.980
        |   Name : TIME ENTRY 5
        |         Duration (H:M:S) : 2:30:00
        |         Duration (Hours) : 2.5
        |         Duration (Days) : 0.313
        > Duration total (Hours) : 10.346
        > Duration total (Days) : 1,293
        * Project : PROJECT3
        |   Name : TIME ENTRY 6
        |         Duration (H:M:S) : 1:30:00
        |         Duration (Hours) : 1.5
        |         Duration (Days) : 0.188
        > Duration total (Hours) : 1.5
        > Duration total (Days) : 0.188
    > Total (Hours) : 11.846
    > Total (Days) : 1.481
    ------------------------------------------------

Exemple with --redmine option: 
===================
The script is started the 2016-02-22, the current work week will be 2016-02-22 - 2016-02-26
We are the Monday so we have just one day to display on this week

We have two Issues #12345 and #67890.
We will create two time entries of 0.5 hours for theses Issues

Output : 
    
    ------------------------------------------------
    |              TOGGL TIME ENTRIES              |
    ------------------------------------------------
    Here are your Toggl's time entries.
    From : 2016-02-22
    To : 2016-02-26
    
    # Date : 2015-01-02
        * Project : PROJECT 1
        |   Name : TIME ENTRY 1
        |         Duration (H:M:S) : 7:50:44
        |         Duration (Hours) : 7.846
        |         Duration (Days) : 0.980
        |   Name : TIME ENTRY 2
        |         Duration (H:M:S) : 2:30:00
        |         Duration (Hours) : 2.5
        |         Duration (Days) : 0.313
        > Duration total (Hours) : 10.346
        > Duration total (Days) : 1,293
        * Project : PROJECT TEST REDMINE
        |   Name : TIME ENTRY TEST & #12345 FIX AND #67890 DEV AND TEST
        |         Duration (H:M:S) : 1:30:00
        |         Duration (Hours) : 1
        |         Duration (Days) : 0.188
        |         Redmine : 
        |                 #12345 : OK
        |                 #67890 : OK
        > Duration total (Hours) : 1.5
        > Duration total (Days) : 0.188
    > Total (Hours) : 11.846
    > Total (Days) : 1.481
    ------------------------------------------------

As you can see a new line is displayed on the message "Redmine : #12345 : OK - #67890 : OK".
This will let you know which ticket has been created on Redmine (will display "ERROR" if an error has occured)

The same output with the --rtracker option : 

    ------------------------------------------------
    |              TOGGL TIME ENTRIES              |
    ------------------------------------------------
    Here are your Toggl's time entries.
    From : 2016-02-22
    To : 2016-02-26
    
    # Date : 2015-01-02
        * Project : PROJECT 1
        |   Name : TIME ENTRY 1
        |         Duration (H:M:S) : 7:50:44
        |         Duration (Hours) : 7.846
        |         Duration (Days) : 0.980
        |   Name : TIME ENTRY 2
        |         Duration (H:M:S) : 2:30:00
        |         Duration (Hours) : 2.5
        |         Duration (Days) : 0.313
        > Duration total (Hours) : 10.346
        > Duration total (Days) : 1,293
        * Project : PROJECT TEST REDMINE
        |   Name : TIME ENTRY TEST & #12345 FIX AND #67890 DEV AND TEST
        |         Duration (H:M:S) : 1:30:00
        |         Duration (Hours) : 1
        |         Duration (Days) : 0.188
        |         Redmine : 
        |                 #12345 : OK
        |                 #67890 : OK
        |         Infos : 
        |                 #12345 (Tracker : Issue - Project : PROJECT TEST REDMINE 1)
        |                 #67890 (Tracker : Evolution - Project : PROJECT TEST REDMINE 2)
        > Duration total (Hours) : 1.5
        > Duration total (Days) : 0.188
    > Total (Hours) : 11.846
    > Total (Days) : 1.481
    ------------------------------------------------


Todo :
===================
* test new smtplib auth (not fully tested) and maybe an email smtplib improvements
* better options management (maybe cfg file instead ?)
* general improvement
