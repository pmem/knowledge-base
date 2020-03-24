---
layout: page
title: Product Alerts 
pagination: 
  enabled: true
  collection: alert
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

{% for alert in paginator.posts %}

       <tr>
            <td>
		<a href="{{ alert.url | prepend: site.baseurl }}"> 
		    {{ alert.title }} {% if alert.doc %} ( {{ alert.docid}} ) {% endif %} 
		</a>
	    </td>
            <td>{{ alert.date | date_to_string }}</td>
        </tr>

{% endfor %}

    </tbody>
</table>

{% include paginate-collection.html %}
