sedi.notify_teams
=========

Send messages to MS-Teams by a webhook, either by an Ansible handler or immediately by a task.

Requirements
------------

You need to [create a webhook](https://learn.microsoft.com/en-us/microsoftteams/platform/webhooks-and-connectors/how-to/add-incoming-webhook?tabs=dotnet) for your target Teams channel.

Role Variables
--------------

### Required

- `sdteams_title`: the title for the notification
- `sdteams_message`: a summary of the notification
- `sdteams_details`: detailed output
- `sdteams_date_time_format`: The date + time format used in the Teams message header
- `sdteams_webhook`: the full hook URI you got from MS-Teams configuration
- `sdteams_status`: one of `[ init, running, success, failure ]` - will also set an image accordingly (see `sdteams_status_image`)
- `sdteams_button_text`: set the button text
- `sdteams_button_url`: sets the URL the button will use

### Optional

- `sdteams_2nd_button_text`: specify the button text for a second button
- `sdteams_2nd_button_url`: specify the URL for that second button
- `sdteams_status_image`: a list of `<status>: "<url>"` values used to be displayed when specifying `sdteams_status`
- `sdteams_skip_notify`: if set to `true` this enables a global overwrite for skipping any notification (e.g. when you're debugging your ansible tasks)

Dependencies
------------

- Ansible v2.9 or later


# Usage

Using it as a handler
---------------------

```
# this will trigger the notification handler at the (very) end
- shell: echo foo
  notify: sdteams_notify
```

Using it as an immediate notification
-------------------------------------

```
# handlers will notify once at the very end only but you might want to 
# send a notification right NOW.
# -> this is handled by "tasks_from: notify_NOW.yml".
# note: this does not clear a triggered "sdteams_notify" handler, so if you use both 
# ("notify: sdteams_notify" + notify_NOW.yml) then you will get 1 notify due to the handler
# at the end and immediately any executed notify_NOW.yml.
#
# this is how to use it, of course you can specify all the sdteams variables
# elsewhere, as usual in Ansible:

- include_role:
    name: sedi.notify_teams
    tasks_from: notify_NOW.yml
  vars:
    sdteams_status: success
    sdteams_message: "MS-Teams notify role released!"
    sdteams_details: "You can find it at Ansible-Galaxy and on Github. Check it out!"
    sdteams_button_text: "Galaxy"
    sdteams_button_url: "https://galaxy.ansible.com/sedi/notify_teams"
    sdteams_2nd_button_text: "Github"
    sdteams_2nd_button_url: "https://github.com/secure-diversITy/ansible_role_notify-teams"
```

Example Playbook
----------------

For a complete example, including advanced methods like using `rescue` to trigger failures, see: [example-play.yml](https://github.com/secure-diversITy/ansible_role_notify-teams/blob/master/example-play.yml)

# License

GPL-3.0-only

# Author / Fork Information

Based on the great work of [@lucasdk3](https://github.com/lucasdk3/ansible-notify-teams).

Adapted and enhanced by me:

- make it ansible galaxy compatible
- added notification handler
- added an optional second button if specified
- bugfixes


