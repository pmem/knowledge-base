---
layout: page
title: Announcements 
pagination: 
  enabled: true
  collection: announcement
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

{% for announcement in paginator.posts %}

       <tr>
            <td>
		<a href="{{ announcement.url | prepend: site.baseurl }}"> 
		    {{ announcement.title }} {% if announcement.doc %} ( {{ announcement.docid}} ) {% endif %} 
		</a>
	    </td>
            <td>{{ announcement.date | date_to_string }}</td>
        </tr>

{% endfor %}

    </tbody>
</table>

{% include paginate-collection.html %}
