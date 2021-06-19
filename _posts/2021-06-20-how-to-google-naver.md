---
date: 2021-06-20 12:35:40
layout: post
title: Jekyll, Github blog를 검색엔진에 노출시키기!
subtitle: google,naver에 내 사이트 검색되게 하기! 
description:  만들어진 Github site를 google,naver 검색엔진에 노출시키는 방법을 알아보자. 해당 내용은 Jekyll 기준으로 작성되어있다.
image: http://drive.google.com/uc?export=view&id=1nUQa6xi612oAHmnJ4_DDOocos5NlEKyE
optimized_image: http://drive.google.com/uc?export=view&id=1nUQa6xi612oAHmnJ4_DDOocos5NlEKyE
category: coding
tags:
  - coding
  - blog
  - jeyll
author: Rudezoo
---


### Github로 만든 내 사이트를 검색엔진에 노출시키기
---
나는 주로 정보를 구글링을 통해 검색한다. 이때, 유용한 정보가 담긴 블로그들이 검색되었고 이중에 깃허브 사이트또한 포함되어있었다. 그렇다면, 내가 만든 블로그도 검색하면 노출되면 좋겠다 싶었다.  

처음에 **Jekyll**를 이용해 블로그를 만들고 나서는 당연히 바로 검색엔진을 통해 노출되지 않는다. 그래서 내 블로그를 구글과 네이버에 노출시키는 법을 검색했고, 직접 블로그에 적용했다.  

내가 사용한 방법은 아래와 같다. 이 블로그에는 Jekyll를 이용해 구축했으므로 이를 기준으로 설명하겠다.  

<br/>


<br/>

#### 1. Google

