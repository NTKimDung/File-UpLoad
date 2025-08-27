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
Bước 2: Ta thực hiện up load một file với đuôi `.php` lên server, tuy nhiên ở trang web chỉ phép upload file ảnh (JPEG, PNG).

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/a4a4ee78-d7dc-4fa6-be93-0163049f9e2e" />


<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/f014ebc7-e88a-4f56-a9c5-52029a7f783f" />

Trang web có cơ chế lọc file upload:

Nó chỉ cho phép file có Content-Type image/jpeg hoặc image/png.

Khi bạn upload file shell.php, trình duyệt gửi Content-Type mặc định là application/octet-stream → bị chặn.

* Bước 3: Thực hiện điều tra sâu bằng công cụ burp suite:
  Ở bước này ta theo dõi ở tab Repeater ở dòng `Content-Type` ta thấy được file ta chèn vào là loại đuôi được hiển thị ra là `application/octet-stream` hiển thị như hình.
  
  <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/d6f23e5d-3a8f-4edb-b8b4-0f04877c1ac7" />

  vì trang web có cơ chế lọc đuôi file nên ta thực hiện mô phỏng bằng cách thay đổi đuôi từ `application/octet-stream` sang `image/jpeg` trong request là để bypass bộ lọc Content-Type của server. Kết quả sau khi send request đã thay đổi thì trang web lại up load thành công file shell.php lên server (vì server sẽ tưởng rằng file của bạn là ảnh vì vậy server cho phép upload, dù thực chất đây là file PHP):
  <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/f45c9a92-d1ab-4b74-9efc-29ae6c768ecd" />

  Kết quả ở trang web ta có thể thấy được file shell.php được up load lên:
  
  <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/03485468-d86b-42a8-abeb-50b2bfdca32b" />

 * Bước 4:
   Tại bước này ta đã chèn thành công file `shell.php` vào server mà trong file mã độc có đoạn code `<?php system($_GET['command']); ?>`. Trong đoạn mã trên, biến `$_GET['command']` sẽ lấy giá trị từ tham số command trên URL và truyền vào hàm system() để thực thi trên hệ điều hành của server.

Ví dụ: khi ta truy cập đường dẫn: `shell.php?command=ls` thì PHP sẽ thực thi lệnh ls trên hệ thống. Kết quả là server sẽ liệt kê các file và thư mục trong thư mục hiện tại, sau đó hiển thị ngay trên trang web.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/cdee2e61-ffac-4296-b668-eb5d534397b7" />

Ta có thể mô phỏng khai thác của kẻ tấn công váo server bằng cách khai thác qua công cụ burp suite như sau:
Khi thực hiện câu lệnh `command=ls` trên URL và hiển thị kết quả ở trang web thì ta có thể thay đổi lệnh `ls` trong request ở tab Repeater thành các lệnh khác để thực hiện tấn công vào trang web.
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/0b0e785b-7475-432d-981b-92040dfd0d48" />

*Ý nghĩa bài lab: 

Bài lab này minh họa một điểm yếu phổ biến trong cơ chế upload file trên ứng dụng web.
Mặc dù ứng dụng đã triển khai biện pháp lọc đuôi file (ví dụ: chặn .php, .asp, …) để ngăn ngừa việc upload file thực thi, nhưng lại không kiểm tra nội dung bên trong file.

Điều này tạo ra sơ hở cho kẻ tấn công có thể bypass cơ chế lọc bằng cách đổi tên file hoặc sử dụng các đuôi file hợp lệ nhưng vẫn được server xử lý như file thực thi (ví dụ: shell.php → shell.php.jpg, shell.pHp, shell.php%00.png, …). Và sau khi upload thành công, nội dung bên trong (chứa mã độc PHP như <?php system($_GET['command']); ?>) vẫn được server diễn dịch và thực thi.
  
Từ đó kẻ tấn công có thể thực thi lệnh từ xa (RCE) trên server thông qua tham số được truyền trên URL.

* Cách phòng tránh:

 Đây là minh chứng rằng chỉ lọc đuôi file là không đủ an toàn, cần phải:

Kiểm tra MIME type thực sự của file là đọc trực tiếp từ nội dung file → khó giả mạo hơn, giúp phát hiện file độc hại đội lốt hình ảnh.

Lưu file ở thư mục không thực thi được (non-executable directory).

