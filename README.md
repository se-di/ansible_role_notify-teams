Role Name
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

Example Playbook
----------------

see: [example-play.yml](https://github.com/secure-diversITy/ansible_role_notify-teams/blob/master/example-play.yml)

License
-------

GPL-3.0-only

Author Information
------------------

Based on the great work of [@lucasdk3](https://github.com/lucasdk3/ansible-notify-teams), adapted and enhanced to allow using it also as a notification handler instead of just a classical task.

