---
layout: page
title: Persistent Memory Enabled Applications
pagination: 
  enabled: true
  collection: apps
  trail: 
    before: 5
    after: 5
---

<table class="uk-table uk-table-responsive">
    <thead>
        <tr>
            <th>Document Title</th>
            <th>Date</th>
        </tr>
    </thead>
    <tbody>

{% for apps in paginator.posts %}

       <tr>
            <td>
		<a href="{{ apps.url | prepend: site.baseurl }}"> 
		    {{ apps.title }} {% if alert.doc %} ( {{ apps.docid}} ) {% endif %}
		</a>
	    </td>
            <td>{{ apps.date | date_to_string }}</td>
        </tr>

{% endfor %}

    </tbody>
</table>

{% include paginate-collection.html %}
