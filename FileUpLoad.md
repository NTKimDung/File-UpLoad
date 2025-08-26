# A. Lý thuyết
## I. Đăt vấn đề
### 1. Giới thiệu lỗ hổng File upload
Chắc hẳn các bạn đều đã quen thuộc với các tính năng thay đổi ảnh đại diện, ảnh bìa trong quá trình hoàn thành hồ sơ cá nhân. Quá trình tải lên một ảnh đại diện chính là đang thực hiện hành động upload file, cụ thể tệp tải lên ở đây là tệp tin dạng hình ảnh. Tải tệp lên là một tính năng cơ bản trong ứng dụng web và di động, cho phép người dùng chuyển tệp từ thiết bị của họ sang bộ nhớ trực tuyến. Tính năng này kết nối giao diện phía máy khách và phần mềm quản lý phía máy chủ, đảm bảo việc truyền tải tài liệu, hình ảnh và video an toàn và liền mạch. Về mặt kỹ thuật, đây là một thành phần nền tảng hỗ trợ các tác vụ như chia sẻ nội dung và quản lý tài liệu, khiến nó trở thành một khía cạnh thiết yếu của phát triển ứng dụng hiện đại. Giống với các chức năng khác, hành động upload file cũng ẩn chứa những mối nguy tới hệ thống. Dạng lỗ hổng này thường được gọi là File upload vulnerabilities.
### 2. Nguyên nhân gây ra lỗ hổng File upload
Lỗ hổng tải tệp lên có thể phát sinh vì nhiều lý do, bao gồm xác thực đầu vào của người dùng không đầy đủ, kiểm tra loại tệp không chính xác, quyền tệp không đủ hoặc thiếu xác thực nội dung.

Kẻ tấn công có thể khai thác những điểm yếu này bằng cách tải lên các tệp hình ảnh đơn giản chứa mã độc hoặc vi-rút, hoặc sử dụng phần mở rộng tệp lừa đảo để tránh bị phát hiện. Điều này có thể dẫn đến việc thực thi các tập lệnh phía máy chủ cho phép thực thi mã từ xa.
### 3. Tác động của lỗ hổng File upload
Tác động của lỗ hổng tải tệp lên thường phụ thuộc vào hai yếu tố chính:

* Lỗi xác thực
  
Các khía cạnh cụ thể của tệp mà trang web không xác thực chính xác, chẳng hạn như kích thước, loại hoặc nội dung. Nếu những khía cạnh này không được kiểm tra nghiêm ngặt, các tệp độc hại có thể được tải lên, dẫn đến vi phạm bảo mật.

* Hạn chế sau khi tải lên
  
Các hạn chế áp dụng cho tệp sau khi tải lên thành công. Nếu tệp được tải lên không được hạn chế đúng cách, tệp có thể thực thi mã độc, truy cập dữ liệu nhạy cảm hoặc làm gián đoạn hoạt động của máy chủ.

Lỗi tải tệp lên là mối lo ngại bảo mật đáng kể vì chúng có thể dẫn đến vi phạm dữ liệu, truy cập trái phép vào thông tin nhạy cảm và xâm phạm hệ thống.
### 4. Webshell
Webshell có thể hiểu là một dạng mã độc chứa các chức năng được xây dựng bởi kẻ tấn công, hỗ trợ họ trong quá trình khai thác và xâm nhập hệ thống dễ dàng hơn.

Webshell có thể xây dựng bằng nhiều ngôn ngữ lập trình khác nhau. Tùy vào công nghệ sử dụng và các đặc trưng của mục tiêu, kẻ tấn công có thể lựa chọn ngôn ngữ phù hợp để xây dựng Webshell cùng các chức năng mong muốn cho mình.

Thông thường, Webshell thường được sử dụng làm công cụ thu thập các thông tin, dữ liệu nhạy cảm; làm phần mềm trung gian cho việc tải lên hoặc lan truyền các dạng phần mềm, mã độc khác; Hỗ trợ cho các dạng tấn công khác cũng như chiếm quyền hệ thống; ...
# B. Thực hành
## I. Exploiting unrestricted file uploads to deploy a web shell (Khai thác tải lên tệp không giới hạn để triển khai shell web)
### 1. Lab: Remote code execution via web shell upload (LAB: Thực thi mã từ xa thông qua tải lên shell web)
Các bước thực hiện:
* Bước 1: Đăng nhập vào account mà web cung cấp với `Name: wiener` và `Passwword: peter`
  <img width="1865" height="962" alt="image" src="https://github.com/user-attachments/assets/aa30092e-3d01-4f3e-a6ee-e4ac0d6117f3" />
  <img width="1862" height="971" alt="image" src="https://github.com/user-attachments/assets/bfd1b751-cff9-4548-b906-41d8fde792ff" />
  Kết quả:
  <img width="1853" height="912" alt="image" src="https://github.com/user-attachments/assets/879c1e64-81f5-467f-8f36-16117fb60725" />

*Bước 2: Thực hiện upload file để thay dổi hình avatar
Up file `meo-meo-4.jpg`:
<img width="1843" height="913" alt="image" src="https://github.com/user-attachments/assets/9f330867-f22d-4265-b066-7468a1d4406c" />
Trang web sẽ hiện ra thông báo up file thành công:
<img width="864" height="274" alt="image" src="https://github.com/user-attachments/assets/07e9061b-31c6-4faf-8bb3-45a82e4b6f36" />
Kết quả là ở trang web ta sẽ thấy được hình ảnh ta thay dổi avatar hiện lên:
<img width="1247" height="911" alt="image" src="https://github.com/user-attachments/assets/f8a94edf-4d1d-4136-93a1-da8a04ef7f0e" />

