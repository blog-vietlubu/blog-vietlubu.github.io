---
layout: post
title: publicRO - server Ragnarok cho mọi người
date: 2018-01-22 00:00:00
photos: /assets/images/posts/publicro-server-ragnarok-cho-moi-nguoi/screenpublicRO000.jpg
categories:
- publicRO
tags:
- games
- publicRO
- ragnarok-online
- rathena
- server
---

Mục đích ra đời
---------
- Trước hết, bản thần mình muốn có một server RO có thể khởi tạo nhanh chống để chơi `offline` hoặc lâu lâu sẽ test script mới hay là item mới.
- Tiếp đó mình muốn nhiều anh em chơi RO biết rõ hơn về cách xây dựng server, Để có thể tạo một server chơi cùng bạn bè hay thậm chí là mở server online cho tất cả mọi người.
- Chia sẻ. Bản thân mình cũng chỉ biết những vấn đề cơ bản của RO server, hay [rAthena](https://github.com/rathena/rathena/). Mình sẽ cố gắng để sưu tầm những script, item hay map để đống góp vào `publicRO`. Và hy vọng sẽ có những người khác có cùng suy nghĩ với mình.
- Tiếp theo `publicRO` có thể sẽ là một loạt bài của mình về cách tạo `NCP` cách thêm `item`, `monster`, `map` vào RO.

publicRO là gì?
---------

`publicRO = rAthena + rAsql + RO client + ♥`

> rAthena is a collaborative software development project revolving around the creation of a robust massively multiplayer online role playing game (MMORPG) server package. Written in C, the program is very versatile and provides NPCs, warps and modifications. The project is jointly managed by a group of volunteers located around the world as well as a tremendous community providing QA and support. rAthena is a continuation of the eAthena project.

- [rAthena](https://github.com/rathena/rathena/) là một bộ mã nguồn mở (open sourse), được phát triển để xây dựng server game Ragnarok Online.
- Mặc định [rAthena](https://github.com/rathena/rathena/) hoạt động với MySQL, đồng nghĩa với việc nến muốn khởi chạy một server RO thì thì phải khởi chạy service MySQL hay phải có một server khác chạy MySQL. Điều này sẽ dẫn việc nếu bạn chỉ muốn chơi `offline` hay test sơ qua vài script của rAthena thì sẽ tốn thêm chút thời gian. Vậy nên [rAsql](https://github.com/rathena/rAsql) ra đời để bỏ qua việc cài đặt MySQL.
- `publicRO` nói ngắn gọn là một server RO có thể khởi tạo nhanh mà cách bạn không cần phải làm gì hết, kể cả việc `compile`. Chỉ cần `start` là đủ.
- `publicRO` không phải là một server online. Nó có thể là một server offline để bạn có thể chơi trên máy mình. Bạn cũng có thể public ra cho bạn bè cùng chơi, hay thậm chí là mở một server online. Sẽ có những bài viết khác giúp bạn làm những việc này một cách đơn giản.

Tính năng
---------

`publicRO` hiện tại cũng có những chức năng cơ bản:
- Client renewal
- Tất nhiên có job 3 và Doram
- Có sẵn một `ID` admin. Login bằng ID và pass như sau: `admin/admin`
- Max level mình không đổi.
- Rate thì có đổi lại chút. `x25` cho cả `exp` và `drop`
- Enable vài NPC custom cơ bản của `rAthena`
```
    // server/npc/scripts_custom.conf
    // ----------------------- Basic Scripts -----------------------
    npc: npc/custom/warper.txt
    npc: npc/custom/jobmaster.txt
    npc: npc/custom/platinum_skills.txt
    npc: npc/custom/healer.txt
    npc: npc/custom/breeder.txt
    npc: npc/custom/card_seller.txt
    npc: npc/custom/itemmall.txt
    npc: npc/custom/stylist.txt
    npc: npc/custom/resetnpc.txt
    npc: npc/custom/card_remover.txt
    npc: npc/custom/item_signer.txt
    npc: npc/custom/woe_controller.txt
```

- Sắp tới sẽ có những bài hướng dẫn để các bạn tự custom server của riêng mình.



Cài đặt
---------
#### 1. Download
- [publicRO server](https://github.com/publicRO/server): Link tải trực tiếp: https://github.com/publicRO/server/archive/master.zip
- [rAsql](https://github.com/publicRO/rAsql): Link tải trực tiếp: https://github.com/publicRO/rAsql/archive/master.zip 
- publicRO client: [Full client](https://drive.google.com/open?id=1kkbmBTka_4x-s3iX4HL-W8ocgs5sciCO). Hoặc [Lite client](https://github.com/publicRO/lite-client). Các bạn nên tải bản full.

Note: Chút lưu ý về lite-client, bạn có thể đọc ở [đây](https://github.com/publicRO/lite-client/blob/master/README.md). Dưới đây mình sẽ tóm tắt lại lưu ý.
> Với Lite-client, hiện tại mình đã thử với DarksideRO, TalonRO và NovaRO thì chỉ có một mình [DarksideRO](http://panel.darkside-ro.com/) chạy được. Nên mình khuyên các bạn nên tải bản [Full client](https://drive.google.com/open?id=1kkbmBTka_4x-s3iX4HL-W8ocgs5sciCO) hoặc tải [DarksideRO](http://panel.darkside-ro.com/) và bản lite-client. Hiện tại mình đang chơi DarksideRO và TalonRO.

Sau khi tải xong về giải nén bất kỳ đâu bạn muốn.

#### 2. Khởi động rAsql

Mở `rAsql\mysql_start.bat` Nếu thấy thông báo thành công như:

```
The MySQL server is working on disk Z:\ [port 3306]

Press any key to continue . . .
```

Lúc này bạn có thể thấy cửa sổ connect MySQL, bạn có thể ấn OK để connect và theo dõi database.

Nếu không thấy có mà buốn theo dõi DB thì có thể mở `rAsql/udrive/bin/heidisql.exe`

Đồng thời, máy bạn cũng sẽ xuất hiện một ổ đĩa ảo, ở máy mình là `Z:\`. ổ này sẽ mất khi bạn stop. Những dữ liệu của bạn thì không mất.

#### 3. Khởi động server

Mở `server/runserver.bat`. 3 cửa sổ CMD sẽ được mở lên, chờ 1-3 phút nếu không có dòng thông báo đỏ nào thì bạn đã start thành công.

#### 4. Khởi động game

Sau khi `rAsql` và `server` đã start thành công. Bạn có thể mở `publicRO/publicRO.exe` để khởi động game.

Để đăng ký account thì ở lần đăng nhập đầu tiền bạn hãy nhập.

```
ID: idcuaban_M
Password: password
```

Trong đó có `_M` là xác định gới tính nam `_F` là nữ. Những lần đăng nhập sau bạn không cần những hậu tố này nữa.

#### 5. Video start publicRO

Mình có làm một video ngắn về việc khởi động `publicRO` từ rAsql cho đến server. Làm theo 3 bước (2-3-4) ở trên - 1 phút thôi:

<iframe width="560" height="315" src="https://www.youtube.com/embed/Thqs6xHMcrQ?rel=0" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

#### 6. Cách tắt server

Cái này cũng khá quan trọng. Đừng tắt nang những cửa sổ `cmd`, có thể dẫn đến việc bạn không thể login được nữa khi `run` server lại.

- Đầu tiên, login một account admin vào game. (`admin/admin` mình đã tạo sẵn)
- Gõ lệnh `@kickall`: lệnh này dùng để kick hết rất cả user ra. Bạn chơi một mình thì không quan trọng lắm.
- Gõ lệnh `@mapexit`: lệnh này dùng để tắt map server. Lúc đó nhận vật của bạn sẽ bị disconnect
- Ngay lúc đó chuyển sang màn hình `cmd` của `map-server.exe`.  Nhanh tay ấn `ctrl+c` nhập `y` và `enter`. Nếu không sau 15 giây `@mapexit` thì map-server sẽ restart lại. Thấy nhiều thao tác nhưng không phức tạp lắm đâu. Lỡ nó restart lại rồi thì mình lại login admin làm lại thôi :D
- Nếu bạn đã lỡ `stop` thẳng tay mà không chạy `@mapexit`, rồi sau đó `start` lại mà không login vào được thì khởi động lại máy thôi :)

Đó là những lưu ý về việc tắt server. Còn về MySQL (rAsql) thì như sau.

- Sau khi stop server.
- Chạy file `rAsql/mysql_stop.bat`
- Vậy là xong.
- Trường hợp quên stop `rAsql` mà tắt máy thì mình chưa thử, nhưng mình nghĩ sẽ không có vấn đề gì. có khi lúc mở máy lên không cần phải chạy `rAsql` nữa :D



Nếu có vấn đề?
---------

Nếu gặp vấn đề hãy để lại câu hỏi ở:

- Comment ngay dưới blog này. Hoặc:
- Facebook Page (chưa có like nào :D): <a href="https://www.facebook.com/publicRO/" target="_blank">https://www.facebook.com/publicRO/</a> - Mình sẽ post những quicktip, hướng dẫn nhanh vào page facebook.
- Discord Chat (chưa có member nào :D): <a href="https://discord.gg/TNDA2S2" target="_blank">https://discord.gg/TNDA2S2</a> - Kênh chat thảo luận tất cả mọi thứ về Ragnarok, kể cả BOT
- Hay Group Facebook (có thể sẽ không dùng vì đã có Discord): <a href="https://www.facebook.com/groups/ragnarokviet/" target="_blank">https://www.facebook.com/groups/ragnarokviet/</a>

