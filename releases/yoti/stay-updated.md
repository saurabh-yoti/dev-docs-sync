---
type: page
title: Stay updated
listed: true
slug: stay-updated
description: 
index_title: Stay updated
hidden: 
keywords: 
tags: 
---

To stay informed on our product's uptime and operational status please head over to the following link:

- [https://status.yoti.com/ ](https://status.yoti.com/)

All past incidents will be listed on the webpage. The statuses are explained in the below table:

{% table %}
| Name | Description | 
| ---- | ---- | 
| Operational | The component is working. | 
| Performance Issues | The component is experiencing some slowness. | 
| Partial outage | The component may not be working for everybody. This could be a geographical issue for example. | 
| Major outage | The component is not working for anybody. | 
{% /table %}

## Notifications

In order to get real time notifications you will need to generate a GET method to retrieve information from the Yoti Status API using this URL:  [https://status.yoti.com/api/v1/components](https://status.yoti.com/api/v1/components)

Please take note of the product name and status name.

{% code %}
{% tab language="http" %}
{
meta: {
pagination: {
total: 6,
count: 6,
per_page: 20,
current_page: 1,
total_pages: 1,
links: {
next_page: null,
previous_page: null
}
}
},
data: [
{
id: 4,
name: "Yoti Hub",
description: "",
link: "",
status: 1,
order: 0,
group_id: 1,
created_at: "2020-02-27 13:23:46",
updated_at: "2020-04-27 08:25:22",
deleted_at: null,
enabled: true,
meta: null,
status_name: "Operational",
tags: [ ]
},
{
id: 1,
name: "Yoti Website",
description: "",
link: "",
status: 1,
order: 0,
group_id: 1,
created_at: "2020-02-27 13:22:51",
updated_at: "2020-05-11 10:49:02",
deleted_at: null,
enabled: true,
meta: null,
status_name: "Operational",
tags: [ ]
},
{
id: 5,
name: "Yoti Sign",
description: "",
link: "",
status: 1,
order: 0,
group_id: 1,
created_at: "2020-02-27 13:24:10",
updated_at: "2020-02-27 13:29:13",
deleted_at: null,
enabled: true,
meta: null,
status_name: "Operational",
tags: [ ]
},
{
id: 3,
name: "Yoti App",
description: "",
link: "",
status: 1,
order: 0,
group_id: 1,
created_at: "2020-02-27 13:23:18",
updated_at: "2020-05-28 16:55:31",
deleted_at: null,
enabled: true,
meta: null,
status_name: "Operational",
tags: [ ]
},
{
id: 6,
name: "Yoti Doc Scan",
description: "",
link: "",
status: 1,
order: 0,
group_id: 1,
created_at: "2020-02-27 13:24:44",
updated_at: "2020-02-28 11:49:35",
deleted_at: null,
enabled: true,
meta: null,
status_name: "Operational",
tags: [ ]
},
{
id: 2,
name: "Yoti Age Scan",
description: "",
link: "",
status: 1,
order: 0,
group_id: 1,
created_at: "2020-02-27 13:23:05",
updated_at: "2020-03-27 20:01:03",
deleted_at: null,
enabled: true,
meta: null,
status_name: "Operational",
tags: [ ]
}
]
}
{% /tab %}
{% /code %}