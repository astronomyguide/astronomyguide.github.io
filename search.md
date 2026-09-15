---
layout: page
title: 검색
permalink: /search/
---

<div class="container" style="padding-top: 40px; max-width: 700px; margin: 0 auto;">
  <h2>찾으시는 게시물의 제목을 입력해 주세요</h2>
  
  <!-- 검색 입력창 -->
  <div style="margin-top: 20px;">
    <input type="text" id="search-input" placeholder="검색어를 입력하세요..." style="width: 100%; padding: 12px; font-size: 16px; border: 1px solid #ccc; border-radius: 4px;">
  </div>

  <!-- 검색 결과 리스트 출력 영역 -->
  <ul id="results-container" style="list-style: none; padding-left: 0; margin-top: 20px;"></ul>
</div>

<br>
<hr class="border-hr-dashed">


<div>
{% for category in site.categories %}
  <div class="archive-group">
    {% capture category_name %}{{ category | first }}{% endcapture %}
    <div id="#{{ category_name | slugize }}"></div>
    <p></p>
    <h3 class="category-head">{{ category_name }}</h3>
    <a name="{{ category_name | slugize }}"></a>
    {% for post in site.categories[category_name] %}
    <article class="archive-item">
      <h4><a href="{{ site.baseurl }}{{ post.url }}">{{post.title}}</a></h4>
    </article>
    {% endfor %}
  </div>
{% endfor %}
</div>



<!-- Simple Jekyll Search 라이브러리 스크립트 -->
<script src="https://unpkg.com/simple-jekyll-search/dest/simple-jekyll-search.min.js"></script>
<script>
  SimpleJekyllSearch({
    searchInput: document.getElementById('search-input'),
    resultsContainer: document.getElementById('results-container'),
    json: '{{ "/search.json" | relative_url }}',
    searchResultTemplate: '<li style="margin-bottom: 15px;"><a href="{url}" style="font-size: 18px; font-weight: 600; color: #0072ce;">{title}</a><div style="font-size: 13px; color: #666;">{date}</div></li>',
    noResultsText: '<li style="color: #888;">검색 결과가 없습니다.</li>',
    limit: 10
  });
</script>