---
layout: post
title:  "Xây dựng trang cá nhân với gem Jekyll"
author: sal
categories: [ Jekyll, tutorial ]
image: assets/images/jekyll.png
featured: true
hidden: true
---

Nếu bạn là 1 dev Ruby on Rails thì với môi trường đã có sẵn, không mất đến 5 phút để bạn có riêng cho mình 1 trang cá nhân ngầu  theo các bước sau:

### Basic

```ruby
# Install Jekyll and Bundler gems through RubyGems
gem install jekyll bundler

# Create a new Jekyll site at ./myblog
jekyll new myblog

# Change into your new directory
cd myblog

# Build the site on the preview server
bundle exec jekyll serve

# Now browse to http://localhost:4000
```

### With theme

Trên đây là 1 basic blog, còn nếu muốn dùng 1 theme màu mè hơn, đẹp hơn thì có thể search google có vô vàn theme cho các bạn lựa chọn. Mình thì chọn của [@wowthemes](https://www.wowthemes.net/jekyll-themes-templates/)

Mình chọn [mediumish-theme-jekyll](https://github.com/wowthemesnet/mediumish-theme-jekyll/)

```ruby
# Clone project
git clone git@github.com:wowthemesnet/mediumish-theme-jekyll.git

# Rename to anything you want
mv mediumish-theme-jekyll blog

# Change into your blog
cd blog

# After create repo on your Github named blog, add it to origin
git remote add origin git@github.com:YOUR_GITHUB_ACCOUNT/blog.git

# Change _config.yml
baseurl: '/blog'

# Add your change
git add -A

# Commit them
git commit "Init amazing blog"

# Push them to your repo
git push origin master
```

Vậy là gần xong rồi, bạn chỉ cần vào settings của repo, trong phần Github page rồi chọn branch Master.

Tận hưởng thành quả thôi. Đây là blog của mình [https://sondh5.github.io/blog/](https://sondh5.github.io/blog/)

Let's have fun!

Chú ý:
- Cho người dùng mac thì nếu bị lỗi install gem ffi thì tham khảo [issue này](https://github.com/ffi/ffi/issues/651)  và [gist này](https://gist.github.com/Dreyer/0a0976f5606c0c963ab9a622f03ee26d).

Tham khảo:
- [https://jekyllrb.com](https://jekyllrb.com)
- [https://jekyllrb.com](https://github.com/wowthemesnet/mediumish-theme-jekyll)
