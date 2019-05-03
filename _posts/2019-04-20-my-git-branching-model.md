---
layout: post
title:  Git branching model mà mình theo đuổi
excerpt: Flow này có gọi là mô hình xương rồng (cactus model), xu hướng rewrite history. Tối giản tối đa git tree của bạn.
author: sondh5
categories: [ Git ]
image: https://cdn0.tnwcdn.com/wp-content/blogs.dir/1/files/2018/03/GitHub-brave-hed-796x418.jpg
image_hidden: true
featured: true
status: public
---

{% include figure image_path="https://user-images.githubusercontent.com/46481345/55465834-2622b480-5628-11e9-954b-72f6ba496bae.png" caption="My cactus model" %}

Flow này có gọi là mô hình xương rồng (cactus model), xu hướng rewrite history.<br>
Các nhánh dev sẽ không bao giờ merge lại master, các commit sẽ được cherry-pick hoặc merge squash vào 1 nhánh master duy nhất.

### Workflow example
**I. Khi có chức năng mới**
1. Pull code mới nhất từ master về
2. Leader checkout nhánh feature tổng từ master

**II. Khi có task/bug mới**
1. Pull code mới nhất từ nhánh tổng
2. Dev checkout nhánh task/bug từ nhánh feature tổng
3. Coding trên nhánh task/bug, tạo pull request đến nhánh feature tổng
4. Dev review chéo rồi approve, leader review, approve và **merge squash** vào nhánh tổng

**III. Khi release**
1. Leader tạo pull request từ nhánh feature tổng đến master
2. Leader **merge squash** PR vào master, rewrite commit message

**IV. Khi nhánh feature bị outdate so với master**
1. Leader rebase master vào feature tổng, fix conflict nếu có
2. Leader push -f để update nhánh feature tổng, thông báo với cả team
3. Dev tự update lại nhánh task/bug của bản thân và gửi lại pull request

**Chú ý:**
- Không push trực tiếp code lên nhánh feature tổng
- Luôn sử dụng squash để dễ dàng review commit trong nhánh tổng và master
- Không để tồn tại merge commit trên nhánh feature/master
