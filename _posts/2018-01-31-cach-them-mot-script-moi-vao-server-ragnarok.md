---
layout: post
title: Cách thêm script mới vào server Ragnarok
date: 2018-01-31 00:00:00
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

Nếu như bạn đã có một server Ragnarok cho riêng mình mà chưa biết phải thêm `NPC`mới vào server như thế nào thì bài viết này dành cho bạn. Nếu chưa có server hãy xem qua bài này: [Hướng dẫn cài đặt publicRO]({% post_url 2018-01-22-publicro-server-ragnarok-cho-moi-nguoi %}).

Bài viết này giúp giúp các bạn add nhưng `script` có sẵn vào nhé, còn cách tạo `npc` cụ thể thì sẽ có loạt bài sau.

#### Script trong rAthena là gì?

Đối với mình nó là một ngôn ngữ lập trình mini. Với các syntax, function được quy định với source rAthena. Chủ yếu script dùng để tạo `NPC` ngoài ra còn có thể dùng để bắt event và một số action khác mà có thể mình không biết.

- Folder: `server/npc`: [https://github.com/publicRO/server/tree/master/npc](https://github.com/publicRO/server/tree/master/npc)
- Document (tài liệu):
  - Wiki: [https://github.com/rathena/rathena/wiki/scripting](https://github.com/rathena/rathena/wiki/scripting)
  - Doc: [https://github.com/rathena/rathena/blob/master/doc/script_commands.txt](https://github.com/rathena/rathena/blob/master/doc/script_commands.txt)
- Editor: Mọi người có thể dùng Notepad++, Sublime Text, Atom hay bất kỳ editor nào bạn thích.

#### Hello World

Nếu bạn từng học lập trình thì chắc chắn chương trình đầu tiên bạn viết sẽ là `Hello World`.

##### 1. Hiểu về folder `npc`

Folder này chưa toàn bộ script của server:

![](/assets/images/posts/2018-01-31-cach-them-mot-script-moi/npc-folder.png)

Có 2 folder đăng biệt là `npc/pre-re` và `npc/re`. Dùng để xác định các `npc` riêng của server `renewal` hay `pre-renewal`.

Các file `*.conf` là những file quy định script nào được load khi start server.

Ví dụ nội dung 1 file như thế này:

```
// ----------------------- Basic Scripts -----------------------
npc: npc/custom/warper.txt
// npc: npc/custom/jobmaster.txt
// npc: npc/custom/platinum_skills.txt
// npc: npc/custom/healer.txt
// npc: npc/custom/breeder.txt
// npc: npc/custom/card_seller.txt
// npc: npc/custom/itemmall.txt
// npc: npc/custom/stylist.txt
// npc: npc/custom/resetnpc.txt
// npc: npc/custom/card_remover.txt
// npc: npc/custom/item_signer.txt
npc: npc/custom/woe_controller.txt
```

Những dòng có dâu `//` ở trước tức là đã bị comment, sẽ không chạy khi start server.

Như ví dụ trên thì chỉ có `npc/custom/warper.txt` và `npc/custom/woe_controller.txt` được load.

##### 2. Tạo file script của riêng mình

Tạo file script mới `npc/test/hello.txt`. Trong đó:

- `npc/test` là folder mình muốn lưu file script. Có thể dùng folder khác hay tạo folder mới trong `npc`.
- `hello.txt` tên file script, là file `*.txt`.

Đoạn code đầu tiên nào

```
prontera,156,145,4  script  Hello  58,{
	mes "[Hello NPC]";
	mes "Hello World";
}
```

Giải thích từng phần nhé:

`prontera,156,145,4  script  Hello  58,`

- `prontera`: Tên map muốn cho `npc` của mình vào. Lúc trong game có thể check bằng lệnh `/where`

- `156,145`: Tọa độ đứng, cũng có thể lấy bằng `/where` luôn.

- `4`: Góc `npc` quay mặt. `4` tức là quay mặt hướng 3h. Tham khảo bảng dướng đây

|      |                 |      |
| ---: | :-------------: | :--- |
|    1 |        2        | 3    |
|    8 | Nhìn đâu đây? ⏱ | 4    |
|    7 |        6        | 5    |

- `script`: Script Type, basic thì cứ là `script` thôi.
- `Hello`: Tên `npc` thêm dấu cách bình thường.
- `58`: `npc_id`, quyết định `npc` như thê nào. Vào đây để thấy ID: [http://nn.ai4rei.net/dev/npclist/](http://nn.ai4rei.net/dev/npclist/)

Sau dòng khai báo thông tin `NPC` thì sẽ đến nội dung của `NPC` đó. Đoạn nội dung này bắt đầu và kế thúc với cặp dấu ngoặc nhọn `{  }`. Với `npc` hiện tại của mình, nội dung chỉ có show ra 2 câu hội thoại.

```
mes "[Hello NPC]";
mes "Hello World";
```

Đó là toàn bộ script của mình.

##### 3. Khai báo script để load vào game

Như mình đã nói ở phần trước thì phải khai báo, lựa chọn `script` nào được load khi start server. 

- Mở file `/npc/scripts_test.conf` lên, các bạn có thể mở file khác.
- Thêm dòng này ở cuối file: `npc: npc/test/hello.txt`.
- Đơn giản đúng không.
- Tiếp đó là start server. Nếu server đã được start thì vào game với một account Admin dùng lệnh `@reloadscript` để load lại toàn bộ script.
- Check game nào!

#### Dùng script có sẵn.

Về phần hướng dẫn tạo `NPC` chỉ dùng lại ở như trên thôi, để nói sâu hơn mình sẽ có loạt bài khác hoặc bạn có thể vào [https://github.com/rathena/rathena/wiki/scripting](https://github.com/rathena/rathena/wiki/scripting) để tìm hiểu thêm.

Bây giờ mình sẽ giới thiệu các bạn một số nguồn tải script. Vì hiện tại [publicRO]({% post_url 2018-01-22-publicro-server-ragnarok-cho-moi-nguoi %}) đang dùng rAthena nên mình chỉ nhắc đến những nguồn tải script cho rAthena. Nếu bạn dùng script của Hercules thì sẽ bị lỗi.

- [https://rathena.org/board/forum/137-script-collections/](https://rathena.org/board/forum/137-script-collections/): Mình thấy đây có rất nhiều script hay, mình hay tìm script ở đây nhất.
- [https://rathena.org/board/forum/28-script-releases/](https://rathena.org/board/forum/28-script-releases/): Tương tự ở trên.
- [https://rathena.org/board/files/category/36-scripts/](https://rathena.org/board/files/category/36-scripts/): Trang download của rAthena, cũng khá nhiều script, nhưng nhưng script hay ho thường tính tiền :D
  - [Utilities](https://rathena.org/board/files/category/142-utilities/)
  - [PvP, GvG, WoE, Battleground](https://rathena.org/board/files/category/143-pvp-gvg-woe-battleground/)
  - [Games, Events, Quests](https://rathena.org/board/files/category/144-games-events-quests/)

Theo những nguồn này, các bạn lên tải về. Rồi copy vao folder `npc`, khai báo ở một file `*.conf` nào đó, start server.

Nếu trong trường hợp bạn chạy mà gặp lỗi ở trong script:

- Hãy kiểm tra lại bạn đã khai báo `npc` đúng chưa.
- Nếu đã đúng rồi mà vẫn lỗi thì là do script đã cũ sao với những thay đổi của rAthena, hãy hỏi người đăng script này. Hoặc hỏi trong Discord: [https://discord.gg/TNDA2S2](https://discord.gg/TNDA2S2)
- Nếu gặp một function hay 1 lệnh nào đó trong script mà muốn thì hiểu, hãy copy vào tìm trong file này: [https://github.com/publicRO/server/blob/master/doc/script_commands.txt](https://github.com/publicRO/server/blob/master/doc/script_commands.txt)

Chúc bạn có thể tìm được những `npc` ưng ý cho server của mình.