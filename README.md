# Pagination
基于Python的分页类

## 分页组件应用：
### 1. 在视图函数中
```python
queryset = models.Issues.objects.filter(project_id=project_id)
page_object = Pagination(
    current_page=request.GET.get('page'),
    all_count=queryset.count(),
    base_url=request.path_info,
    query_params=request.GET
)
issues_object_list = queryset[page_object.start:page_object.end]

context = {
    'issues_object_list': issues_object_list,
    'page_html': page_object.page_html()
}
return render(request, 'issues.html', context)
```

### 2. 前端
```html
{% for item in issues_object_list %}
    {{item.xxx}}
{% endfor %}

 <nav aria-label="...">
    <ul class="pagination" style="margin-top: 0;">
        {{ page_html|safe }}
    </ul>
</nav>
```


