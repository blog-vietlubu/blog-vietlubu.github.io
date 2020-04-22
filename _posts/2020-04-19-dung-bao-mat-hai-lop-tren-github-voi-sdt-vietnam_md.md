---
layout: post
title: Dùng bảo mật hai lớp của Github với số điện thoại Việt Nam
date: 2020-04-19 16:00:00 0700
photos: 
categories:
- Developer
tags:
- github
- 2fa
---
Mở bảo mật hai lớp gần như là việc bắt buộc mình làm khi sử dụng bất kỳ một dịch vụ online nào. Trừ trường hợp dịch vụ đó không có hỗ trợ thôi. Bình thường, chúng ta sẽ có 2 phương thức để sử dụng tính năng này. Đó là qua những app Authenticator hoặc qua SMS đến số điện thoại. Mình thì thường dùng cả 2. Qua app Authenticator và mở option backup qua số điện thoại để trách trường hợp app có vấn đề.

Với Github, có đủ 2 cách trên. Tuy nhiên với  cách thức nhận mã xác thực qua điện thoại thì Github lại không hỗ trợ số điện thoại tại Việt Nam. Khó hiểu!!! Hôm nay mình đã thử dùng chút "gian lận" xem có dùng được số điện thoại Việt Nam không. Và nó thành công mới hay. Và đây là cách mình đã làm. Anh em nào dùng Github để làm việc thì có thể tham khảo nhé.

**Bước 1:** Vào Setting scurity: <a target="_blank" herf="https://github.com/settings/security">https://github.com/settings/security</a>

Ở đây chúng ta mở bảo mất 2 lớp bằng "Authenticator app" như bình thường.

**Bước 2:** Ở phần "Fallback SMS number", khi add số điện thoại vào thì sẽ không thấy mã quốc gia Việt Nam đâu hết.

![Không có mã vùng Việt Nam trong danh sách](/assets/images/posts/2020-04-19-dung-bao-mat-hai-lop-tren-github-voi-sdt-vietnam/khong-ma-vung-vietnam.png)

**Bước 3:** Trick chút nào! Bạn mở Inspect chọn select box **Country code**. Sau đó, mở thẻ select ra bạn sẽ thấy option đầu tiên là United States +1 với `value="+1"` . Giờ việc của chúng ta là đổi +1 này thành +84. Nhập số điện thoại vào **Phone number** rồi chọn **Set fallback**

![Inspect](/assets/images/posts/2020-04-19-dung-bao-mat-hai-lop-tren-github-voi-sdt-vietnam/inspect.png)

Bước 4: Lúc này bạn sẽ nhập được mã xác thưc gửi qua SMS đến số điện thoại, hoàn tất cài đặt thôi.

![Inspect](/assets/images/posts/2020-04-19-dung-bao-mat-hai-lop-tren-github-voi-sdt-vietnam/SMS.png)