Triển khai thêm cơ chế sandbox là tạo ra một môi trường "cách ly" (an toàn, giới hạn) để chạy thử hoặc xử lý file mà người dùng upload trước khi cho nó hoạt động trên hệ thống chính hoặc chặn toàn bộ việc upload script là không bao giờ cho phép upload file thực thi (script, code, chương trình) và chỉ cho phép upload đúng loại file cần thiết (ví dụ: hình ảnh `.jpg, .png`, `tài liệu .pdf`) và từ chối tất cả các loại script như: `.php (PHP script)`, `.jsp (Java server page)`, `.asp, .aspx (ASP.NET script)`, `.js (JavaScript)`, `.exe, .sh, .bat (chạy trực tiếp được).`

### 2. Preventing file execution in user-accessible directories() -Lab: Web shell upload via path traversal(Lab: Web Shell Tải lên qua đường dẫn đường dẫn)

Ở bài lab này ta thực hiện các bước đầu tiên như Lab: Web shell upload via Content-Type restriction bypass ở trên.
Tuy nhiên ở đây trang web này lại up load thành công file `shell.php`

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/259ef928-a502-4018-b13d-b2cd47bb39e6" />

Và vì file đã được up load thành công ta thử thực thi xem lệnh `command=ls` xem thử có chạy lệnh không và kết quả là:

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/bd4dc097-7892-4efe-a84e-9445666a7226" />

-> Dù file shell.php đã được up load thành công nhưng vẫn không thể thực thi lệnh trong file vì có thể trang web đã thực thi cơ chế ngăn chặn không cho phép người dùng thực thi file một cách trực tiếp.
* Bước 3: Điều tra sâu bằng công cụ burpsuite:
  Ở bước này ta thấy được file up load thành công nhưng kết quả ở respone chỉ trả về nội dung file được upload:
  <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/619fb396-f421-48f2-928b-53760dc06fbd" />
  
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/f8fbee04-e876-4ac6-9aff-f86cc0e53447" />

* Bước 4: Ở bước này ta có thể kết hợp lỗ hổng Directory traversal với mục đích để đưa file upload tới thư mục khác cho phép thực thi file php, thay đổi tên file thành ../shell.php.
Ta thực hiện thay đổi `filename=shell.php` thành `filename=../shell.php` trong request upload để kiểm tra xem máy chủ có bị lỗ hổng Directory Traversal trong quá trình lưu file hay không.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/e8352b48-c1ae-4c95-bbcb-7f5ffa89de1d" />

Tuy nhiên sau khi thay đổi kết quả ở Respone vẫn như cũ có nghĩa là trang web có cơ chế ngăn chặn đã loại bỏ chuỗi ../. Vì vậy ta có thể bypass cơ chế này với URL encode: `..%2fshell.php` như sau:

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/8784c74f-ad84-495b-96e7-07f0d15a3e0d" />

Ta thay đổi `filename="..%2Fshell.php"` với `..` là thư mục cha và `%2F` thay thế cho ký tự `/` đã URL-encode tức là `../shell.php`. Mục đích thay đổi ở đây để ta tìm được thư mục có thể thực thi được file shell.php. Vì thư mục upload file bình thường `avatars/shell.php` chỉ cho phép tải file nhưng không cho phép thực thi file php vì đã chuẩn hóa cơ chế ngăn chặn các đuôi file nguy hiểm vì vậy ta thực hiện tìm thư mục gốc bằng cách lùi một cấp để ra khỏi thư mục `/avatars/` để vào thư mục cha để có thể chạy file php và ta có thể thực hiện khai thác lệnh trong file shell. Kết quả sau thi thay đổi:
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/c6581025-7e1d-465d-a375-db50d55c1f44" />

Kết quả này ta thấy được sau khi lùi một cấp thì ta tìm ra được thư mục có thể thực thi được file shell.php.

<img width="1446" height="1080" alt="image" src="https://github.com/user-attachments/assets/e1af8a69-407f-4b47-a3fe-df0dcdf630c9" />

Sau khi xác định được thư mục có thể thực thi được file `shell.php` ta lợi dụng điểm đó để thực thi lệnh trong file mã độc để khai thác trang web.

