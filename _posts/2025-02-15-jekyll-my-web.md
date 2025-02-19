---
title: "Build a website using Jekyll"
categories:
  - Blog
tags:
  - Jekyll
---

<div class="notice--info">
    <h4>💡使用工具</h4>
    <p> </p>
    <p>Ruby: 一種程式語言</p>
    <p>Jekyll: 利用 Ruby 撰寫的靜態網站產生器</p>
    <p>gem: Ruby 的套件管理工具，類似於 Python 的 pip</p>
    <p>Minimal Mistake: Jekyll 中使用率最高的極簡風主題 (Github star 12.7k)</p>
    <p>Github Page: GitHub 所提供的網頁託管服務</p>
</div>

# Introduction

## What is Jekyll?

Jekyll 是一個**靜態網站產生器**（Static Site Generator），用 Ruby 語言編寫，相似的架站工具有 Hugo, Hexo 

使用者可使用 Markdown 語法寫文章，Jekyll 會將 Markdown 轉換成靜態 HTML，適合用來建個人網站

## Why we use Jekyll？

1. **簡單**：使用 Markdown 撰寫文章，無需建立 backend server
2. **可部署在 GitHub Pages**：Jekyll 是 GitHub Pages 的官方支援工具，免費託管網站
3. **擴充性強**：支援 plugin 與 themes，根據需求調整功能與外觀

---

# Install

### STEP1. Ruby

因為 Jekyll 是用 Ruby 編寫，使用 Jekyll 或其他 Ruby 工具（如 Rails、Bundler）前，必須先安裝 Ruby

```bash
brew install ruby
ruby --version # 檢查版本
echo 'export PATH="/opt/homebrew/opt/ruby/bin:$PATH"' >> ~/.zshrc # 將 Ruby 添加到 PATH
source ~/.zshrc
```

### STEP2. Gem

**Gem**

`gem install [packageName]`

- Ruby 的套件管理工具，類似於 Python 的 pip 套件或 JavaScript 的 npm 模組，程式開發經常要載入不同開發者提供的工具，透過套件管理工具可以增加下載的便利性
- 網頁框架（Rails）、靜態網站產生器（Jekyll）也是 Gem 的一種，裝 ruby 時會一起安裝

**Bundler**：管理 Gem 版本，確保所有人使用相同的版本

```bash
gem --version # 檢查版本
gem install jekyll bundler # 安裝 gem: jekyll & bundler
```

github-pages(Gem)

**用途**：啟用 Jekyll 的套件，讓你在本地模擬 GitHub Pages 的環境，確保本地預覽、測試、上線後的表現一致

```bash
gem install github-pages
```

---

# **Build**

## **Option1. 建立新的 Jekyll 網站**

(一) 轉換目錄到你要存放此專案的資料夾，建立一個新的 jekyll site

```bash
# 1. Create a new Jekyll site at ./myblog
jekyll new myblog
# 2. Change into your new directory
cd myblog
# 3. Build the site and make it available on a local server
bundle exec jekyll serve
```

