---
title: ChatrHub API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://chatrhub.com/signup/index.html'>Sign Up for a API Key</a>
  (Settings -> API -> Secret Key)

includes:
  - errors

search: true
---

# Introduction

Welcome to the ChatrHub API! You can use these endpoints to access and/or update agents, agent activity, groups, agent groups, chats, messages, visitors, reports, transcriptions, and tasks.  Settings currently need to be updated in the portal.

We have language bindings in Shell! You can view code examples in the dark area to the right. We have a python SDKs coming.

More information:

[Tutorials On Building Assistants](https://chatrhub.com/assistant_docs)

[Chat Setting Documentation](https://chatrhub.com/assistant_docs)

[FAQ](https://chatrhub.com/faq)

If you are looking for custom action webhook support please visit our Python library here: [chatendpoint](https://github.com/ChatrHub/chatendpoint).

# Authentication

> To authorize, use this code:

```shell
# With shell, you can pass the Authorization header with each request
curl "http://localhost:5000/api/v1/agents.json" \
    -H "Authorization: Bearer 123456789"
```

> Make sure to replace `123456789` with your API key.

ChatrHub uses JWT tokens (API keys) to authorize API access. Each ChatrHub account is given one key.  Find it under Settings -> API -> Secret Key.  Signup for a new account on our [website](http://chatrhub.com/signup/index.html).

ChatrHub expects the API key with all API requests in a header that looks like the following:

`Authorization: Bearer api_key`

<aside class="notice">
You must replace <code>api_key</code> with your account's API key.
</aside>

# Agent Activity

## Get Agent Activity

```shell
curl "http://localhost:5000/api/v1/agent_activities/agent_id/1.json?start_date=2018-05-01&end_date=2019-05-01" \
    -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhZ2VudF9pZCI6MSwiYWNjZXNzX3R5cGUiOiJhcGkiLCJhcGlfaWQiOiJ6ZDdyYmRuNjN2cWdiZHVma2ltdiJ9.jWNHTojO6E9myLuATQWg8mwaysKb37Q3PXeeqTOj9lg"
```

> The above command returns JSON structured like this:

```json
{
    "data": [
        {
            "type": "agent_activities",
            "id": 1,
            "attributes": {
                "updt_dt": "2018-06-19T13:00:00+00:00",
                "client_id": 1,
                "create_by": 1,
                "agent_id": 1,
                "create_dt": "2018-06-19T13:00:00+00:00",
                "trmnt_ind": false,
                "updt_by": 1,
                "status": "available"
            }
        },
        {
            "type": "agent_activities",
            "id": 1,
            "attributes": {
                "updt_dt": "2018-06-19T13:05:00+00:00",
                "client_id": 1,
                "create_by": 1,
                "agent_id": 1,
                "create_dt": "2018-06-19T13:05:00+00:00",
                "trmnt_ind": false,
                "updt_by": 1,
                "status": "unavailable"
            }
        },
        {
            "type": "agent_activities",
            "id": 1,
            "attributes": {
                "updt_dt": "2018-06-19T13:10:00+00:00",
                "client_id": 1,
                "create_by": 1,
                "agent_id": 1,
                "create_dt": "2018-06-19T13:10:00+00:00",
                "trmnt_ind": false,
                "updt_by": 1,
                "status": "offline"
            }
        }
    ]
}
```

This endpoint returns the historical availability codes of an agent in 5 minute intervals.

Status can be either "available", "unavailable", or "offline".

### HTTP Request

`GET http://localhost:5000/api/v1/agent_activities/agent_id/<agent_id>.json?start_date=<start_date>&end_date=<end_date>`

### Query Parameters

Parameter | Description | Required?
--------- | ----------- | -----------
agent_id | The ID of the agent for the report. ID can be sourced from the Agents endpoint. | Yes
start_date | The start date filter for the report. Format: YYYY-MM-DD | Yes
end_date | The end date filter for the report. Format: YYYY-MM-DD | Yes

<aside class="notice">
All parameters are required.
</aside>

### Response Body

Parameter | Description
--------- | -----------
create_dt | Date and time of snapshot
status | Staus of agent.  See below.

### Status Code Descriptions

Status Code | Descriptions
--------- | -----------
available | Agent is available to chat with new visitors.  Represented by green bar in the portal's agent tab.
unavailable | Agent can chat with new or existing visitors, but new visitors cannot start a new conversation with the agent. Used when the agent can no longer handle more conversations. Represented by a yellow bar in the portal's agent tab.
offline | Agent is not connected to XMPP and cannot chat with new or current conversations.  Represented by a red bar in the portal's agent tab.







# Agent Groups

## List Groups by Agent

```shell
curl "http://localhost:5000/api/v1/agent_groups/1.json" \
    -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhZ2VudF9pZCI6MSwiYWNjZXNzX3R5cGUiOiJhcGkiLCJhcGlfaWQiOiJ6ZDdyYmRuNjN2cWdiZHVma2ltdiJ9.jWNHTojO6E9myLuATQWg8mwaysKb37Q3PXeeqTOj9lg"
```

> The above command returns JSON structured like this:

```json
{
    "data": [{
        "type": "agent_groups",
        "id": 1,
        "attributes": {
            "group": {
                SEE GROUP
            },
            "updt_by": null,
            "trmnt_ind": false,
            "agent": {
                SEE AGENT
            },
            "group_id": 10245,
            "updt_dt": null,
            "create_by": 1,
            "create_dt": "2018-06-19T20:01:41+00:00",
            "is_assigned": true,
            "client_id": 1,
            "agent_id": 1
        }
    }]
}
```

This endpoint lists what groups are assigned to an agent.

The Group and Agent information is provided in nested attributes.

### HTTP Request

`GET http://localhost:5000/api/v1/agent_groups/<agent_id>.json`

### Query Parameters

Parameter | Description
--------- | -----------
agent_id | The ID of the agent for the report. ID can be sourced from the Agents endpoint.

<aside class="notice">
All parameters are required.
</aside>

### Response Body

Parameter | Description
--------- | -----------
is_assigned | If group is assigned to the agent.
agent_id | Agent ID that is/is not associated with the group ID.
group_id | Group ID that is associated to the agent.
agent | Nested agent data.  See agents endpoint.
group | Nested group data.  See groups endpoint.
updt_by | Agent ID who updated the agent/link.
updt_dt | Date and time agent/group linking was updated.
create_by | Agent ID who created the agent/group link.
create_dt | Date and time agent/group linking was created.






## Get Agent Group Assignment

```shell
curl "http://localhost:5000/api/v1/agent_groups/agent_id/1/group_id/10204.json" \
    -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhZ2VudF9pZCI6MSwiYWNjZXNzX3R5cGUiOiJhcGkiLCJhcGlfaWQiOiJ6ZDdyYmRuNjN2cWdiZHVma2ltdiJ9.jWNHTojO6E9myLuATQWg8mwaysKb37Q3PXeeqTOj9lg"
```

> The above command returns JSON structured like this:

```json
{
    "data": {
        "type": "agent_groups",
        "id": 1,
        "attributes": {
            "group": {
                SEE GROUP
            },
            "updt_by": null,
            "trmnt_ind": false,
            "agent": {
                SEE AGENT
            },
            "group_id": 10245,
            "updt_dt": null,
            "create_by": 1,
            "create_dt": "2018-06-19T20:01:41+00:00",
            "is_assigned": true,
            "client_id": 1,
            "agent_id": 1
        }
    }
}
```

This endpoint returns an agent/group assignment object.  For example, if you wanted to know if one agent was assigned or unassigned to a particular group.  If no object is returned, the agent is not associated to the group, the agent/group combination does not exist, or the agent_id/group_id is not owned by that client.

The Group and Agent information is provided in the nested attributes.

### HTTP Request

`GET http://localhost:5000/api/v1/agent_groups/agent_id/<agent_id>/group_id/<group_id>.json`

### Query Parameters

Parameter | Description | Required?
--------- | ----------- | -----------
agent_id | The ID of the agent. ID can be sourced from the Agents endpoint. | Yes
group_id | The ID of the group. ID can be sourced from the Agents endpoint. | Yes

<aside class="notice">
All parameters are required.
</aside>

### Response Body

See List Groups by Agent







## Assign Agent to Group

```shell
curl -X "POST" "http://localhost:5000/api/v1/agent_groups/1.json" \
    -d '{"data": {"type": "agent_groups", "attributes": {"agent_id": 1, "group_id": 10204, "is_assigned": false}}}' \
    -H 'Content-Type: application/json' \
    -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhZ2VudF9pZCI6MSwiYWNjZXNzX3R5cGUiOiJhcGkiLCJhcGlfaWQiOiJ6ZDdyYmRuNjN2cWdiZHVma2ltdiJ9.jWNHTojO6E9myLuATQWg8mwaysKb37Q3PXeeqTOj9lg"
```

> Request Body Example

```json
{
    "data": {
        "type": "agent_groups",
        "attributes": {
            "agent_id": 1,
            "group_id": 10204,
            "is_assigned": true
        }
    }
}
```


> Response Body Example:

```json
{
    "data": [{
        "type": "agent_groups",
        "id": 1,
        "attributes": {
            "group": {
                SEE GROUP
            },
            "updt_by": null,
            "trmnt_ind": false,
            "agent": {
                SEE AGENT
            },
            "group_id": 10245,
            "updt_dt": null,
            "create_by": 1,
            "create_dt": "2018-06-19T20:01:41+00:00",
            "is_assigned": true,
            "client_id": 1,
            "agent_id": 1
        }
    }]
}
```

This endpoint will update the assigned group for an agent.

It also returns the final updated assignment object.

The Group and Agent information is provided in nested attributes.

### HTTP Request

`POST http://localhost:5000/api/v1/agent_groups/<agent_id>.json`

### Query Parameters

Parameter | Description | Required?
--------- | ----------- | -----------
agent_id | The ID of the agent you are updating. See Agents endpoint. | Yes

### Request Body Parameters

Parameter | Description | Required?
--------- | ----------- | -----------
agent_id | The ID of the agent you are updating. See Agents endpoint. | Yes
group_id | The ID of the group you are assigning.  See Groups endpoint. | Yes
is_assigned | 'true' or 'false' | Yes

<aside class="notice">
All parameters are required.
</aside>

### Response Body

See List Groups by Agent






## Remove Agent From Group

```shell
curl -X "DELETE" "http://localhost:5000/api/v1/agent_groups/agent_id/1/group_id/10204.json" \
    -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhZ2VudF9pZCI6MSwiYWNjZXNzX3R5cGUiOiJhcGkiLCJhcGlfaWQiOiJ6ZDdyYmRuNjN2cWdiZHVma2ltdiJ9.jWNHTojO6E9myLuATQWg8mwaysKb37Q3PXeeqTOj9lg"
```

> Response Body Example:

```json
{
    "success": "Deleted"
}
```

This endpoint will remove an agent from an existing group.

The Group and Agent information is provided in the nested attributes.

### HTTP Request

`DELETE http://localhost:5000/api/v1/agent_groups/agent_id/<agent_id>/group_id/<group_id>.json`

### Query Parameters

Parameter | Description
--------- | -----------
agent_id | The ID of the agent. See Agents endpoint. (Required)
group_id | The ID of the group. See Groups endpoint. (Required)


















# Agents

## List Agents

```shell
curl -X "GET" "http://localhost:5000/api/v1/agents.json" \
    -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhZ2VudF9pZCI6MSwiYWNjZXNzX3R5cGUiOiJhcGkiLCJhcGlfaWQiOiJ6ZDdyYmRuNjN2cWdiZHVma2ltdiJ9.jWNHTojO6E9myLuATQWg8mwaysKb37Q3PXeeqTOj9lg"
```

> The above command returns JSON structured like this:

```json
{
    "data": [
        {
            "type": "agents",
            "id": 4,
            "attributes": {
                "username": "5b2aaeb29fb5ba6af2e3ae2e",
                "is_assign_training_tasks": false,
                "is_assign_operational_task_by_variable": false,
                "client_id": 1,
                "create_dt": "2018-06-20T19:44:50+00:00",
                "updt_dt": null,
                "updt_by": null,
                "is_assign_training_task_send_email": false,
                "trmnt_ind": 0,
                "create_by": 1,
                "assign_operational_task_variable": null,
                "is_bot": true,
                "is_assign_operational_tasks": false,
                "is_taking_chats": true,
                "full_name": "123",
                "is_agent_setup": false,
                "assign_operational_task_values": "[]",
                "agent_id": "4",
                "is_unsubscribe": true,
                "authorization_level": 1,
                "xmpp_password": "4uwbe8mkf6gqf8uxxwl0",
                "email": "",
                "is_assign_operational_task_send_email": false
            },
        }
    ]
}
```

This endpoint returns a list of all agents.

### HTTP Request

Get agent list:

`GET http://localhost:5000/api/v1/agents.json`

Search by agent username:

`GET http://localhost:5000/api/v1/agents.json?agent_username=<agent_username>`

### Query Parameters

Parameter | Description | Required?
--------- | ----------- | -----------
agent_username | Search by agent username | No

### Response Body

Parameter | Description
--------- | -----------
agent_id | ID of the agent
username | Username of the human or bot agent (String)
email | Email of agent.
authorization_level | Authorization Level of Agent | 1 -> Agent | 3-> Supervisor | 5 -> Admin
xmpp_password | Password to XMPP
is_assign_training_tasks | If training tasks are assigned to this agent.
is_assign_operational_task_by_variable | Should the dialog variable be considered when assigning a task to this agent.
assign_operational_task_variable | Name of the dialog variable involved in the decision to assign this agent a task. See is_assign_operational_task_by_variable and assign_operational_task_values
assign_operational_task_values | Searlized JSON string representing a list of all variable values that will trigger a task to be sent to this agent.  See assign_operational_task_variable
is_assign_training_task_send_email | Should a new training task kickoff an email to the agent.
is_assign_operational_task_send_email | Should a new operational task kickoff an email to the agent.
create_dt | Date and time this object was created.
updt_dt | Date and time this object was updated.
display_name | Name of agent
create_by | Agent ID that created this agent.
is_bot | Is this agent a human or bot
is_taking_chats | Is agent available or unavailable if online.
full_name | Full name of agent visible to other agents and visitors (Customers).
is_agent_setup | Has agent updated profile image?
is_unsubscribe | Has the agent unsubscribed from emails?







## Get Agent

```shell
curl -X "GET" "http://localhost:5000/api/v1/agents/1.json" \
    -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhZ2VudF9pZCI6MSwiYWNjZXNzX3R5cGUiOiJhcGkiLCJhcGlfaWQiOiJ6ZDdyYmRuNjN2cWdiZHVma2ltdiJ9.jWNHTojO6E9myLuATQWg8mwaysKb37Q3PXeeqTOj9lg"
```

> The above command returns JSON structured like this:

```json
{
    "data": [
        {
            "type": "agents",
            "id": 4,
            "attributes": {
                "username": "5b2aaeb29fb5ba6af2e3ae2e",
                "is_assign_training_tasks": false,
                "is_assign_operational_task_by_variable": false,
                "client_id": 1,
                "create_dt": "2018-06-20T19:44:50+00:00",
                "updt_dt": null,
                "updt_by": null,
                "is_assign_training_task_send_email": false,
                "trmnt_ind": 0,
                "create_by": 1,
                "assign_operational_task_variable": null,
                "is_bot": true,
                "is_assign_operational_tasks": false,
                "is_taking_chats": true,
                "full_name": "123",
                "is_agent_setup": false,
                "assign_operational_task_values": "[]",
                "agent_id": "4",
                "is_unsubscribe": true,
                "authorization_level": 1,
                "xmpp_password": "4uwbe8mkf6gqf8uxxwl0",
                "email": "",
                "is_assign_operational_task_send_email": false
            },
        }
    ]
}
```

This endpoint returns one agent object by ID.

### HTTP Request

`GET http://localhost:5000/api/v1/agents/<agent_id>.json`

### Query Parameters

Parameter | Description
--------- | -----------
agent_id | The ID of the agent. (Required)

### Response Body

See List Agents







## Update Agent

```shell
curl -X "PATCH" "http://localhost:5000/api/v1/agents/1.json" \
    -d '{"data": {"type": "agents", "attributes": {"full_name": "Joe", "email": "joe@example.com"}}}' \
    -H 'Content-Type: application/json' \
    -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhZ2VudF9pZCI6MSwiYWNjZXNzX3R5cGUiOiJhcGkiLCJhcGlfaWQiOiJ6ZDdyYmRuNjN2cWdiZHVma2ltdiJ9.jWNHTojO6E9myLuATQWg8mwaysKb37Q3PXeeqTOj9lg"
```

> Request Body Example

```json
{
    "data": {
        "type": "agents",
        "attributes": {
            "full_name": "Joe",
            "email": "joe@example.com"
        }
    }
}
```


> Response Body Example:

```json
{
  "data": {
    "type": "agents",
    "attributes": {
      "username": "unittest500",
      "create_dt": "2018-06-20T16:11:21+00:00",
      "assign_operational_task_variable": null,
      "create_by": 1,
      "updt_by": 1,
      "email": "joe@example.com",
      "avatar_img": "x.png",
      "is_assign_training_tasks": true,
      "agent_id": "1",
      "trmnt_ind": 0,
      "updt_dt": "2018-06-22T01:03:30+00:00",
      "authorization_level": 5,
      "is_assign_operational_tasks": true,
      "is_bot": false,
      "assign_operational_task_values": "[]",
      "client_id": 1,
      "display_name": "Test Display",
      "xmpp_password": "7f94mc9grrxnb4y",
      "is_agent_setup": true,
      "full_name": "Joe",
      "is_assign_training_task_send_email": true,
      "is_taking_chats": true,
      "is_unsubscribe": false,
      "is_assign_operational_task_send_email": true,
      "is_assign_operational_task_by_variable": false,
      "is_temp_login": false
    },
    "id": 1
  }
}
```

This endpoint will update agent attributes.

It also returns the final updated agent object.

### HTTP Request

`PATCH http://localhost:5000/api/v1/agents/<agent_id>.json`

### Query Parameters

Parameter | Description | Required?
--------- | ----------- | -----------
agent_id | The ID of the agent you are updating. See Agents endpoint. | Yes

### Request Body Parameters

Parameter | Description | Required?
--------- | ----------- | -----------
email | Email of agent. | No
authorization_level | Authorization Level of Agent ( 1 -> Agent, 3-> Supervisor or 5 -> Admin) | No
is_assign_training_tasks | If training tasks are assigned to this agent. | No
is_assign_operational_task_by_variable | Should the dialog variable be considered when assigning a task to this agent. | No
assign_operational_task_variable | Name of the dialog variable involved in the decision to assign this agent a task. See is_assign_operational_task_by_variable and assign_operational_task_values | No
assign_operational_task_values | Searlized JSON string representing a list of all variable values that will trigger a task to be sent to this agent.  See assign_operational_task_variable | No
is_assign_training_task_send_email | Should a new training task kickoff an email to the agent. | No
is_assign_operational_task_send_email | Should a new operational task kickoff an email to the agent. | No
is_bot | Is this agent a human or bot | No
is_taking_chats | Is agent available or unavailable if online. | No
full_name | Full name of agent visible to other agents and visitors (Customers). | No
is_agent_setup | Has agent updated profile image? | No
is_unsubscribe | Has the agent unsubscribed from emails? | No

### Response Body

See Get Agent







## Invite Agent

```shell
curl -X "POST" "http://localhost:5000/api/v1/agents/invite.json" \
    -d '{"data": {"type": "agents", "attributes": {"full_name": "Joe Schmo", "authorization_level": 1, "email": "test@example123sdfuiow.com"}}}' \
    -H 'Content-Type: application/json' \
    -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhZ2VudF9pZCI6MSwiYWNjZXNzX3R5cGUiOiJhcGkiLCJhcGlfaWQiOiJ6ZDdyYmRuNjN2cWdiZHVma2ltdiJ9.jWNHTojO6E9myLuATQWg8mwaysKb37Q3PXeeqTOj9lg"
```



> Request Body Example

```json
{
    "data": {
        "type": "agents",
        "attributes": {
            "full_name": "Joe",
            "authorization_level": 1,
            "email": "ddj209@gmail.com"
        }
    }
}
```


> Response Body Example:

```json
{
    "data": {
        "type": "agents",
        "id": 4,
        "attributes": {
            "username": "5b2aaeb29fb5ba6af2e3ae2e",
            "is_assign_training_tasks": false,
            "is_assign_operational_task_by_variable": false,
            "client_id": 1,
            "create_dt": "2018-06-20T19:44:50+00:00",
            "updt_dt": null,
            "updt_by": null,
            "is_assign_training_task_send_email": false,
            "trmnt_ind": 0,
            "create_by": 1,
            "assign_operational_task_variable": null,
            "is_bot": true,
            "is_assign_operational_tasks": false,
            "is_taking_chats": true,
            "full_name": "123",
            "is_agent_setup": false,
            "assign_operational_task_values": "[]",
            "agent_id": "4",
            "is_unsubscribe": true,
            "authorization_level": 1,
            "xmpp_password": "4uwbe8mkf6gqf8uxxwl0",
            "email": "",
            "is_assign_operational_task_send_email": false
        },
    }
}
```

This endpoint will add an agent and send an email invitation to the user.

It also returns the agent object.

### HTTP Request

`POST http://localhost:5000/api/v1/agents/invite.json`

### Request Body Parameters

Parameter | Description | Required?
--------- | ----------- | -----------
full_name | Name of agent. | Yes
authorization_level | The permissions of the user (1 -> Agent, 3 -> Supervisor, or 5 -> Admin) | Yes
email | Email of user.  Will be used to send an invitation to the user. | Yes
is_assign_training_tasks | Should this user be assigned training tasks. | Default false
is_assign_training_task_send_email | Should this user be assigned training tasks | Default false
is_assign_operational_tasks | Should this user be assigned operational tasks | Default false
is_assign_operational_task_by_variable | Should this user be assigned an operational task by variable | Default false
assign_operational_task_variable |  Variable to determine if an agent should be assigned a task | No
assign_operational_task_values | JSON serialized list. Assign if variable contains any of these variables | No

### Response Body

See List Agents












# Chats

## List Chats

```shell
curl -X "GET" "http://localhost:5000/api/v1/chats.json?start_date=1529083167000&end_date=1534353567000" \
    -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhZ2VudF9pZCI6MSwiYWNjZXNzX3R5cGUiOiJhcGkiLCJhcGlfaWQiOiJ6ZDdyYmRuNjN2cWdiZHVma2ltdiJ9.jWNHTojO6E9myLuATQWg8mwaysKb37Q3PXeeqTOj9lg"
```

> The above command returns JSON structured like this:

```json
{
  "data": [{
    "type": "chats",
    "attributes": {
      "is_billable": 0,
      "is_missed": null,
      "tag": null,
      "overall_rating": null,
      "group_id": null,
      "group": {
          SEE GROUP
      },
      "is_beat_out": 1,
      "knowledge_rating": null,
      "response_delay": null,
      "create_dt": "2018-06-21T01:50:49+00:00",
      "create_by": 1,
      "is_feedback_requested": 0,
      "client_id": 1,
      "average_rating": null,
      "agent_id_to": null,
      "is_ended": 1,
      "responsive_rating": null,
      "agent_id": 4,
      "agent": {
          SEE AGENT
      },
      "duration": null,
      "ended_rsn_cd": null,
      "updt_dt": "2018-06-21T01:58:09+00:00",
      "visitor_id": 2,
      "visitor": {
          SEE VISITOR
      },
      "trmnt_ind": false,
      "frendly_rating": null,
      "transfer_to_agent_id": null,
      "feedback": null,
      "updt_by": 1
    },
    "id": 2
  }]
}
```

This endpoint lists all chats that meet the query parameter filters.

### HTTP Request

Get chat list:

`GET http://localhost:5000/api/v1/chats.json`

### Query Parameters

Parameter | Description | Required?
--------- | ----------- | -----------
start_date | Start date of filter.  Format: Epoch in milliseconds | Yes
end_date | End date of filter.  Format: Epoch in milliseconds | Yes
agent_id | ID of agent.  See agents endpoint.  | No
visitor_id | ID of visitor. See visitors endpoint. | No
group_id | ID of group.  See groups endpoint. | No
tag | Tag of conversation.  String | No
rating | 'poor_chats', 'ok_chats', or 'great_chats' | No
missed | 'missed_chats' or 'serviced_chats' | No

### Response Body

Parameter | Description
--------- | -----------
is_billable | Is the conversation billable?
is_missed | Was the conversation missed?
tag | Tag string of chat.
overall_rating | 1 -> 3 integer.  How well did the agent perform overall.
frendly_rating | 1 -> 3 integer.  How friendly was the agent.
responsive_rating | 1 -> 3 integer. How responsive was the agent.
knowledge_rating | 1 -> 3 integer. How knowledgable was the agent.
average_rating | % of all the ratings above.
group_id | ID of the group.  See groups endpoint.
group | Group object if group_id is present.
is_beat_out | Was the conversation beat out by another agent.  When routing = "All Agents"
response_delay | Time in seconds for the agent to respond.
create_dt | Date the conversation was initiated.
is_feedback_requested | Was feedback requested either manually or automatically
client_id | The client ID of the chat.
agent_id_to | The agent ID if its an Agent to Agent chat.
is_ended | Has the conversation ended.
agent_id | The agent ID if its an Agent to Visitor chat.
agent | Agent object.  See agents endpoint.
duration | The duration in seconds of the chat.
ended_rsn_cd | The reason the chat has ended.  ('offline', 'no_reply', 'inactive')
visitor_id | The ID of the visitor if its an Agent to Visitor chat.
visitor | Visitor object.  See visitors endpoint.
transfer_to_agent_id | Was the chat transferred and if so to what agent.
feedback | Feedback from the visitor.






## Get Chat

```shell
curl -X "GET" "http://localhost:5000/api/v1/chats/1.json" \
    -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhZ2VudF9pZCI6MSwiYWNjZXNzX3R5cGUiOiJhcGkiLCJhcGlfaWQiOiJ6ZDdyYmRuNjN2cWdiZHVma2ltdiJ9.jWNHTojO6E9myLuATQWg8mwaysKb37Q3PXeeqTOj9lg"
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "type": "chats",
    "id": 2,
    "attributes": {
      "is_billable": 0,
      "is_missed": null,
      "tag": null,
      "overall_rating": null,
      "group_id": null,
      "group": {
          SEE GROUP
      },
      "is_beat_out": 1,
      "knowledge_rating": null,
      "response_delay": null,
      "create_dt": "2018-06-21T01:50:49+00:00",
      "create_by": 1,
      "is_feedback_requested": 0,
      "client_id": 1,
      "average_rating": null,
      "agent_id_to": null,
      "is_ended": 1,
      "responsive_rating": null,
      "agent_id": 4,
      "agent": {
          SEE AGENT
      },
      "duration": null,
      "ended_rsn_cd": null,
      "updt_dt": "2018-06-21T01:58:09+00:00",
      "visitor_id": 2,
      "visitor": {
          SEE VISITOR
      },
      "trmnt_ind": false,
      "frendly_rating": null,
      "transfer_to_agent_id": null,
      "feedback": null,
      "updt_by": 1
    }
  }
}
```

This endpoint returns one chat object by ID.

### HTTP Request

`GET http://localhost:5000/api/v1/chats/<chat_id>.json`

### Query Parameters

Parameter | Description | Required?
--------- | ----------- | -----------
chat_id | The ID of the chat for which you would like to transfer. | Required

### Response Body

See List Chats








## Update Chat Tag

```shell
curl -X "PATCH" "http://localhost:5000/api/v1/chat/1.json" \
    -d '{"data": {"type": "chats", "attributes": {"tag": "New Tag"}}}' \
    -H 'Content-Type: application/json' \
    -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhZ2VudF9pZCI6MSwiYWNjZXNzX3R5cGUiOiJhcGkiLCJhcGlfaWQiOiJ6ZDdyYmRuNjN2cWdiZHVma2ltdiJ9.jWNHTojO6E9myLuATQWg8mwaysKb37Q3PXeeqTOj9lg"
```

> Request Body Example

```json
{
    "data": {
        "type": "chats",
        "attributes": {
            "tag": "New Tag"
        }
    }
}
```


> Response Body Example:

```json
{
  "data": {
    "type": "chats",
    "id": 2,
    "attributes": {
      "is_billable": 0,
      "is_missed": null,
      "tag": "New Tag",
      "overall_rating": null,
      "group_id": null,
      "group": {
          SEE GROUP
      },
      "is_beat_out": 1,
      "knowledge_rating": null,
      "response_delay": null,
      "create_dt": "2018-06-21T01:50:49+00:00",
      "create_by": 1,
      "is_feedback_requested": 0,
      "client_id": 1,
      "average_rating": null,
      "agent_id_to": null,
      "is_ended": 1,
      "responsive_rating": null,
      "agent_id": 4,
      "agent": {
          SEE AGENT
      },
      "duration": null,
      "ended_rsn_cd": null,
      "updt_dt": "2018-06-21T01:58:09+00:00",
      "visitor_id": 2,
      "visitor": {
          SEE VISITOR
      },
      "trmnt_ind": false,
      "frendly_rating": null,
      "transfer_to_agent_id": null,
      "feedback": null,
      "updt_by": 1
    }
  }
}
```

This endpoint will update the tag of a chat.

A tag is a string representing what happened on the call and is manually updated by the agent or set during the AI dialog.

It also returns the final updated chat object.

### HTTP Request

`PATCH http://localhost:5000/api/v1/chats/<chat_id>.json`

### Query Parameters

Parameter | Description | Required?
--------- | ----------- | -----------
chat_id | The ID of the chat you are updating. | Yes

### Request Body Parameters

Parameter | Description | Required?
--------- | ----------- | -----------
tag | String | Yes

### Response Body

See Get Chat







## Chat Reports

```shell
curl -X "GET" "http://localhost:5000/api/v1/chats/report.json?start_date=2018-01-01&end_date=2018-12-01" \
    -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhZ2VudF9pZCI6MSwiYWNjZXNzX3R5cGUiOiJhcGkiLCJhcGlfaWQiOiJ6ZDdyYmRuNjN2cWdiZHVma2ltdiJ9.jWNHTojO6E9myLuATQWg8mwaysKb37Q3PXeeqTOj9lg"
```



> Response Body Example:

```json
{
    "data": {
        "type": "report",
        "id": 2,
        "attributes": {
            "missed_chats": null,
            "overall_rating": 3,
            "knowledge_rating": 2,
            "average_response_delay": null,
            "average_rating": 87.0,
            "average_duration": null,
            "responsive_rating": 3,
            "ok_chats_count": 0,
            "total_ratings": 1,
            "total_chats": 2,
            "great_chats_count": 1,
            "frendly_rating": 3,
            "poor_chats_count": 0
        }
    }
}
```


This endpoint will summarize chat volumes, duration, and agent performance over a date range.

### HTTP Request

`GET http://localhost:5000/api/v1/agents/report.json`

### Query Parameters

Parameter | Description | Required?
--------- | ----------- | -----------
start_date | Start date filter. | Yes
end_date | End date filter. | Yes
agent_id | Agent ID filter.  See Agents endpoint | No
group_id | Group ID filter.  See Groups endpoint | No

### Response Body

Parameter | Description
--------- | -----------
missed_chats | Number of missed chats (Integer)
average_rating | Average Chat Rating (Percentage)
overall_rating | Average overall rating (Percentage)
knowledge_rating | Average knowledge rating (Percentage)
responsive_rating | Average Responsiveness Rating (Percentage)
frendly_rating | Average Friendliness rating (Percentage)
total_ratings | Total number of chats that have a rating (Integer)
total_chats | Total number of chats (Integer)
great_chats_count | Count of chats that were marked as GREAT (Integer)
ok_chats_count | Count of chats that were marked as OK. (Integer)
poor_chats_count | Count of chats that were marked as POOR (Integer)
average_response_delay | Average Response Delay (Integer)
average_duration | Average Chat Duration (Integer)



## Transfer Chat

```shell
curl -X "GET" "http://localhost:5000/api/v1/chats/transfer/1.json?agent_username_from=johnsmith1&agent_username_to=jennybrown1" \
    -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhZ2VudF9pZCI6MSwiYWNjZXNzX3R5cGUiOiJhcGkiLCJhcGlfaWQiOiJ6ZDdyYmRuNjN2cWdiZHVma2ltdiJ9.jWNHTojO6E9myLuATQWg8mwaysKb37Q3PXeeqTOj9lg"
```

> The above command returns JSON structured like this:

```json
{
    "success": "Sent Transfer Action"
}
```

This endpoint will transfer a visitor from one agent to another.

After making the transfer request, a message will be sent to the agent being transferred to and if that agent responds, the chat will be transferred.

### HTTP Request

`GET http://localhost:5000/api/v1/chats/transfer/<chat_id>.json?agent_username_from=<agent_username_from>&agent_username_to=<agent_username_to>`

### Query Parameters

Parameter | Description | Required?
--------- | ----------- | -----------
chat_id | The ID of the chat for which you would like to transfer. | Yes
agent_username_from | The username of the agent you want to transfer from. | Yes
agent_username_to | The username of the agent you want to transfer to. | Yes

### Response Body

Response | Description
--------- | -----------
"Invalid usernames or authentication." | Transfer failed. Supplied the wrong usernames or chat_id
"Sent Transfer Action" | Transfer request sent.  Transfer to agent must reply to complete transfer.















# Groups

## List Groups

```shell
curl -X "GET" "http://localhost:5000/api/v1/groups.json" \
    -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhZ2VudF9pZCI6MSwiYWNjZXNzX3R5cGUiOiJhcGkiLCJhcGlfaWQiOiJ6ZDdyYmRuNjN2cWdiZHVma2ltdiJ9.jWNHTojO6E9myLuATQWg8mwaysKb37Q3PXeeqTOj9lg"
```

> The above command returns JSON structured like this:

```json
{
  "data": [{
    "type": "groups",
    "attributes": {
      "group_name": "Sales",
      "create_by": 1,
      "client_id": 1,
      "updt_by": null,
      "updt_dt": null,
      "trmnt_ind": false,
      "create_dt": "2018-06-21T01:59:55+00:00",
      "system_group": false,
      "visitor_phone_matches": "[\"123\"]",
      "visitor_email_matches": "[\"\"]",
      "visitor_referrer_url_matches": "[\"\"]",
      "visitor_company_matches": "[\"\"]",
      "visitor_state_matches": "[\"\"]",
      "visitor_zip_matches": "[\"\"]",
      "visitor_city_matches": "[\"\"]",
      "visitor_country_matches": "[\"\"]",
      "visitor_current_url_matches": "[\"\"]",
    },
    "id": 10204
  }]
}
```

This endpoint lists all groups.

Groups allow you to visually separate your agents in the chat console and they also facilitate routing.

### HTTP Request

Get group list:

`GET http://localhost:5000/api/v1/groups.json`

### Response Body

Parameter | Description
--------- | -----------
group_name | Name of group
create_by | Agent ID of agent that created group
updt_by | Agent ID of agent that updated group
updt_dt | The date and time the object was last updated.
create_dt | The date and time the object was last created.
visitor_phone_matches | List of all phone numbers that the group should match (Stringified JSON)
visitor_email_matches | List of all emails that the group should match (Stringified JSON)
visitor_current_url_matches | List of all current urls that the group should match (Stringified JSON)
visitor_referrer_url_matches | List of all referrer urls that the group should match (Stringified JSON)
visitor_company_matches | List of all company names that the group should match (Stringified JSON)
visitor_state_matches | List of all states (ISO Short Code) that the group should match (Stringified JSON)
visitor_zip_matches | List of all zip codes that the group should match (Stringified JSON)
visitor_city_matches | List of all cities that the group should match (Stringified JSON)
visitor_country_matches | List of all countries (ISO Short Code) that the group should match (Stringified JSON)






## Get Group

```shell
curl -X "GET" "http://localhost:5000/api/v1/groups/10204.json" \
    -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhZ2VudF9pZCI6MSwiYWNjZXNzX3R5cGUiOiJhcGkiLCJhcGlfaWQiOiJ6ZDdyYmRuNjN2cWdiZHVma2ltdiJ9.jWNHTojO6E9myLuATQWg8mwaysKb37Q3PXeeqTOj9lg"
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "type": "groups",
    "attributes": {
      "group_type": "CUSTOM",
      "client_id": 1,
      "group_name": "Sales",
      "visitor_zip_matches": "[\"\"]",
      "visitor_state_matches": "[\"\"]",
      "create_dt": "2018-06-21T01:59:55+00:00",
      "visitor_email_matches": "[\"\"]",
      "visitor_country_matches": "[\"\"]",
      "visitor_company_matches": "[\"\"]",
      "system_group": false,
      "visitor_phone_matches": "[\"123\"]",
      "visitor_current_url_matches": "[\"\"]",
      "updt_by": null,
      "visitor_city_matches": "[\"\"]",
      "trmnt_ind": false,
      "updt_dt": null,
      "visitor_referrer_url_matches": "[\"\"]",
      "create_by": 1
    },
    "id": 10204
  }
}
```

This endpoint returns one group object.

Groups allow you to visually separate your agents in the chat console and they also facilitate routing.

### HTTP Request

Get group list:

`GET http://localhost:5000/api/v1/groups/<group_id>.json`

### Query Parameters

Parameter | Description | Required?
--------- | ----------- | -----------
group_id | ID of group to return. | Yes

### Response Body

See List Groups






## Add Group

```shell
curl -X "POST" "http://localhost:5000/api/v1/groups.json" \
    -d '{"data": {"type": "groups", "attributes": {"group_name": "New Group", "visitor_phone_matches": "[\"312-555-9323\"]"}}}' \
    -H 'Content-Type: application/json' \
    -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhZ2VudF9pZCI6MSwiYWNjZXNzX3R5cGUiOiJhcGkiLCJhcGlfaWQiOiJ6ZDdyYmRuNjN2cWdiZHVma2ltdiJ9.jWNHTojO6E9myLuATQWg8mwaysKb37Q3PXeeqTOj9lg"
```

> Request Body Example

```json
{
    "data": {
        "type": "groups",
        "attributes": {
            "group_name": "New Group",
            "visitor_phone_matches": "[\"312-555-9323\"]"
        }
    }
}
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "type": "groups",
    "id": 10205,
    "attributes": {
      "group_type": "CUSTOM",
      "client_id": 1,
      "group_name": "New Group",
      "visitor_zip_matches": "[\"\"]",
      "visitor_state_matches": "[\"\"]",
      "visitor_email_matches": "[\"\"]",
      "visitor_country_matches": "[\"\"]",
      "visitor_company_matches": "[\"\"]",
      "visitor_current_url_matches": "[\"\"]",
      "visitor_referrer_url_matches": "[\"\"]",
      "visitor_city_matches": "[\"\"]",
      "visitor_phone_matches": "[\"312-555-9323\"]",
      "create_dt": "2018-06-23T13:32:45+00:00",
      "system_group": false,
      "updt_by": null,
      "trmnt_ind": false,
      "updt_dt": null,
      "create_by": 1
    }
  }
}
```

This endpoint creates a new group.

Groups allow you to visually separate your agents in the chat console
and they also facilitate routing.

### HTTP Request

`GET http://localhost:5000/api/v1/groups.json`

### Request Body

Parameter | Description | Required?
--------- | ----------- | -----------
group_name | The name of the new group | Yes
visitor_zip_matches | JSON stringified list of zip codes this group should match | No
visitor_state_matches | JSON stringified list of states (ISO Short Code) this group should match | No
visitor_email_matches | JSON stringified list of emails this group should match | No
visitor_country_matches | JSON stringified list of countries (ISO Short Code) this group should match | No
visitor_company_matches | JSON stringified list of company names this group should match | No
visitor_current_url_matches | JSON stringified list of current urls this group should match | No
visitor_referrer_url_matches | JSON stringified list of referrer urls this group should match | No
visitor_city_matches | JSON stringified list of city names this group should match | No

### Response Body

See List Groups








## Edit Group

```shell
curl -X "PATCH" "http://localhost:5000/api/v1/groups/10204.json" \
    -d '{"data": {"type": "groups", "attributes": {"group_name": "New Group", "visitor_phone_matches": "[\"555-555-9323\"]"}}}' \
    -H 'Content-Type: application/json' \
    -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhZ2VudF9pZCI6MSwiYWNjZXNzX3R5cGUiOiJhcGkiLCJhcGlfaWQiOiJ6ZDdyYmRuNjN2cWdiZHVma2ltdiJ9.jWNHTojO6E9myLuATQWg8mwaysKb37Q3PXeeqTOj9lg"
```

> Request Body Example

```json
{
    "data": {
        "type": "groups",
        "attributes": {
            "group_name": "New Group",
            "visitor_phone_matches": "[\"312-555-9323\"]"
        }
    }
}
```


> Response Body Example:

```json
{
  "data": {
    "type": "groups",
    "attributes": {
      "trmnt_ind": false,
      "visitor_city_matches": "[\"\"]",
      "create_dt": "2018-06-21T01:59:55+00:00",
      "system_group": false,
      "create_by": 1,
      "visitor_current_url_matches": "[\"\"]",
      "visitor_email_matches": "[\"\"]",
      "visitor_company_matches": "[\"\"]",
      "visitor_phone_matches": "[\"555-555-9323\"]",
      "client_id": 1,
      "group_type": "CUSTOM",
      "updt_by": 1,
      "visitor_referrer_url_matches": "[\"\"]",
      "visitor_zip_matches": "[\"\"]",
      "visitor_state_matches": "[\"\"]",
      "updt_dt": "2018-06-23T13:48:49+00:00",
      "group_name": "Sales",
      "visitor_country_matches": "[\"\"]"
    },
    "id": 10204
  }
}
```

This endpoint will update the group attributes.

It also returns the final updated group object.

### HTTP Request

`PATCH http://localhost:5000/api/v1/groups/<group_id>.json`

### Query Parameters

Parameter | Description | Required?
--------- | ----------- | -----------
group_id | The ID of the group you are updating.| Yes

### Request Body Parameters

Parameter | Description | Required?
--------- | ----------- | -----------
group_name | The name of the new group | Yes
visitor_zip_matches | JSON stringified list of zip codes this group should match | No
visitor_state_matches | JSON stringified list of states (ISO Short Code) this group should match | No
visitor_email_matches | JSON stringified list of emails this group should match | No
visitor_country_matches | JSON stringified list of countries (ISO Short Code) this group should match | No
visitor_company_matches | JSON stringified list of company names this group should match | No
visitor_current_url_matches | JSON stringified list of current urls this group should match | No
visitor_referrer_url_matches | JSON stringified list of referrer urls this group should match | No
visitor_city_matches | JSON stringified list of city names this group should match | No

### Response Body

See Get Group







## Remove Group

```shell
curl -X "DELETE" "http://localhost:5000/api/v1/groups/10204.json" \
    -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhZ2VudF9pZCI6MSwiYWNjZXNzX3R5cGUiOiJhcGkiLCJhcGlfaWQiOiJ6ZDdyYmRuNjN2cWdiZHVma2ltdiJ9.jWNHTojO6E9myLuATQWg8mwaysKb37Q3PXeeqTOj9lg"
```

> Response Body Example:

```json
{
    "success": "Deleted"
}
```

This endpoint will remove a group.

### HTTP Request

`DELETE http://localhost:5000/api/v1/groups/<group_id>.json`

### Query Parameters

Parameter | Description | Required?
--------- | ----------- | -----------
group_id | The ID of the group for the report. | Yes
















# Messages

## List Messages

```shell
curl -X "GET" "http://localhost:5000/api/v1/messages.json?visitor_username=tqxsbcndxs6q4fbm13dacg73kazefqx4pufr&include_admin=false" \
    -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhZ2VudF9pZCI6MSwiYWNjZXNzX3R5cGUiOiJhcGkiLCJhcGlfaWQiOiJ6ZDdyYmRuNjN2cWdiZHVma2ltdiJ9.jWNHTojO6E9myLuATQWg8mwaysKb37Q3PXeeqTOj9lg"
```

> The above command returns JSON structured like this:

```json
{
  "data": [{
    "type": "messages",
    "attributes": {
      "manual_user_id_2": null,
      "to_visitor_id": null,
      "final_manual_intent_id": null,
      "from_agent": null,
      "batch_intent_id": null,
      "is_admin": false,
      "is_interruption_blocked": false,
      "create_dt": "2018-06-22T01:31:27+00:00",
      "manual_user_id_5": null,
      "from_agent_id": null,
      "manual_intent_id_3": null,
      "manual_user_id_4": null,
      "manual_intent_id_2": null,
      "body": "Hi\n",
      "manual_user_id_3": null,
      "client_id": 1,
      "manual_intent_id_1": null,
      "manual_user_id_1": null,
      "batch_intent_probability": null,
      "manual_intent_id_5": null,
      "manual_intent_id_4": null,
      "chat_id": 1,
      "to_agent_id": 1,
      "from_visitor_id": 2
    },
    "id": 20
  }]
}
```

This endpoint lists all messages for a particular chat ID or visitor username.

### HTTP Request

Get group list:

`GET http://localhost:5000/api/v1/messages.json?visitor_username=<visitor_username>&chat_id=<chat_id>&include_admin=<include_admin>`

### Query Parameters

Parameter | Description | Required?
--------- | ----------- | -----------
visitor_username | Filter messages by visitor username | Either visitor_username or chat_id are required
chat_id | Filter messages by chat ID | Either visitor_username or chat_id are required
 include_admin | "true" or "false" | Yes


### Response Body

Parameter | Description
--------- | -----------
from_agent_id | Message sent from Agent ID.  Null if N/A
from_visitor_id | Message sent from Visitor ID.  Null if N/A
to_agent_id | Message sent to Agent ID.  Null if N/A
to_visitor_id | Message sent to Visitor ID.  Null if N/A
from_agent | Agent object.  See Get Agent
batch_intent_id | If message to bot, the resulting intent ID from AI.
is_admin | Is an admin message?
is_interruption_blocked | Was the message blocked due to interruption.
body | The body of the message.
batch_intent_probability | If message to bot, the probability of the intent.
chat_id | The chat associated to the message.
manual_intent_id_1 | Manually updated intent ID.
manual_intent_id_2 | Manually updated intent ID.
manual_intent_id_3 | Manually updated intent ID.
manual_intent_id_4 | Manually updated intent ID.
manual_intent_id_5 | Manually updated intent ID.
manual_user_id_1 | Agent ID of the manually updated intent.
manual_user_id_2 | Agent ID of the manually updated intent.
manual_user_id_3 | Agent ID of the manually updated intent.
manual_user_id_4 | Agent ID of the manually updated intent.
manual_user_id_5 | Agent ID of the manually updated intent.
final_manual_intent_id | The final updated intent.
create_dt | Date and time of message.
















# Tasks

## List Tasks

```shell
curl -X "GET" "http://localhost:5000/api/v1/q_tasks.json?after=0&task_type=operational&is_resolved=0" \
    -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhZ2VudF9pZCI6MSwiYWNjZXNzX3R5cGUiOiJhcGkiLCJhcGlfaWQiOiJ6ZDdyYmRuNjN2cWdiZHVma2ltdiJ9.jWNHTojO6E9myLuATQWg8mwaysKb37Q3PXeeqTOj9lg"
```

> The above command returns JSON structured like this:

```json
{
    "data": [
        {
            "type": "q_tasks",
            "id": 1,
            "attributes": {
                "node_name": "Schedule Service",
                "message": null,
                "message_id": null,
                "client_id": 1,
                "assigned_agent_id": 1,
                "is_complete": false,
                "updt_dt": null,
                "variables_": "{}",
                "intent_id": null,
                "create_by": 1,
                "updt_by": null,
                "create_dt": "2018-06-23T14:42:10+00:00",
                "task_type": "operational"
            }
        }
    ]
}
```

This endpoint lists either operational or machine learning tasks.

Tasks are a result of either an event occurring in a dialog ('operational' task) or
a when a message has a low intention probability from the AI assistant and needs clarification
from a human.

### HTTP Request

Get task list:

`GET http://localhost:5000/api/v1/q_tasks.json`

### Query Parameters

Parameter | Description | Required?
--------- | ----------- | -----------
after | Offset for chat results. Must be an integer | Yes
task_type | Filter for chats.  Either 'operational' or 'machine_learning' | Yes
is_resolved | Filter for chats.  Either '1' -> Yes or '0' -> No | Yes

### Response Body

Parameter | Description
--------- | -----------
task_type | Either 'operational' or 'machine_learning'.  See description.
node_name | Name of the node that kicked off the operational task.  Null for machine learning tasks.
message_id | ID of message that triggered the machine learning task. Null for operational tasks.
message | The message object if message_id is not Null.
assigned_agent_id | The Agent ID that the task is assigned to and is present in the Agents portal.
is_complete | Is the task complete?  Boolean.
updt_dt | The date and time the task was updated.
variables_ | The variables collected during the conversation for this task.  JSON searlized.  For operational tasks only.
intent_id | The intent ID that was selected manually by the agent.  For machine learning tasks only.
updt_by | The date and time the task was updated.
create_dt | The date and time the task was created.






## Update Machine Learning Task

```shell
curl -X "GET" "http://localhost:5000/api/v1/q_tasks/machine_learning/1/1.json" \
    -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhZ2VudF9pZCI6MSwiYWNjZXNzX3R5cGUiOiJhcGkiLCJhcGlfaWQiOiJ6ZDdyYmRuNjN2cWdiZHVma2ltdiJ9.jWNHTojO6E9myLuATQWg8mwaysKb37Q3PXeeqTOj9lg"
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "type": "q_tasks",
    "id": 1,
    "attributes": {
      "node_name": "Schedule Service",
      "message": {
          See Message Endpoint
      },
      "message_id": 1,
      "client_id": 1,
      "assigned_agent_id": 1,
      "is_complete": true,
      "updt_dt": "2018-06-23T14:59:51+00:00",
      "variables_": "{}",
      "intent_id": "1",
      "create_by": 1,
      "updt_by": 1,
      "create_dt": "2018-06-23T14:42:10+00:00",
      "task_type": "machine_learning"
    }
  }
}
```

This endpoint updates the intention of a machine learning task.  A machine learning task is created when a message has a low intention probability from the AI assistant and needs clarification.

The endpoint will also return the task object.

### HTTP Request

Update message intent:

`GET http://localhost:5000/api/v1/q_tasks/machine_learning/<task_id>/<intent_id>.json`

### Query Parameters

Parameter | Description | Required?
--------- | ----------- | -----------
task_id | ID of the task to update. | Yes
intent_id | ID of the intent to update. | Yes

### Response Body

See List Tasks






## Update Operational Task

```shell
curl -X "GET" "http://localhost:5000/api/v1/q_tasks/operational/2/1.json" \
    -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhZ2VudF9pZCI6MSwiYWNjZXNzX3R5cGUiOiJhcGkiLCJhcGlfaWQiOiJ6ZDdyYmRuNjN2cWdiZHVma2ltdiJ9.jWNHTojO6E9myLuATQWg8mwaysKb37Q3PXeeqTOj9lg"
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "type": "q_tasks",
    "id": 2,
    "attributes": {
      "variables_": "{}",
      "is_complete": true,
      "assigned_agent_id": 1,
      "message_id": null,
      "node_name": "Schedule Service",
      "task_type": "operational",
      "create_by": 1,
      "client_id": 1,
      "updt_by": 1,
      "intent_id": null,
      "message": null,
      "create_dt": "2018-06-23T14:42:10+00:00",
      "updt_dt": "2018-06-23T15:09:53+00:00"
    }
  }
}
```

This endpoint sets the resolved flag for operational tasks.

The endpoint will also return the task object.

### HTTP Request

Update message resolved flag for operational tasks (Task):

`GET http://localhost:5000/api/v1/q_tasks/operational/<task_id>/<is_complete>.json`

### Query Parameters

Parameter | Description | Required?
--------- | ----------- | -----------
task_id | ID of the task to update. | Yes
is_complete | Resolve or un-resolve the task.  Either '1' -> Yes or '0' -> No. | Yes

### Response Body

See List Tasks
















# Visitors

## List Visitors

```shell
curl -X "GET" "http://localhost:5000/api/v1/visitors.json" \
    -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhZ2VudF9pZCI6MSwiYWNjZXNzX3R5cGUiOiJhcGkiLCJhcGlfaWQiOiJ6ZDdyYmRuNjN2cWdiZHVma2ltdiJ9.jWNHTojO6E9myLuATQWg8mwaysKb37Q3PXeeqTOj9lg"
```

> The above command returns JSON structured like this:

```json
{
  "data": [{
    "type": "visitors",
    "id": 1,
    "attributes": {
      "name": "Test Visitor Name",
      "company_name": "New Co",
      "street_address_1": "123 Circle Dr",
      "street_address_2": null,
      "city": "Minneapolis",
      "state": "MN",
      "zip_code": "12345",
      "country": "US",
      "phone": "1231231234",
      "email": "example@testexample.com",
      "group_id": null,
      "xmpp_password": "gqseyr2ccspul4usdnb36xulf7mfvm2qhv0l",
      "xmpp_username": "geo1jqmurtnl3qjgwt0lsm4i6x4zsrtqzmj8",
      "client_id": 1,
      "create_by": 1,
      "create_dt": "2018-06-20T16:11:21+00:00",
      "updt_by": null,
      "updt_dt": null,
      "current_url": null,
      "referrer_url": null,
      "ip_address": "127.0.0.1"
    }
  }]
}
```

This endpoint lists all visitors.

Visitors are either website visitors or customers using text.

### HTTP Request

Get visitor list:

`GET http://localhost:5000/api/v1/visitors.json?name=<name>&email=<email>&company_name=<company_name>&city=<city>&state=<state>&zip_code=<zip_code>&ip_address=<ip_address>&visitor_id=<visitor_id>&has_phone_number=<has_phone_number>`

### Query Parameters
Parameter | Description | Required?
--------- | ----------- | -----------
name | Filter visitors by name | No
email | Filter visitors by email | No
phone | Filter visitors by phone | No
company_name | Filter visitors by company name | No
city | Filter visitors by city | No
state | Filter visitors by state | No
zip_code | Filter visitors by zip code | No
ip_address | Filter visitors by ip address | No
visitor_id | Filter visitors by visitor id | No
has_phone_number | Filter visitors by if a phone number exists | No

### Response Body

Parameter | Description
--------- | -----------
name | Name of visitor
company_name | Name of visitors company
street_address_1 | Street address of visitor
street_address_2 | Street address of visitor
city | City address of visitor
state | State address of visitor
zip_code | Zip code of visitor
country | Country code of visitor (ISO Short Code)
phone | Phone number of visitor
email | Email of visitor
group_id | Current group ID assigned to visitor (See groups endpoint)
xmpp_password | XMPP password for the visitor
xmpp_username | XMPP username for the visitor
create_dt | Date and time the visitor was first seen.
updt_by | Agent ID that last updated this visitor.
updt_dt | Date and time the visitor was last updated.
current_url | The last current url of the visitor
referrer_url | The last referrer url of the visitor.
ip_address | The IP address of the visitor if on web chat.







## Get Visitor By Username

```shell
curl -X "GET" "http://localhost:5000/api/v1/visitors.json?visitor_username=geo1jqmurtnl3qjgwt0lsm4i6x4zsrtqzmj8" \
    -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhZ2VudF9pZCI6MSwiYWNjZXNzX3R5cGUiOiJhcGkiLCJhcGlfaWQiOiJ6ZDdyYmRuNjN2cWdiZHVma2ltdiJ9.jWNHTojO6E9myLuATQWg8mwaysKb37Q3PXeeqTOj9lg"
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "type": "visitors",
    "attributes": {
      "create_dt": "2018-06-20T16:11:21+00:00",
      "ip_address": "127.0.0.1",
      "street_address_2": null,
      "create_by": 1,
      "updt_by": null,
      "email": "example@testexample.com",
      "company_name": "New Co",
      "referrer_url": null,
      "street_address_1": "123 Circle Dr",
      "zip_code": "12345",
      "name": "Test Visitor Name",
      "trmnt_ind": false,
      "state": "MN",
      "updt_dt": null,
      "client_id": 1,
      "group_id": null,
      "xmpp_username": "geo1jqmurtnl3qjgwt0lsm4i6x4zsrtqzmj8",
      "xmpp_password": "gqseyr2ccspul4usdnb36xulf7mfvm2qhv0l",
      "country": "US",
      "phone": "1231231234",
      "current_url": null,
      "city": "Minneapolis"
    },
    "id": 1
  }
}
```

This endpoint returns one visitor object based on visitor username.

A visitor is defined as a customer who is interacting via chat client or text message.

This endpoint will also make sure the visitor username is available in XMPP.

### HTTP Request

Get visitor:

`GET http://localhost:5000/api/v1/visitors.json?visitor_username=<visitor_username>`

### Query Parameters

Parameter | Description | Required?
--------- | ----------- | -----------
visitor_username | Visitor username. | Yes

### Response Body

See List Visitors






## Add Visitor

```shell
curl -X "POST" "http://localhost:5000/api/v1/visitors.json" \
    -d '{"data": {"type": "visitors", "attributes": {"company_name": "New Company"}}}' \
    -H 'Content-Type: application/json' \
    -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhZ2VudF9pZCI6MSwiYWNjZXNzX3R5cGUiOiJhcGkiLCJhcGlfaWQiOiJ6ZDdyYmRuNjN2cWdiZHVma2ltdiJ9.jWNHTojO6E9myLuATQWg8mwaysKb37Q3PXeeqTOj9lg"
```

> Request Body Example

```json
{
    "data": {
        "type": "visitors",
        "attributes": {
            "company_name": "New Company"
        }
    }
}
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "type": "visitors",
    "attributes": {
      "create_dt": "2018-06-23T20:44:54+00:00",
      "ip_address": null,
      "street_address_2": null,
      "create_by": 1,
      "updt_by": null,
      "email": null,
      "company_name": "New Company",
      "referrer_url": null,
      "street_address_1": null,
      "zip_code": null,
      "name": null,
      "trmnt_ind": false,
      "state": null,
      "updt_dt": null,
      "client_id": 1,
      "group_id": null,
      "xmpp_username": "7118d321-626d-4bcf-ad80-6b7efad27ec8",
      "xmpp_password": "dc2c9bca-52b0-4e53-92ba-35436db7132b",
      "country": null,
      "phone": null,
      "current_url": null,
      "city": null
    },
    "id": 6
  }
}
```

This endpoint creates a new visitor manually.

Typically new visitors are created when a customer visits a website with
the chat widget installed or texts a phone number that has been activated
with ChatrHub.

### HTTP Request

`POST http://localhost:5000/api/v1/visitors.json`

### Request Body

Parameter | Description | Required?
--------- | ----------- | -----------
company_name | Visitor company name | No
street_address_1 | Visitor street name 1 | No
street_address_2 | Visitor street name 2 | No
city | Visitor city | No
state | Visitor state (ISO Short Code) | No
zip_code | Visitor zip code | No
name | Visitor name | No
email | Visitor email | No
phone | Visitor phone (characters other than numbers will be striped) | No
country | Visitor country code (ISO short code) | No
group_id | Group ID visitor is associated to | No

### Response Body

See List Visitors








## Edit Visitor

```shell
curl -X "PATCH" "http://localhost:5000/api/v1/visitors/1.json" \
    -d '{"data": {"type": "visitors", "attributes": {"company_name": "Different Company name"}}}' \
    -H 'Content-Type: application/json' \
    -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhZ2VudF9pZCI6MSwiYWNjZXNzX3R5cGUiOiJhcGkiLCJhcGlfaWQiOiJ6ZDdyYmRuNjN2cWdiZHVma2ltdiJ9.jWNHTojO6E9myLuATQWg8mwaysKb37Q3PXeeqTOj9lg"
```

> Request Body Example

```json
{
    "data": {
        "type": "visitors",
        "attributes": {
            "company_name": "Different Company name"
        }
    }
}
```


> Response Body Example:

```json
{
  "data": {
    "type": "visitors",
    "attributes": {
      "create_dt": "2018-06-20T16:11:21+00:00",
      "ip_address": "127.0.0.1",
      "street_address_2": null,
      "create_by": 1,
      "updt_by": 1,
      "email": "example@testexample.com",
      "company_name": "Different Company name",
      "referrer_url": null,
      "street_address_1": "123 Circle Dr",
      "zip_code": "12345",
      "name": "Test Visitor Name",
      "trmnt_ind": false,
      "state": "MN",
      "updt_dt": "2018-06-23T21:12:22+00:00",
      "client_id": 1,
      "group_id": null,
      "xmpp_username": "geo1jqmurtnl3qjgwt0lsm4i6x4zsrtqzmj8",
      "xmpp_password": "gqseyr2ccspul4usdnb36xulf7mfvm2qhv0l",
      "country": "US",
      "phone": "1231231234",
      "current_url": null,
      "city": "Minneapolis"
    },
    "id": 1
  }
}
```

This endpoint will update visitor attributes.

### HTTP Request

`PATCH http://localhost:5000/api/v1/visitors/<visitor_id>.json`

### Query Parameters

Parameter | Description
--------- | -----------
visitor_id | The ID of the visitor you are updating. (Required)

### Request Body Parameters

See Add Visitor

### Response Body

See Get Visitor
