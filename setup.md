---
layout: page
title: Setup and Configuration Guides 
pagination: 
  enabled: true
  collection: setup
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

{% for setup in paginator.posts %}

       <tr>
            <td>
		<a href="{{ setup.url | prepend: site.baseurl }}"> 
		    {{ setup.title }} {% if setup.doc %} ( {{ setup.docid}} ) {% endif %}
		</a>
	    </td>
            <td>{{ setup.date | date_to_string }}</td>
        </tr>

{% endfor %}

    </tbody>
</table>

{% include paginate-collection.html %}
