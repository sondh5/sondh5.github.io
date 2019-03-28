---
layout: post
title:  "Xây dựng trang cá nhân với gem Jekyll"
author: sondh5
categories: [ Jekyll, tutorial ]
image: assets/images/jekyll.png
featured: true
hidden: true
---

Nếu bạn là 1 dev Ruby on Rails thì với môi trường đã có sẵn, không mất đến 5 phút để bạn có riêng cho mình 1 trang cá nhân ngầu  theo các bước sau:

## Chuẩn bị
### Setup Ruby
Nếu bạn là RoR dev thì có thể bỏ qua bước này, còn nếu không thì: install ruby, install bundle

### Setup repo & page
**Tạo new repo**
![](https://guides.github.com/features/pages/create-new-repo-button.png)
để tên repo là `blog`
![](https://guides.github.com/features/pages/create-new-repo-screen.png)

**Setting Github page**
Chọn setting trong repo của bạn
![](https://guides.github.com/features/pages/repo-settings.png)

Kéo xuống phần github page và chọn master branch:
![](https://guides.github.com/features/pages/launch-theme-chooser.png)

Vậy là xong phần chuẩn bị rồi, bắt đầu nào!

## Bắt đầu

### Basic

```ruby
# Install Jekyll and Bundler gems through RubyGems
gem install jekyll bundler

jekyll new myblog

# Change into your new directory

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

# After create repo on your Github named blog, set it to origin
git remote set-url origin git@github.com:YOUR_GITHUB_ACCOUNT/blog.git

# Change _config.yml
baseurl: '/blog'

# Add your change
git add -A

# Commit them
git commit "Init amazing blog"

# Push them to your repo
git push origin master
```

Tận hưởng thành quả thôi. Đây là blog của mình [https://sondh5.github.io/blog/](https://sondh5.github.io/blog/)

Let's have fun!

Chú ý:
- Nếu không muốn để subpath là "/blog" thì bạn có thể đổi tên repo thành YOUR_GITHUB_ACCOUNT.github.io để có địa chỉ là YOUR_GITHUB_ACCOUNT.github.io <br>
Đừng quên sửa lại _config.yml: `baseurl: ""`
- Cho người dùng mac thì nếu bị lỗi install gem ffi thì tham khảo [issue này](https://github.com/ffi/ffi/issues/651)  và [gist này](https://gist.github.com/Dreyer/0a0976f5606c0c963ab9a622f03ee26d).

Tham khảo:
- [https://jekyllrb.com](https://jekyllrb.com)
- [https://github.com/wowthemesnet/mediumish-theme-jekyll](https://github.com/wowthemesnet/mediumish-theme-jekyll)
- [https://guides.github.com/features/pages/](https://guides.github.com/features/pages/)
