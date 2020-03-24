---
layout: page
title: How To 
pagination: 
  enabled: true
  collection: howto
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

{% for howto in paginator.posts %}

       <tr>
            <td>
		<a href="{{ howto.url | prepend: site.baseurl }}"> 
		    {{ howto.title }} {% if howto.doc %} ( {{ howto.docid}} ) {% endif %}
		</a>
	    </td>
            <td>{{ howto.date | date_to_string }}</td>
        </tr>

{% endfor %}

    </tbody>
</table>

{% include paginate-collection.html %}