(二) Browse to [http://localhost:4000](http://localhost:4000/)

用瀏覽器打開[localhost:4000](https://localhost:4000/)就可以看到你的網站現在的外觀

## Option2. 使用現成的 **Jekyll 網站**

快速搭建起來的部落格外觀簡陋，可以使用現成版型

(一) git clone 現成 code 

```bash
git clone https://github.com/mmistakes/mm-github-pages-starter.git
```

(二) 修改現有的 Gemfile

使用 homebrew 安裝的最新版的 ruby 預設不含 faraday-retry、mutex_m，我們需手動新增

```
source "https://rubygems.org"

gem "github-pages", group: :jekyll_plugins

gem "tzinfo-data"
gem "wdm", "~> 0.1.0" if Gem.win_platform?

gem "faraday-retry"
gem "mutex_m"

# If you have any plugins, put them here!
group :jekyll_plugins do
  gem "jekyll-paginate"
  gem "jekyll-sitemap"
  gem "jekyll-gist"
  gem "jekyll-feed"
  gem "jemoji"
  gem "jekyll-include-cache"
  gem "jekyll-algolia"
end

```

(三) 轉換目錄到存放此專案的資料夾

根據你專案目錄中的 Gemfile 來安裝所有指定的 Ruby 套件（Gems）

```bash
bundle install
```

啟動伺服器，在 local 測試 → 在瀏覽器打開 [http://127.0.0.1:4000](http://127.0.0.1:4000/) (預設)

```bash
bundle exec jekyll serve
```

---

# File **Structure**

**專案目錄**

**用途**：網站的原始來源檔案

```bash
├── Gemfile
├── Gemfile.lock
├── README.md
├── _config.yml # 基礎設定檔
├── _data
│   └── navigation.yml
├── _pages
│   ├── 404.md
│   ├── about.md
│   ├── category-archive.md
│   ├── tag-archive.md
│   └── year-archive.md
├── _posts
│   ├── 2010-01-07-post-modified.md
│   ├── 2010-01-07-post-standard.md
│   ├── 2010-01-08-post-chat.md
│   ├── 2010-02-05-post-notice.md
│   ├── 2010-02-05-post-quote.md
│   ├── 2010-03-07-post-link.md
│   └── 2019-04-18-welcome-to-jekyll.md
├── assets
│   └── images
│       └── bio-photo.jpg
└── index.html
```

## _site

**用途**：靜態檔案，呈現給瀏覽器的網站內容

bundle exec jekyll serve 後，Jekyll 會將以上來源檔案生成一包『_site 資料夾』，此為最終網站輸出結果

1. 讀取 `_config.yml` 與其他來源檔案 (ex. `_posts`、`_pages`)
2. 利用 Liquid 模板語言處理並組合檔案，生成最終的 HTML、CSS、JavaScript，並輸出到預設資料夾 _site
3. 訪問 http://localhost:4000 時，看到的就是 _site 資料夾裡的內容
- 新增 _site 資料夾
    
    ```bash
    .
    ├── Gemfile
    ├── Gemfile.lock
    ├── README.md
    ├── _config.yml
    ├── _data
    │   └── navigation.yml
    ├── _pages
    │   ├── 404.md
    │   ├── about.md
    │   ├── category-archive.md
    │   ├── tag-archive.md
    │   └── year-archive.md
    ├── _posts
    │   ├── 2010-01-07-post-modified.md
    │   ├── 2010-01-07-post-standard.md
    │   ├── 2010-01-08-post-chat.md
    │   ├── 2010-02-05-post-notice.md
    │   ├── 2010-02-05-post-quote.md
    │   ├── 2010-03-07-post-link.md
    │   └── 2019-04-18-welcome-to-jekyll.md
    ├── _site
    │   ├── 404.html
    │   ├── README.md
    │   ├── about
    │   │   └── index.html
    │   ├── assets
    │   │   ├── css
    │   │   │   └── main.css
    │   │   ├── images
    │   │   │   └── bio-photo.jpg
    │   │   └── js
    │   │       ├── _main.js
    │   │       ├── lunr
    │   │       │   ├── lunr-en.js
    │   │       │   ├── lunr-gr.js
    │   │       │   ├── lunr-store.js
    │   │       │   ├── lunr.js
    │   │       │   └── lunr.min.js
    │   │       ├── main.min.js
    │   │       ├── main.min.js.map
    │   │       ├── plugins
    │   │       │   ├── gumshoe.js
    │   │       │   ├── jquery.ba-throttle-debounce.js
    │   │       │   ├── jquery.fitvids.js
    │   │       │   ├── jquery.greedy-navigation.js
    │   │       │   ├── jquery.magnific-popup.js
    │   │       │   └── smooth-scroll.js
    │   │       └── vendor
    │   │           └── jquery
    │   │               └── jquery-3.6.0.js
    │   ├── blog
    │   │   ├── post-chat
    │   │   │   └── index.html
    │   │   ├── post-link
    │   │   │   └── index.html
    │   │   ├── post-modified
    │   │   │   └── index.html
    │   │   ├── post-notice
    │   │   │   └── index.html
    │   │   ├── post-quote
    │   │   │   └── index.html
    │   │   ├── post-standard
    │   │   │   └── index.html
    │   │   └── welcome-to-jekyll
    │   │       └── index.html
    │   ├── categories
    │   │   └── index.html
    │   ├── feed.xml
    │   ├── index.html
    │   ├── page2
    │   │   └── index.html
    │   ├── posts
    │   │   └── index.html
    │   ├── robots.txt
    │   ├── sitemap.xml
    │   └── tags
    │       └── index.html
    ├── assets
    │   └── images
    │       ├── bio-photo-comic.jpg
    │       ├── bio-photo.jpg
    │       └── woman.png
    └── index.html
    ```
    

**優點**

- **維護方便**
    - 保留原始來源檔案，輕鬆修改
    - _site 資料夾則只是一個生成的輸出，不需要手動編輯，也不需上傳 Github
- **部署目標**：最終部署到 GitHub Pages 上的就是 _site 資料夾中的內容，不包含原始 Markdown 或檔案

## _config.yml

定義網站的基本資料、layout、外觀、插件、post/page 的預設值

### (1) Site settings

**用途**：向訪客介紹關於自己，ex. 網站`title` , `description`, 連接其他社群 (twitter, github)

- 查看 HTML 文件，可透過 {{ site.title }}、{{ site.email }} 存取
- **可建立任何自訂 variable，在模板中透過 {{ site.myvariable }} 訪問**

**參數**

- `title`：定義網站 `title` (網站標題)
- `description`：定義網站描述，協助 SEO(搜尋引擎優化)
- `minimal_mistakes_skin`：選擇主題 background color，包含 https://mmistakes.github.io/minimal-mistakes/docs/configuration/
- `logo`：在網站 title 前插入徽標，將圖形放在`/assets/images/`目錄中，並將檔案名稱新增至此
- `search`：啟用全站搜索

### (2) Build settings

**用途**：設定網站的建置方式與輸出格式

- `markdown`: kramdown 用於 Markdown 轉換
- `remote_theme`：選用主題名稱
- `permalink`: /:categories/:title/ (預設永久連結樣式)
    - 文章 title: [2016-01-01-my-post.md](http://2016-01-01-my-post.md/), 文章 categories: foo
    - 永久連結: _site/foo/my-post/index.html
- `paginate`：每頁最多顯示貼文數目
- `timezone`：時區環境變量，Ruby 使用它來處理時間和日期，預設值是您 OS 設定的本地時區

### (3) Include

**用途**：告訴 Jekyll 要強制處理原本會因為命名規則而被忽略的檔案或資料夾，以被包含在網站 build 的過程中，才能被處理並輸出到最終網站顯示

**include**: - _pages

- 資料夾名稱以底線開頭：依照 Jekyll 的規則，它會被忽略，不會被處理成網頁
- _pages 資料夾：存放非部落格文章、自訂的頁面，ex. About、Home、Category、Tags …
    
    為了讓 _pages 裡的檔案能被 Jekyll 處理並轉成網頁，我們需要在 _config.yml 中透過 include 指令告知 Jekyll「請把 _pages 資料夾中的檔案一起處理」
    

### (4) Exclude from processing

**用途**：列出不希望 Jekyll 處理的檔案或目錄，例如 Gemfile、node_modules 等

### (5) Plugins (外掛)

**用途**：使用 GitHub Pages 託管時，主題使用了其中的幾個出網站建置時要啟用的外掛插件 (gem)

| Plugins | Description |
| --- | --- |
| jekyll-paginate | 分頁功能 |
| jekyll-sitemap | 生成符合 sitemaps.org 標準的地圖 |
| jekyll-gist | 支援嵌入 GitHub Gist |
| jekyll-feed | 產生 Jekyll 貼文的 Atom(類似 RSS feed) 提要 |
| jemoji | 支援在文章中使用 emoji 表情 |
| jekyll-include-cache | 快取 include 進的檔案，提高網站重建速度 |

### (6) Author

**用途**：定義作者側邊欄顯示基本資訊，向訪客介紹自己，ex. 姓名、簡歷、位置、電子郵件、社群網站

- `name`：姓名
- `avatar`：大頭貼路徑
- `bio`：簡歷描述
- `links`：社群網站連結

| Name | Description |
| --- | --- |
| label | Link label (e.g. "Twitter") |
| icon | [Font Awesome icon classes](https://fontawesome.com/v6/search) (e.g. "fab fa-fw fa-twitter-square") |
| url | Link URL (e.g. "https://twitter.com/mmistakes") |

### (7) Footer

**用途**：定義頁腳底部資訊、主題原生支援的社群網站，ex. Twitter、LinkedIn、GitHub、Stack Overflow

## Front Matter

### **Front Matter**

**位置**：每個文件 (ex. Markdown, HTML) 開頭都有獨立的 Front Matter**，**用 `---` 包起來的 YAML 區塊

**範圍**：單一檔案的特定資訊

**用途**

- **個別設定**：定義該文件專屬的 metadata，ex. layout、title、date、categories、permalink
- **生成控制**：告訴 Jekyll 如何處理、組織及渲染這個文件

### **Front Matter Defaults**（預設頁面屬性）

**位置**：_config.yml 的 default 區塊

**範圍**：多個檔案統一提供預設設定

**用途**

- **預設值設定**：在 _config.yml 設定指定類型檔案 (ex. post) 的共通屬性
- **節省時間**：每次新增 post, page 時，自動帶入預設值，讓所有內容都使用預設設定，不必在每個文件的 Front Matter 都重複寫相同設定，ex. author profiles, reading time, comments, social sharing

**defaults**：列表，包含不同 scope 的預設值

- **scope**
    - `path: ""` 表示針對所有路徑下的檔案
    - `type: posts` 適用於 _posts 資料夾中的文章
- **values:** 為文章預設設定
    - `layout: single`：使用單欄文章佈局
    - `author_profile: true`：顯示作者資訊
    - `read_time: true`：顯示預估閱讀時間
    - `comments: true`：啟用評論功能
    - `share: true`：啟用社群分享按鈕
    - `related: true`：啟用相關文章推薦

## 如何設定頁面的 URL

**用途**：讓使用者能夠在指定的 URL 看到輸出的 index.tml 頁面

- **預設**：Minimal Mistakes 主題於 _config.yaml 只有內建 category_archive 和 tag_archive，可透過 path 設定 URL，不需額外至 _pages/category-archive.md 和 _pages/tag-archive.md 設定 permalink
    
    > 若兩者同時設定，後者有較高優先權
    > 
- **自訂**：若想設定 category 與 tag 之外的頁面 URL (ex. about, post)，需另外建立 _pages/year-archive.md 並於 Front Matter 設定 permalink

### (1) 主題內建

**設定檔位置：**_config.yaml

- **category_archive:**
    - `type: liquid`：使用 Liquid 模板語言生成 category_archive 頁面
    - `path: /categories/`：造訪 [https://lilyfallasleep.github.io/categories/](https://lilyfallasleep.github.io/categories/) 時，會看到 category_archive 頁面 (_site/categories/index.html)
- **tag_archive:**
    - `type: liquid`：使用 Liquid 模板生成 tag_archive 頁面
    - `path: /tags/`：造訪 [https://lilyfallasleep.github.io/tags/](https://lilyfallasleep.github.io/categories/) 時，會看到 tag_archive 頁面 (_site/tags/index.html)

**自動生成檔位置：**_site/categories/index.html

執行 serve 指令後，Jekyll 會依照 `_config.yml` 的設定自動生成對應的 index.html 頁面

- _site/categories/index.html → URL：[https://lilyfallasleep.github.io/categories/](https://lilyfallasleep.github.io/categories/)
- _site/tags/index.html→ URL：[https://lilyfallasleep.github.io/tags/](https://lilyfallasleep.github.io/categories/)

### (2) 自訂來源檔

在 `_pages` 資料夾中建立 `about.md` 並於 Front Matter 設定 permalink

**來源檔位置：**_pages/about.md

- `permalink: /about/`：造訪 [https://lilyfallasleep.github.io/about/](https://lilyfallasleep.github.io/categories/) 時，會看到 about 頁面 (_site/about/index.html)

**自動生成檔位置：**_site/about/index.html

執行 serve 指令後，Jekyll 會依照 Front Matter 的設定生成對應的 index.html 頁面

- _site/about/index.html → URL：[https://lilyfallasleep.github.io/about/](https://lilyfallasleep.github.io/categories/)

```bash
# Site settings
# These are used to personalize your new site. If you look in the HTML files,
# you will see them accessed via {{ site.title }}, {{ site.email }}, and so on.
# You can create any custom variable you would like, and they will be accessible
# in the templates via {{ site.myvariable }}.
title: Lily Lin # 顯示在最上方的網站名稱
email:
description: >- # this means to ignore newlines until "baseurl:"
  Write an awesome description for your new site here. You can edit this
  line in _config.yml. It will appear in your document head meta (for
  Google search results) and in your feed.xml site description.
logo: 
twitter_username: username
github_username: lilyfallasleep
minimal_mistakes_skin: default # "air", "aqua", "contrast", "dark", "dirt", "neon", "mint", "plum", "sunrise"
logo: 
search: true

# Build settings
markdown: kramdown
remote_theme: mmistakes/minimal-mistakes
# Outputting
permalink: /:categories/:title/
paginate: 5 # amount of posts to show
paginate_path: /page:num/
timezone: # https://en.wikipedia.org/wiki/List_of_tz_database_time_zones

include:
  - _pages

# Exclude from processing.
# The following items will not be processed, by default. Create a custom list
# to override the default setting.
# exclude:
#   - Gemfile
#   - Gemfile.lock
#   - node_modules
#   - vendor/bundle/
#   - vendor/cache/
#   - vendor/gems/
#   - vendor/ruby/

# Plugins (previously gems:)
plugins:
  - jekyll-paginate
  - jekyll-sitemap
  - jekyll-gist
  - jekyll-feed
  - jemoji
  - jekyll-include-cache

author:
  name   : "Lily Lin"
  avatar : "/assets/images/bio-photo-comic.jpg"
  bio: |
    Deep-thinker, Passion-driven, Proactive person, Team player.  
    I’m an engineer with a background in computer science and machine learning.  
    I have great passion for software development and artificial intelligence.
  links:
    - label: "Website"
      icon: "fas fa-fw fa-link"
          url: "https://lilyfallasleep.github.io'"
    - label: "GitHub"
      icon: "fab fa-fw fa-github"
      url: "https://github.com/lilyfallasleep"

footer:
  links:
    - label: "GitHub"
      icon: "fab fa-fw fa-github"
      url: "https://github.com/lilyfallasleep"

defaults:
  # _posts
  - scope:
      path: ""
      type: posts
    values:
      layout: single
      author_profile: true
      read_time: true
      comments: true
      share: true
      related: true
  # _pages
  - scope:
      path: "_pages"
      type: pages
    values:
      layout: single
      author_profile: true

category_archive:
  type: liquid
  path: /categories/
tag_archive:
  type: liquid
  path: /tags/
```

## navigation.yml

頂部欄的配置，當視窗縮小導致沒有空間顯示所有選項時，會將項目移至切換選單中

**位置**：_data/navigation.yml

```bash
main:
  - title: "Posts"
    url: /posts/
  - title: "Categories"
    url: /categories/
  - title: "Tags"
    url: /tags/
  - title: "About"
    url: /about/
```

## /_includes

**目的**：儲存網站中重複使用的 HTML 和 Liquid 程式碼，用來組合成網站各個部分，ex. header、footer、author、navigation、comment，我們將它獨立出來，方便在多個頁面間共用

**優點**：維護簡單，當修改某個區塊時，只需更新 _includes 中的檔案，所有引用的頁面都會自動更新

**如何使用**：在其他 layout 中，可以用 Liquid 指令引入

### /_includes/head/custom.html

網站圖示 (Favicons) 是網址列中顯示的圖示，每個 Device/OS/platform 都有自己的標準

使用 [RealFavIconGenerator](https://realfavicongenerator.net/) 產生符合標準的圖片，並放入圖片資料夾 /assets/images/favicons/

## 💡YAML 中，如何換行、空格？:** 
**換行**
解析前  
    
    bio: |  
      
      Hi, my name is Lyn!

      Nice to meet you.

解析後
    
    Hi, my name is Lyn!
    
    Nice to meet you.
    

**空格**

解析前
    
    bio: >
    
      Hi, my name is Lyn!
    
      Nice to meet you.
    

解析後
    
    Hi, my name is Lyn! Nice to meet you.    
{: .notice}

---

## Reference

**從0搭建**

- https://jekyllrb.com/docs/
- https://www.shubo.io/jekyll-github-page-blog/
- https://chenuin.blogspot.com/2020/05/jekyll-getting-started.html
- https://yunchipang.github.io/setting-up-a-ghpages-site-with-jekyll.html
- https://medium.com/@nickhuang9527/%E4%BD%BF%E7%94%A8-jekyll-minimal-mistakes-%E5%9C%A8-github-pages-%E4%B8%8A%E6%9E%B6%E8%A8%AD%E8%87%AA%E5%B7%B1%E7%9A%84%E9%83%A8%E8%90%BD%E6%A0%BC-jekyll-x-minimal-mistakes-x-github-pages-c5699ffabd28

**現成搭建**

- https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/
- https://www.lixl.cn/2019/061036412.html
- https://kodeworker.github.io/%E6%95%99%E5%AD%B8/%E4%B8%80%E7%A2%B0minimal-mistakes%E5%B0%B1%E4%B8%8A%E6%89%8B/

**檔案架構介紹**

- https://mmistakes.github.io/minimal-mistakes/docs/configuration/
- https://renatogolia.com/2020/10/22/creating-this-blog-theme/
- http://tduyng.medium.com/build-your-personal-website-without-spending-any-money-30e6b2264e08
- https://jekyllrb.com/docs/structure/
- https://blog.csdn.net/weixin_51100018/article/details/130438900