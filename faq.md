---
layout: page
title: Frequently Asked Questions 
pagination: 
  enabled: true
  collection: faq
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

{% for faq in paginator.posts %}

       <tr>
            <td>
		<a href="{{ faq.url | prepend: site.baseurl }}"> 
		    {{ faq.title }} {% if faq.doc %} ( {{ faq.docid}} ) {% endif %}
		</a>
	    </td>
            <td>{{ faq.date | date_to_string }}</td>
        </tr>

{% endfor %}

    </tbody>
</table>

{% include paginate-collection.html %}
