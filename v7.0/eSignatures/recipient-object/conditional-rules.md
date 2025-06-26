---
type: page
title: Conditional rules
listed: true
slug: conditional-rules
description: 
index_title: Conditional rules
hidden: 
keywords: 
tags: 
---

Conditional logic allows you to specify that certain conditions must be met, before triggering an action. The available actions are show or hide, the trigger for these actions is defined within rules.

{% code %}
{% tab language="json" %}
{
    "rules": [
        {
            "action": "show",
            "conditions": [
                {
                    "trigger_tag_name": "sign-here",
                    "criteria": "has_value"
                }
            ],
            "affected_tag_names": [
                "signee-name"
            ]
        }
    ]
}
{% /tab %}
{% /code %}

{% table widths="241" %}
| Parameter | Description | 
| ---- | ---- | 
| `action` | The action to take when a condition is triggered\n\n\n\n- `show`\n- `hide` | 
| `conditions` | A list of condition objects that represent the rule’s conditions that have to be met, so that the action can be applied to the affected tags or tag groups.\n\n\n\n`trigger_tag_name` name of a tag that belongs to that recipient\n\n\n\n- a tag name matching the `trigger_tag_name` specified must be present in the recipient's list of tags\n- has to be unique for the rule, i.e. two conditions within a rule cannot have the same trigger tags\n- the trigger tag cannot be of type `date_signed_field`\n\n\n`criteria` the criteria of the condition which causes the specified action to be activated\n\n\n\n- can be one of the following: `has_value` or `no_value` | 
| `affected_tag_names` | A list of tag names which are affected by the rule\n\n\n\n- specified tag names must be present in the recipient's list of tags\n- names in this array cannot appear more than once for a given recipient\n- a name cannot also be listed as a trigger tag in the conditions for this rule i.e. a tag cannot affect its own behaviour | 
| `affected_tag_group_names` | A list of tag names which are affected by the rule\n\n\n\n- specified tag names must be present in the recipient's list of tags\n- names in this array cannot appear more than once for a given recipient\n- a name cannot also be listed as a trigger tag in the conditions for this rule i.e. a tag cannot affect its own behaviour | 
{% /table %}