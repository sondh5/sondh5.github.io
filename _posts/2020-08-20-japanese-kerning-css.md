---
layout: post
title:  Japanese kerning CSS
excerpt: Khoảng cách của các kí tự tiếng Nhật của mình trông cứ sai sai...
author: sondh5
categories: [ HTML/CSS ]
image_hidden: true
featured: false
status: private
---

Gần đây mình có làm 1 trang hiển thị tiếng Nhật sử dụng font Noto Sans JP, sau khi làm xong thi khoảng cách ở dấu 、。・ và các kí tự Katakana rất lớn, trông nó cứ sai sai. Sau 7749 giờ tìm hiểu bất lực thì mình được đồng nghiệp ném cho keyword là kerning và palt.

Dù vậy bài viết bằng tiếng Anh/Việt thì không có nên mình đã phải google dịch bài viết bằng tiếng Nhật :v

Vậy nên trong bài này mình sẽ lược dịch lại bài đó tại đây.
Link bài gốc ở đây nha https://ics.media/entry/14087/


<hr>


![](https://ics.media/entry/14087/images/kerning-font-feature-settings-palt__960.png)

Bên trái là đoạn hiện thị text mà mình thấy nó "trông cứ sai sai".

Bên phải là sau khi thêm đoạn css
```css
  .selector {
    font-feature-settings: "palt";
  }
```
Mục đích chính của mình là sự khác biệt của dấu câu và các kí tự katakana.


Nguồn tham khảo:
- https://ics.media/entry/14087/
- https://saruwakakun.com/html-css/reference/letter-spacing
