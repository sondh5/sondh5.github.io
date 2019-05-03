---
layout: tils_layout
title:  "Be careful when use find_by"
author: sondh5
categories: [ TILs, Rails ]
status: public
---

```ruby
City.find_by(name: "Maria") || City.find_by(name: "Aoi")
```
Liệu có giống với:
```ruby
City.find_by(name: ["Maria", "Aoi"])
```

Trông thì có vẻ giống đó, thử check SQL câu dưới xem

```ruby
Idol.find_by(name: ["Maria", "Aoi"])
# => SELECT  `idols`.* FROM `idols` WHERE `idols`.`name` IN ('Maria', 'Aoi') LIMIT 1
```
Trông vẫn có vẻ ổn, nhưng câu này lại trả ra `Aoi` thay vì `Maria` như mình mong đợi.

Vấn đề là hàm `find_by(arg, *args)` được định nghĩa như sau:

>Finds the first record matching the specified conditions. There is no implied ordering so if order matters, you should specify it yourself.
>If no record is found, returns nil.

```ruby
# File activerecord/lib/active_record/relation/finder_methods.rb, line 80
def find_by(arg, *args)
  where(arg, *args).take
rescue ::RangeError
  nil
end
```

Vì `no implied ordering`, nên khi gặp `Aoi` với id nhỏ hơn sẽ trả ra kết quả luôn thay vì tìm `Maria` trước theo như argument mà ta truyền vào.

Để có được kết quả như mong đợi mình phải dùng where và thêm order:
```ruby
Idol.where(name: ["Maria", "Aoi"]).order("FIELD(name, ('Maria, Aoi'))").take
# => SELECT  `idols`.* FROM `idols` WHERE `idols`.`name` IN ('Maria', 'Aoi') ORDER BY FIELD(name, ('Maria, Aoi')) LIMIT 1
```