* Ý nghĩa bài lab này là:

  Mặc dù trang web có cơ chế ngăn chặn người dùng tải file độc hại bằng cách giới hạn thư mục lưu trữ (ví dụ: /avatars/) tuy nhiên ứng dụng không chuẩn hóa và kiểm tra kỹ đường dẫn của tên file cũng như không có cơ chế ngăn chặn hoặc kiểm tra nội dung bên trong file. 

Kẻ tấn công có thể lợi dụng lỗ hổng path traversal bằng cách sửa tên file khi upload,ví dụ: `filename=..%2Fshell.php`

Khi đó, file không bị lưu trong /avatars/ mà được ghi trực tiếp vào thư mục gốc của website – nơi PHP có thể được thực thi.
Sau khi upload thành công, kẻ tấn công có thể truy cập file này qua URL và truyền tham số `command` để thực thi lệnh từ xa (RCE) trên server, ví dụ: `https://target/shell.php?command=whoami`

 Để ngăn chặn kiểu tấn công này, cần triển khai các biện pháp bảo vệ sau:

Cần chuẩn hóa đường dẫn trước khi lưu tệp để loại bỏ các chuỗi nguy hiểm như ../, %2F hoặc các dạng mã hóa khác có thể bị kẻ tấn công lợi dụng để truy cập trái phép vào hệ thống tập tin. Điều này đảm bảo rằng tệp được lưu đúng vị trí cho phép và không thể vượt ra ngoài phạm vi thư mục được chỉ định.

Việc lưu tệp ngoài thư mục web root là rất quan trọng, thư mục upload nên nằm ở vị trí mà web server không thể trực tiếp thực thi các tập tin, từ đó ngăn chặn kịch bản tấn công thông qua việc tải lên và chạy các đoạn mã độc hại. Nếu cần hiển thị hoặc cho phép tải xuống tệp, hệ thống nên truy xuất gián tiếp thông qua mã ứng dụng, thay vì cho phép truy cập trực tiếp qua URL.

Bên cạnh đó, khi lưu tệp, nên đổi tên tệp thành chuỗi ngẫu nhiên hoặc sử dụng UUID để tránh trùng lặp hoặc bị đoán tên tệp, đồng thời ẩn thông tin gốc của tệp mà người dùng tải lên. 

Tiếp theo, kiểm tra loại tệp và MIME thực tế là bước bắt buộc để ngăn ngừa tải lên các tệp độc hại. Hệ thống chỉ nên cho phép những định dạng an toàn và cần thiết, chẳng hạn như .jpg, .png, hoặc .pdf, đồng thời từ chối các loại tệp có khả năng thực thi như .php, .jsp, .asp, .exe, hoặc .sh.

Cuối cùng, để tăng thêm lớp bảo vệ, có thể triển khai cơ chế sandbox hoặc quarantine. Mọi tệp tải lên sẽ được đưa vào môi trường cách ly để quét và kiểm tra virus hoặc mã độc trước khi được xử lý hoặc cho phép sử dụng chính thức.

### 3. Lab: Web shell upload via extension blacklist bypass(Lab: Web Shell Tải lên thông qua Bỏ qua danh sách đen mở rộng)
Ở lab này ta thực hiện các bước đầu tiên như lab Remote code execution via web shell upload (LAB: Thực thi mã từ xa thông qua tải lên shell web) ở trên.
Ta thực hiện thay đổi file `meme-meo-4.jpg` thành file `shell.php` và chèn thêm đoạn code này `<?php echo file_get_contents('/home/carlos/secret'); ?>` vào request và sau khi send ta có kết quả như sau:

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/6bba0695-37a2-49b1-8f0b-37150e08ba54" />

Ta thấy được ở trang respone hiển thị thông báo lỗi:
`HTTP/2 403 Forbidden`
`Server: Apache/2.4.41 (Ubuntu)`
`Sorry, php files are not allowed`
`Sorry, there was an error uploading your file.`

Có nghĩa là máy chủ đã chặn việc tải tệp PHP. Điều này thường xảy ra khi website có cơ chế kiểm tra (denylist hoặc allowlist) đối với phần mở rộng file khi upload.

Ta thử các cách bypass trên nhưng đều không hiệu quả. Như vậy khả năng lớn là điều dẫn đến chúng ta có thể ghi đè nội dung các file đã có. Chúng ta nhắm tới file .htaccess - là một file có ở thư mục gốc của các hostting và do apache quản lý, cấp quyền. File .htaccess có thể điều khiển, cấu hình được nhiều yếu tố với đa dạng các thông số, nó có khả năng thay đổi các giá trị được set mặc định của Apache.