*Bước 3: Điều tra sâu:

Ở bước này ta điều tra trang web bằng công cụ burp suite:
Ta xem các yêu cầu GET/POST tại tab HTTP history như sau: Ta chú ý vào method `POST` 

<img width="1925" height="1080" alt="image" src="https://github.com/user-attachments/assets/ab08bfbf-ae31-4cab-a60d-0a6cf41259ea" />   

Ở bước này ta quan sát bộ request (yêu cầu) và response (phản hồi) giữa trình duyệt ↔ server khi bạn thực hiện hành động như upload avatar.

Với ý nghĩa như: 
Xác định loại request

Ở hình: ta thấy dòng POST /my-account/avatar → nghĩa là khi bạn upload file, trình duyệt gửi request POST kèm dữ liệu file đến server.

Xem dữ liệu gửi đi

Trong khung Request bạn thấy:

Header (User-Agent, Cookie, Content-Type, Boundary multipart/form-data...)

Body: chứa nội dung file meme-meo-4.jpg.
→ Điều này giúp bạn hiểu chính xác cách dữ liệu được gửi.

Xem phản hồi từ server

Trong khung Response: server trả về HTTP/2 200 OK + thông báo file đã được upload.

Điều này cho thấy server đã chấp nhận và xử lý file thành công.

* Bước 4: Mô phỏng các bước thực hiện tấn công qua Repeater với:
  <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/679613b8-99af-468c-8562-cf38383abe84" />
  <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/4fdc55ae-0ddd-4d75-b9a0-ad83a17e2db8" />
  
Mục đích Repeater là để quan sát response của server sau mỗi lần gửi lại (replay) một request nhiều lần mà không cần thao tác lại trên trình duyệt hoặc chỉnh sửa request (thêm/xóa header, đổi tham số, đổi filename/file content trong upload, đổi cookie…) có thay đổi hay không → từ đó kiểm tra hệ thống có lỗ hổng hay không.

Ở Request `Upload` với nội dung POST /my-account/avatar mà tôi đã gửi từ trình duyệt (qua Proxy rồi gửi sang Repeater).

Nó chứa thông tin file bạn upload (meme-meo-4.jpg).

Response bên phải: server phản hồi "The file avatars/meme-meo-4.jpg has been uploaded." → nghĩa là upload thành công. 

* Bước 5: Thực hiện các bước tấn công như sau:

 Ta thay đổi tên file `meme-meo-4.jpg` ở Request thành `myexploit.php` và chèn thêm ột đoạn code dộc hại `<?php echo file_get_contents('/etc/passwd'); ?>` vào Request và kết quả như hình.
 <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/2c1cc1ae-129c-4cdf-8aaa-3d1bcb5977f4" />
Sau khi thực hiện thay đổi đuôi file từ `.jpg` sang `.php` và chèn đoạn mã độc PHP vào nội dung file tuy nhiên kết quả bên trang Respone là hiển thị file đã upload thành công tức là trang web này không có cơ chế kiểm tra định dạng file nghiêm ngặt nên File myexploit.php đã được lưu thành công trên server dưới dạng file thực thi PHP.

Nghĩa là kẻ tấn công hoàn toàn có thể truy cập URL dẫn đến file vừa upload để kích hoạt mã độc, khi truy cập, server sẽ thực thi đoạn lệnh `<?php echo file_get_contents('/etc/passwd'); ?>` và trả về nội dung file `/etc/passwd`.

Ý nghĩa ở bước thực hiện này là:
Việc response trả về upload thành công chính là dấu hiệu khẳng định lỗ hổng File Upload Vulnerability tồn tại, và hacker có thể khai thác.

* Bước 6: Mô phỏng chạy file mã độc đã được lưu ở server sau khi thực hiện ở bước 5:
Ta thực hiện ở tab Repeater `Show` để thấy được kết quả sau khi gọi file `myexploit.php` có chứa mã độc như sau:
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/2e765aab-180e-4e16-a4df-e69cc77c5740" />

Nội dung trả về ở trang Respone là kết quả lệnh file_get_contents('/etc/passwd').

Do đó bạn thấy toàn bộ nội dung file /etc/passwd của máy chủ bị lộ ra.

* Ý nghĩa bài lab này là:
Ta biết được lỗ hổng của trang web là:
Trang web cho phép người dùng upload file tuy nhiên nó không kiểm tra đúng loại file, đuôi file và không lọc nội dung độc hại, dẫn đến có thể upload file độc hại do kẻ tấn công xây dựng cụ thể ở đây là file `myexploit.php`.
Cũng như biết được cách thức khai thác của kẻ tấn công như:
Kẻ tấn công đổi đuôi file từ .jpg thành .php và chèn mã độc và Upload thành công file được lưu trong thư mục public sau khi truy cập file này qua trình duyệt, server thực thi mã độc thay vì hiển thị ảnh.

## II. Exploiting flawed validation of file uploads (Khai thác xác thực thiếu sót của tải lên tệp)
### 1. Flawed file type validation (Xác thực loại tệp thiếu sót) - Lab: Web shell upload via Content-Type restriction bypass (Lab: Web Shell Tải lên thông qua Bỏ qua hạn chế loại nội dung)
* Tương tự bước 1 ở Lab trên ta đăng nhập vào trang web.
Bước 2:






 








