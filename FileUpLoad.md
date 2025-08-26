# A. Lý thuyết
## I. Đăt vấn đề
### 1. Giới thiệu lỗ hổng File upload
Chắc hẳn các bạn đều đã quen thuộc với các tính năng thay đổi ảnh đại diện, ảnh bìa trong quá trình hoàn thành hồ sơ cá nhân. Quá trình tải lên một ảnh đại diện chính là đang thực hiện hành động upload file, cụ thể tệp tải lên ở đây là tệp tin dạng hình ảnh. Tải tệp lên là một tính năng cơ bản trong ứng dụng web và di động, cho phép người dùng chuyển tệp từ thiết bị của họ sang bộ nhớ trực tuyến. Tính năng này kết nối giao diện phía máy khách và phần mềm quản lý phía máy chủ, đảm bảo việc truyền tải tài liệu, hình ảnh và video an toàn và liền mạch. Về mặt kỹ thuật, đây là một thành phần nền tảng hỗ trợ các tác vụ như chia sẻ nội dung và quản lý tài liệu, khiến nó trở thành một khía cạnh thiết yếu của phát triển ứng dụng hiện đại. Giống với các chức năng khác, hành động upload file cũng ẩn chứa những mối nguy tới hệ thống. Dạng lỗ hổng này thường được gọi là File upload vulnerabilities.
### 2. Nguyên nhân gây ra lỗ hổng File upload
Lỗ hổng tải tệp lên có thể phát sinh vì nhiều lý do, bao gồm xác thực đầu vào của người dùng không đầy đủ, kiểm tra loại tệp không chính xác, quyền tệp không đủ hoặc thiếu xác thực nội dung.

Kẻ tấn công có thể khai thác những điểm yếu này bằng cách tải lên các tệp hình ảnh đơn giản chứa mã độc hoặc vi-rút, hoặc sử dụng phần mở rộng tệp lừa đảo để tránh bị phát hiện. Điều này có thể dẫn đến việc thực thi các tập lệnh phía máy chủ cho phép thực thi mã từ xa.
### 3. 