Upload một file với tên .htaccess, thay đổi header Content-Type thành giá trị text/plain, nội dung file như sau: `AddType application/x-httpd-php .shell` 

Dòng lệnh trên sẽ tạo ra một ánh xạ cho phép các file có phần mở rộng là .shell có quyền thực thi với Content-Type: `application/x-httpd-php.`
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/731758c7-4fde-4d62-a515-218c3d9c2fd4" />

với các bước thự hiện thay đổi trên ta hiểu được nội dung thay thế `AddType application/x-httpd-php .shell` với mục đích là ra lệnh cho Apache coi mọi tệp có đuôi .shell là file PHP có thể thực thi. Và phía response: mã phản hồi `HTTP/2 200 OK` có nghĩa là Upload thành công đồng thời thông báo `The file avatars/.htaccess has been uploaded.`. Điều này xác nhận server không chặn tệp `.htaccess` và file này đã được lưu trong thư mục upload (/avatars/).

Như vậy, hiện tại chúng ta có thể upload các file với phần mở rộng `.shell` và có thể thực thi các đoạn code tương đương với một file php.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/f814f458-8c97-4092-b6c9-85b81b057238" />

Kết quả sau khi up load file shell.shell thành công và trang web hiển thị:
<img width="1439" height="829" alt="image" src="https://github.com/user-attachments/assets/6a1749df-9235-48bd-9414-4845d5878d85" />

Và sau khi hoàn thành việc cho up load thành công file shell.shell với nội dung php thì mọi thao tác khai thác trang web trở nên dễ dàng hơn.

* Ý nghĩa bài lab này là

Hiểu cách kẻ tấn công có thể khai thác một cơ chế upload yếu kém để thực thi mã độc trên máy chủ dù hệ thống đã cố gắng chặn các file nguy hiểm như .php. Cũng như hiểu rõ cơ chế denylist (blacklist) – nơi hệ thống chỉ chặn một số phần mở rộng phổ biến như .php, nhưng không kiểm soát hết mọi phương thức khai thác. Từ đó, học cách upload file `.htaccess` để thay đổi cấu hình thư mục, cho phép chuyển đổi các phần mở rộng tùy chỉnh như .shell thành file thực thi PHP, rồi triển khai web shell và thực thi mã trực tiếp trên server. Bài lab cũng nhấn mạnh mức độ nguy hiểm khi máy chủ được cấu hình yếu kém, chẳng hạn không giới hạn loại file upload, cho phép `.htaccess` trong thư mục public, và lưu file upload trong thư mục có thể thực thi script, khiến hệ thống dễ dàng bị kiểm soát và khai thác.

Điểm nguy hiểm là:
Trang web có cơ chế chặn nhưng Chỉ chặn .php mà không chặn .htaccess hoặc extension lạ nên hacker vẫn bypass được và dễ dàng thực hiện khai thác.

### 4. Lab: Web shell upload via obfuscated file extension(Web shell tải lên thông qua tiện ích mở rộng tệp obfuscated)

Ở lab này ta thực hiện các bước như ở Lab: Web shell upload via Content-Type restriction bypass (Lab: Web Shell Tải lên thông qua Bỏ qua hạn chế loại nội dung) ở trên.

Sau khi submit file shell.php thì trang web hiển thị nội dung như ảnh:
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/eb3cd407-14f3-413d-b469-7c070ea323aa" />

Vậy có nghĩa là trang web có cơ chế lọc đuôi file. 
Ta thử cách có thể sử dụng ký tự null byte %00 để vượt qua cơ chế black list. Nên ta thực hiện thay đổi tên file `shell.php` thành `shell.php%00.png` để trang web nhận được đuôi .png không nằm trong black list, sau khi xử lý thì các ký tự bắt đầu từ ký tự Null byte được loại bỏ, tên file chỉ còn shell.php có thể thực thi. 

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/fee9ad14-7d92-47fe-87c0-1544846056cf" />

Ta thấy được file shell.php đã được up load thành công trên server. Bước tiếp theo ta thực hiện các bước khai thác như các bài lab trên.





 








