---
layout: post
title: Cannot overwrite monster name when spawn
date: 2019-06-24 23:20:00 0700
categories:
- Developer
tags:
- ragnarok-online
- hercules
- ragnarok-online-emulator
- server
---
Ok. Đây không hẳn là blog mà chỉ như một take note về việc mình thấy bug và tạo issue cho <a href="https://github.com/HerculesWS/Hercules" target="_blank">Hercules</a>.

_ps: Ai đi ngang qua mà không biết mình đang nói đến cái gì và Hercules là gì thì bỏ qua bài này nhé!_

Lỗi ở đây là khi mình chạy script event Poring Catcher thì thấy khi Poring spawn ra thì name giống nhau hoàn toàn. Trong script thì rõ ràng là đã overwite lại name rồi.

Vậy là mình thử viết 1 script đơn giản  để test và để đảm bảo là issue từ server chứ không phải script.

```
prontera,155,185,0,0	monster	New poring	1002,1,0,0,0
```

 Tên monster mình muốn show ra là **New poring** nhưng sau khi spawn thì nó vẫn là **Poring**, tên từ DB. Xác định là lỗi của server nên mình tạo 1 ticket trên <a href="https://github.com/HerculesWS/Hercules/issues/2495" target="_blank">github</a> để report vụ này.

Rất nhanh sau đó có <a href="https://github.com/dastgirp" target="_blank">dastgirp</a> và <a href="https://github.com/4144" target="_blank">4144</a> vào fix luôn. Mà chắc cũng do cái này dễ. Mình ngu không tự fix được thôi.

Rồi, cách fix đơn giản thế này. File: `src/map/clif.c`

```diff
@@ -9480,7 +9480,8 @@ static void clif_mobname_normal_ack(int fd, struct block_list *bl)
	struct PACKET_ZC_ACK_REQNAME_TITLE packet = { 0 };
	packet.packet_id = HEADER_ZC_ACK_REQNAME_TITLE;
	packet.gid = bl->id;
-	memcpy(packet.name, BL_UCCAST(BL_MOB, bl)->db->name, NAME_LENGTH);
+	const struct mob_data *md = BL_UCCAST(BL_MOB, bl);
+	memcpy(packet.name, md->name, NAME_LENGTH);
#if PACKETVER_MAIN_NUM >= 20180207 || PACKETVER_RE_NUM >= 20171129 || PACKETVER_ZERO_NUM >= 20171130
	struct unit_data *ud = unit->bl2ud(bl);
	if (ud != NULL) {
```

File `src/map/clif.c` là một file thuộc Map server. Mình không biết nhiệm vụ cụ thể của nó là gì. Chỉ biết nó rất dài, đến hơn 23k line. Nhưng đoạn trên thì hiểu.

Hiện tại `mobname_normal` đang được show name ra bằng cách này `->db->name` từ đó dẫn đến việc name luôn là từ DB lấy ra. Dù script có có overwrite lại thì cũng không show ra. 

Vậy nên sửa lại thành thế này: `->name`. Đơn giản là trỏ đến name thôi. Nếu được overwrite thì sẽ lấy name đó, không thì vẫn là name từ DB. 

Thực ra khi dùng script để spawn monster thì đã phải fill name cho nó rồi, vẫn đề là dùng tên như trong DB hay tên khác thôi.

Cuối cùng đợi release milestone **Release v2019.06.30** và cảm ơn Hercules team!