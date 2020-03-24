---
layout: page
title: Videos 
pagination: 
  enabled: true
  collection: videos
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

{% for videos in paginator.posts %}

       <tr>
            <td>
		<a href="{{ videos.url | prepend: site.baseurl }}"> 
		    {{ videos.title }} {% if alert.doc %} ( {{ videos.docid}} ) {% endif %}
		</a>
	    </td>
            <td>{{ videos.date | date_to_string }}</td>
        </tr>

{% endfor %}

    </tbody>
</table>

{% include paginate-collection.html %}
