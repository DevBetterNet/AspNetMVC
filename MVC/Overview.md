# Giới thiệu về MVC



Trước hết cần phải nói MVC là một design pattern có từ rất rất lâu rồi. Chính xác là vào những năm 1978, một nhà khoa học tên Trygve Reenskaug phát minh ra MVC pattern khi ông thăm nhóm Smalltalk ở trung tâm nghiên cứu Xerox Palo Alto.

| ![](C:\code\github\DevBetterNet\AspNetMVC\MVC\assets\220px-Trygve_Reenskaug_(2010).jpg) | ![](C:\code\github\DevBetterNet\AspNetMVC\MVC\assets\MVC-2006.gif) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |

Sau đó nhiều ngôn ngữ lập trình khác như java đã MVC. Mãi đến năm 2008, Microsoft đưa MVC vào .NET framework. 

![](C:\code\github\DevBetterNet\AspNetMVC\MVC\assets\building_mvc_application.jpg)

Và thế là các lập trình viên phải học thêm về MVC. Lúc này các trang tài liệu của Microsoft chỉ mô tả bằng một hình đơn giản. 

![](C:\code\github\DevBetterNet\AspNetMVC\MVC\assets\MVC.png)

MVC viết tắt của M (Model), V (Views), C (Controller). Và tôi sẽ giới thiệu theo trình tự C-> M -> V

Controller: là thành phần nhận sự tương tác của người dùng, sau đó Controller làm việc với Model và trả phản hồi về cho người sử dụng.

Model: là nơi chúng ta thực hiện logic nghiệp vụ của ứng dụng cần phát triển. Bao gồm thao tác với cơ sở dữ liệu và thực hiện nghiệp vụ.

Views: là thành phần có nhiệm vụ hiển thị giao diện cho người sử dụng tương tác.



Vậy là qua định nghĩa khá cơ bản về ba chữ M, V, C thì chúng ta khó mà hình dung được. ASP.NET MVC là gì. Hãy xem thêm hình dưới đây để hiểu hơn. 



 <img src="C:\code\github\DevBetterNet\AspNetMVC\MVC\assets\MVCmoredetail.png" style="zoom:50%;" />

Chúng ta thấy luồng hoạt động sẽ từ User đến Controller rồi Model, rồi View và quay lại với User.









