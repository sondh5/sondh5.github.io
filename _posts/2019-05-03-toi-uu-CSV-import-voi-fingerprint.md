---
layout: post
title:  Tối ưu CSV import với fingerprint
excerpt: Mình đã giảm thời gian import CSV từ 6 tiếng xuống còn 50 phút với kĩ thuật fingerprint.
author: sondh5
categories: [ Rails ]
image: https://www.hsbc.co.uk/content/dam/hsbc/gb/images/fingerprint.jpg
image_hidden: true
featured: true
status: public
---

Chuyện là khách của mình bán sản phẩm X, hệ thống của ổng có ~1 triệu sản phẩm.  
Mỗi ngày ổng sẽ export database 1 file CSV, gửi cho mình import vào hệ thống T để thống kê.  
Trong file CSV, sẽ có những thay đổi như:
- Sản phẩm thêm mới
- Sản phẩm ngưng kinh doanh
- Sản phẩm thay đổi trạng thái (còn hàng, hết hàng...)
- Sản phẩm không thay đổi gì (~70-80%)

#### Logic xử lí hiện tại
- Đọc từng dòng CSV
- Parse CSV
- Import sử dụng Parallel Import x4 processes

Thời gian cho mỗi lần import ~6 tiếng. Mỗi ngày có 24h mà mất 6h để import thì import xong dữ liệu cũng outdate :v 

#### Bài toán
- Vấn đề: số lượng sản phẩm không thay đổi gì khá lớn, những vẫn rất mất nhiều thời gian để đọc, parse rồi check trùng lặp  
- Ý tưởng: Check trùng lặp trước khi parse, vậy thì chỉ cần parse và import 20-30% số dòng thay vì 100% như trước đây
- Kỹ thuật: Sử dụng kĩ thuật fingerprinting giống như cách [Rails xử lí Asset Pipeline](https://guides.rubyonrails.org/asset_pipeline.html#what-is-fingerprinting-and-why-should-i-care-questionmark)

#### Xử lí
- Tạo 1 Set trong Rails cache, đặt tên là `fp_products_list`
```ruby
fp_products_list = Rails.cache.fetch("fp_products_list") { Set.new } 
```
Lý do mình dùng Set có thể đọc thêm [Ruby Set]({% link _posts/tils/2019-04-26-ruby-set.md %})  


- Với mỗi sản phẩm import thành công, tạo ra 1 fingerprint cho sản phẩm đó
```ruby
finger_print = Digest::MD5.base64digest(row.to_json)
```
mình sử dụng `base64digest` vì nó ngắn hơn, sẽ tiết kiệm size hơn so với `hexdigest`  

- Đưa fingerprint vào `fp_products_list`
```ruby
fp_products_list.add(finger_print)
Rails.cache.write("fp_products_list", fp_products_list)
```

- Trong những lần import sau, kiểm tra xem product đó có thay đổi gì so với lần trước hay không bằng fingerprint  
```ruby
CSV.foreach(file) do |row|
    next if fp_products_list&.include?(Digest::MD5.base64digest(row.to_json))
    # [...]
end
```
Vậy là số dòng phải parse và import giảm được khoảng 75%. Kết quả là thời gian import của mình đã giảm từ 6h xuống còn 53 phút :D 
