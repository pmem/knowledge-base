---
layout: page
title: Development Articles 
pagination: 
  enabled: true
  collection: development
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

{% for development in paginator.posts %}

       <tr>
            <td>
		<a href="{{ development.url | prepend: site.baseurl }}"> 
		    {{ development.title }} {% if development.doc %}  ( {{ development.docid}} ) {% endif %} 
		</a>
	    </td>
            <td>{{ development.date | date_to_string }}</td>
        </tr>

{% endfor %}

    </tbody>
</table>

{% include paginate-collection.html %}
