---
layout: page
title: Problem and Issue Resolution
pagination: 
  enabled: true
  collection: problem
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

{% for problem in paginator.posts %}

       <tr>
            <td>
		<a href="{{ problem.url | prepend: site.baseurl }}"> 
		    {{ problem.title }} {% if problem.doc %} ( {{ problem.docid}} ) {% endif %}
		</a>
	    </td>
            <td>{{ problem.date | date_to_string }}</td>
        </tr>

{% endfor %}

    </tbody>
</table>

{% include paginate-collection.html %}
