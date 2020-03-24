---
layout: page
title: Getting Started 
pagination: 
  enabled: true
  collection: getting_started
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

{% for getting_started in paginator.posts %}

       <tr>
            <td>
		<a href="{{ getting_started.url | prepend: site.baseurl }}"> 
		    {{ getting_started.title }} {% if alert.doc %} ( {{ getting_started.docid}} ) {% endif %}
		</a>
	    </td>
            <td>{{ getting_started.date | date_to_string }}</td>
        </tr>

{% endfor %}

    </tbody>
</table>

{% include paginate-collection.html %}
