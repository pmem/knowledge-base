---
layout: page
title: Troubleshooting Guides 
pagination: 
  enabled: true
  collection: troubleshoot
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

{% for troubleshoot in paginator.posts %}

       <tr>
            <td>
		<a href="{{ troubleshoot.url | prepend: site.baseurl }}"> 
		    {{ troubleshoot.title }} {% if alert.doc %} ( {{ troubleshoot.docid}} ) {% endif %}
		</a>
	    </td>
            <td>{{ troubleshoot.date | date_to_string }}</td>
        </tr>

{% endfor %}

    </tbody>
</table>

{% include paginate-collection.html %}
