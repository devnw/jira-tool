# jira-tool

[![Build Status](https://api.travis-ci.org/nortonlifelock/jira-tool.svg?branch=master)](https://travis-ci.org/nortonlifelock/jira-tool)
[![Go Report Card](https://goreportcard.com/badge/github.com/nortonlifelock/jira-tool)](https://goreportcard.com/report/github.com/nortonlifelock/jira-tool)
[![GoDoc](https://godoc.org/github.com/nortonlifelock/jira-tool?status.svg)](https://godoc.org/github.com/nortonlifelock/jira-tool)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0) [![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)

jira-tool

There are a variety of command line flags required to give the settings of the JIRA tool

-path to give the path to the CSV file containing the bulk changes

-file to give the filename containing the bulk changes

-url to give the address of the JIRA instance you're using

-slack to give an API key for a slack, and the JIRA tool will post status updates to your slack channel

-time to change the time format (default m/d/yy)

GoLang has a unique time formatting convention, here is more information regarding - https://pauladamsmith.com/blog/2011/05/go_time.html

An example execution may look like

jira-tool -time "1/2/06 3:04" -path "/Path/To/File" -file "file.csv" -url "http://myjira.com"

The username and password for the account making these changes are requested in the command line once the program begins

There are three commands supported: Create, Update, Delete

CSV formatting:

The first line of the CSV must describe the format that you're providing. The first entry of the CSV description line must always be the command, with the latter fields being the JIRA fields you're including, and can be in any order. If the status of the ticket is being changed, an assignee must also be supplied. Additionally, a comment field is required in Update commands for the tool to leave on the ticket's page.

An example of a CSV description line:

update,issue key,status,assignee,comment

The columns supported by the JIRA tool are:assets affected, assigned to, assignment group, cve references, cvss, comment, description, due date, ip address, mac address, method of discovery, operating system, priority, resolution date, scan errata, service ports, summary, ticket type, vendor references, vulnerability title

Issue key and title are interchangeable


Required Columns

Update

   issue key/title, comment

   if updating the status, an assignee/assigned to field is required

Create/Delete

   issue key/title

 

In the lines following the description line which describe the tickets you want to create/update/delete, the fields of the ticket must line up with the fields of the description line. First entry of the ticket lines (the entry that lines up with the command in the description line) must have the project that  you're update.


Examples

Bulk delete in project Aegis

delete, issue key

Aegis,Aegis-100

Aegis,Aegis-101

...

 

Bulk create in project Aegis

create, description, operating system, assignment group

Aegis, new vuln, windows, group1

Aegis, ticket description, ubuntu, group2

...

 

Bulk update in project Aegis

update, title, assignment group, status, assignee, comment

Aegis, Aegis-100, group1, Open, username, monthly rescans

Aegis, Aegis-101, group2, Open, username, monthly rescans