구글은 [Google Search Console](https://search.google.com/search-console/welcome)에서 특정 파일을 제출해야한다. 구글뿐만 아닌 네이버도 <code>sitemap.xml</code> 파일을 필요로 한다.  

그럼 sitemap 파일은 어떻게 작성하는가? 이 블로그에 경우는 템플릿 제작자가 sitemap 파일을 미리 포함시켜두었다. 만약 없다면 <code>/root</code>경로에 <code>sitemap.xml</code>을 만들고 코드를 삽입해주면 된다.

 기본적인 코드는 아래와 같다. <U>이때 설정파일에서 사이트 url을 설정을 안해주면 site.url 부분이 나와있지 않아 등록시에 url오류가 날 수 있다. (본인은 이미 경혐했다..) 그러므로 <code>/_config.yml</code>에서 base url을 적는 부분이 있다면 채워놓도록 하자.</U>

```html
---
layout: null
---
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  {% for post in site.posts %}
    <url>
      <loc>{{ site.url }}{{ post.url }}</loc>
      {% if post.lastmod == null %}
        <lastmod>{{ post.date | date_to_xmlschema }}</lastmod>
      {% else %}
        <lastmod>{{ post.lastmod | date_to_xmlschema }}</lastmod>
      {% endif %}

      {% if post.sitemap.changefreq == null %}
        <changefreq>weekly</changefreq>
      {% else %}
        <changefreq>{{ post.sitemap.changefreq }}</changefreq>
      {% endif %}

      {% if post.sitemap.priority == null %}
          <priority>0.5</priority>
      {% else %}
        <priority>{{ post.sitemap.priority }}</priority>
      {% endif %}

    </url>
  {% endfor %}
</urlset>
```

<br/>
##### 그럼 이제 사이트를 등록시켜보자.

구글은 [Google Search Console](https://search.google.com/search-console/welcome)에서 등록을 실시한다.

1. 처음 사이트에 접속하면 아래와 같은 페이지가 보인다. 빨간색으로 표신된 곳에 페이지 주소를 입력한다.
![g1](http://drive.google.com/uc?export=view&id=14vZdih2WItlNL7EoKPEDibKHL96hYPd7)

2. 처음에 등록을 하면, 해당 사이트를 인증하기 위한 절차가 존재한다. 나는 블로그 파일에 html파일을 올리는 것을 선택했고, <code>/root</code>에 구글에서 제공하는 **html을 올리고 github에 push**하면 된다.
   
3. Search Console로 이동 후에 왼쪽 메뉴에 보면 **Sitemaps**라고 메뉴가 있고, 이를 클릭한다.
   
4. 그러면 아래와 같은 화면이 보이고, **사이트맵 url을 입력한후 제출한다.**  
이때 상태에 어떤 에러가 나지 않고 성공으로 뜨면 된다. 만약 에러가 났다면 해당 부분을 클릭하면 그 사유가 나온다. (ex.url오류가 난다면 url부분에 오류가 났다고 지적해준다.)
![google](http://drive.google.com/uc?export=view&id=1fe2EC6ZAWRSeaaFTYduf6oQ5QWFDsRaQ)

<br/>

<!-- ![sitemap](http://drive.google.com/uc?export=view&id=1LkNPBd8RWkmThytlY0BsH50dxHLM87PD) -->

#### 2. Naver

naver의 경우 siteam.xml 뿐만 아닌 feed.xml이 필요하다. 해당 파일은 [네이버 웹마스터 도구](https://searchadvisor.naver.com/)에서 등록한다.
위의 방식과 같이 미리 <code>feed.xml</code>파일이 생성 되어 있지 않다면 <code>/root</code>경로에 <code>feed.xml</code>을 만들고 코드를 삽입해주면 된다. 해당 파일은 확인 시에 브라우저 확장 프로그램 중 RSS를 확인 하는 프로그램을 통해 확인 가능하다.


 기본적인 코드는 아래와 같다.
 
```html
---
layout: null
---
<?xml version="1.0" encoding="UTF-8"?>
<rss version="2.0" xmlns:atom="http://www.w3.org/2005/Atom">
  <channel>
    <title>{{ site.title | xml_escape }}</title>
    <description>{{ site.description | xml_escape }}</description>
    <link>{{ site.url }}{{ site.baseurl }}/</link>
    <atom:link href="{{ "/feed.xml" | prepend: site.baseurl | prepend: site.url }}" rel="self" type="application/rss+xml"/>
    <pubDate>{{ site.time | date_to_rfc822 }}</pubDate>
    <lastBuildDate>{{ site.time | date_to_rfc822 }}</lastBuildDate>
    <generator>Jekyll v{{ jekyll.version }}</generator>
    {% for post in site.posts limit:30 %}
      <item>
        <title>{{ post.title | xml_escape }}</title>
        <description>{{ post.content | xml_escape }}</description>
        <pubDate>{{ post.date | date_to_rfc822 }}</pubDate>
        <link>{{ post.url | prepend: site.baseurl | prepend: site.url }}</link>
        <guid isPermaLink="true">{{ post.url | prepend: site.baseurl | prepend: site.url }}</guid>
        {% for tag in post.tags %}
        <category>{{ tag | xml_escape }}</category>
        {% endfor %}
        {% for cat in post.categories %}
        <category>{{ cat | xml_escape }}</category>
        {% endfor %}
      </item>
    {% endfor %}
  </channel>
</rss>
```

<br/>

##### 그럼 이제 사이트를 등록시켜보자.

네이버는  [네이버 웹마스터 도구](https://searchadvisor.naver.com/)에서 등록을 실시한다.

1. 위의 링크에 접속하면 아래와 같은 화면이 보인다. 여기서 웹마스터 도구를 클릭한다.
![n1](http://drive.google.com/uc?export=view&id=1oR5gQ6pyjjlt31QfDisSsfuDJRvdX_hW)
2. 클릭하면 구글때와 같이 인증하는 방법이 있고, 구글 처럼 html을 파일을 올리면된다.
3. 인증이 되면 아래와 같은 화면이 나온다. 메뉴의 요청을 선택한다.
![n3](http://drive.google.com/uc?export=view&id=1A8LjV7ACP4KeiwsAcoE4bZBb7PSS7vUQ)
4. 해당 메뉴에서 사이트맵과 RSS를 제출한다.
![naver](http://drive.google.com/uc?export=view&id=1iJRhTsJNrY_S3zFumn6E3qxGRTcoywuW)
5. 추가적으로 검증 메뉴에서 <code>robots.txt</code>를 검증 후, 제출후 마무리한다.
<br/>

#### 이때, robots.txt 란?
처음 검색했을때 <code>sitemap.xml</code>파일과 <code>feed.xml</code>파일만 이용하는 줄 알았지만, 추가적으로 robots.txt파일도 있음을 파악했다.  
해당 파일에 <code>sitemap.xml</code>파일과 <code>feed.xml</code>파일의 위치를 등록해두면 검색엔진의 크롤러들이 크롤링시에 더욱 효과적이라고 한다! 위의 방식과 같이 미리 <code>robots.txt</code>파일이 생성 되어 있지 않다면 <code>/root</code>경로에 <code>robots.txt</code>을 만들고 코드를 삽입해주면 된다. 그리고 github에 push후에 위의 사이트에서 등록해주면 된다.


기본적인 코드는 아래와 같다. 

```
User-agent: *
Allow: /

Sitemap: /*사이트 주소*/ /sitemap.xml
```

```
/*사이트 주소*/ 부분을 본인 사이트 주소로 교체해주면 된다.
```

<br/>


## 마무리

이번 게시물은 어떻게 구글과 네이버에 본인이 만든 블로그를 노출 시킬 수 있는지에 대해 알아보았다. 사실 첫 정보 공유 글이였다. 잘 설명되었는지 모르겠지만 기본적으로 <code>sitemap.xml</code>파일과 <code>feed.xml</code>만 만들고 제출만 하면되서 비교적 쉬운 과정이였다! 해당 파일의 기본 양식도 왠만하면 제공되기 때문에 큰 어려움은 없을거라고 생각된다.

유의할 점은 템플릿마다 구조가 비슷하지만, 살짝 다른 경우가 있어 주의해야한다. 각 템플릿마다 <code>_config.yml</code>의 양식이 다를 수 있기에 꼼꼼히 보고 진행해주면 될 것같다.




