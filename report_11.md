Trong bài này, chúng ta sẽ cùng tìm hiểu một trang web, các đường dẫn (the routes), và kiến trúc MVC với Ruby on Rails sẽ hoạt động như thế nào nhé.

# 1.Một trang web hoạt động ra sao?

Một trang web bao gồm nhiều tầng như là Ứng dụng, TCP, Internet, các tầng phần cứng, tất cả được kết nối với nhưng. Nhưng cơ bản vẫn hoạt động thông qua giao thức HTTP viết tắt của Hypertext Transfer Protocol, được dùng để truyển tải dữ liệu giữa các Web server và trình duyệt. Giao thức HTTP hoạt động dựa trên request - response trong mô hình client - server. 

Ví dụ, có một trình duyệt web (Firefox chẳng hạn). Người dùng gõ vào thanh địa chỉ, www.facebook.com, và gửi nó đi, đây được gọi là một URL, đóng vai trò như một HTTP request sẽ được gửi tới máy chủ của Facebook. Máy chủ sẽ trả về một HTTP response có chứa dữ liệu, thường là giao diện web của Facebook, dưới dạng HTML.

Người dùng có thể thao tác trên giao diện web, còn ở máy chủ sẽ lưu trữ và trả về các data (ở database), giải quyết các quá trình logic và nhiều thứ khác.

# 2. Kiến trúc MVC và Rails Routes

![alt text](https://www.tutorialsteacher.com/Content/images/mvc/request-handling-in-mvc.png)

*Mô hình kiến trúc MVC*

Sau khi đã tìm hiểu về phương thức hoạt động của một trang Web, chúng ta sẽ tìm hiểu về kiến trúc MVC cũng như Routes trong Rails.

MVC đại diện cho **M**odel, **V**iew, **C**ontroller

Đối với kiến trúc này, mỗi thành phần sẽ có một nhiệm vụ nhất định, hãy cùng tìm hiểu sâu hơn nhé.

## Model

Model trong Rails đóng vai trò là cầu nối giữa Object và Database, ngoài ra còn kiêm các nhiệm vụ xử lý validation, association và các transaction. Có nghĩa là, model sẽ có mối quan hệ chặt chẽ với cơ sở dữ liệu, mỗi model có thể đại diện cho một bảng trong cơ sở dữ liệu. Đối tượng model sẽ có khả năng, lấy, chỉnh sửa, cũng như xóa dữ liệu trong bảng. Các đối tượng model như là một trung gian giữa ứng dụng và cơ sở dữ liệu của chúng ta.

## View

View dùng để thể hiện kết quá trả về, nó có thể được thể hiện theo nhiều loại dữ liệu như PDF, HTML, JSON, etc. Kết quả cuối cùng của một view sẽ là giao diện người dùng (UI), một phần của 'Client'. Hầu hết các trang web hiện nay đều có giao diện là các file được viết theo HTML và trang trí cũng như sắp xếp bằng CSS và JS.

## Controller

Cuối cùng nhưng không kém phần quan trọng, đó là Controller, nó có nhiệm vụ xử lý flow của ứng dụng, thường sẽ là sử dụng các models để tra cứu và xuất dữ liệu, hay đưa ra các quyết định trả data về cho View.

![alt text](https://i.pinimg.com/originals/6e/f1/8d/6ef18dd3444ddb80c86ffb169bbd6e98.png)

*Trên đây là mô hình hoạt động của Rails*

# MVC và Routes trong một ứng dụng Rails

Hình dung chúng ta đang làm việc với một ứng dụng web có chức năng hiển thị những bài viết về các món ăn trên thế giới. Ở vị thế của một người mê ăn uống. Chúng ta sẽ truy cập tới trang web 'www.foodtheworld.com/posts' và thấy một trang web siều đẹp cùng với đó là một list các bài đăng tuyệt vời về thức ăn khắp nơi trên thế giới.

Khi chúng ta gõ URL và nhấn Enter trên trình duyệt, nó gửi một request tới máy chủ. Trên máy chủ, chúng ta có một ứng dụng Rails và Rails Router sẽ có nhiệm vụ kiểm chứng có URL trùng với URL của người dùng gửi lên không. Chúng ta chỉ cần thêm dòng này vào file routes.rb

`resources :posts`

Nó sẽ tạo ra các đường dẫn RESTful cho các bài đăng. Nếu chạy dòng lệnh `rails routes`, nó sẽ hiển thị ra một loạt các đường dẫn đã được tạo

![alt text](https://rei-website-prod.s3.amazonaws.com/uploads/image/image/40/routes-mappings-installfest.png)

Chúng ta có thể thấy các phương thức `GET`, `POST`, `PUT`, hay `DELETE`. Và cách Rails hướng các `PATH` đến đúng **controller** và **action** trong đó.

Ở ví dụ trên, máy chủ sẽ nhận đường dẫn `/posts` với phương thức `GET`, nó sẽ hướng đến PostsController với hành đồng là `index`.

Trong **controller** PostsController chúng ta sử dụng **model** `Post` để lấy tất cả các bài đăng trong cở sở dữ liệu và render vào file **view** `index.html.erb`, là một file HTML nhưng có nhúng thêm, ngôn ngữ Ruby, trả nó về cho người dùng.

`class PostsController < ApplicationController`
  ```
  def index
    @posts = Posts.all
  end
end
``` 

Người dùng tương tác với UI (gửi yêu cầu tới máy chủ), ứng dụng Rails có router quản lý bản đồ các đường dẫn URL đến đúng với controller. Ở controller, chúng ta có thể làm mọi thứ với model, từ lấy dữ liệu, thêm vào, chỉnh sửa hay thậm chí xóa và cuối cùng là render ra một view tới người dùng.

Trên đây là những điều cơ bản cần biết về cấu trúc và cách hoạt đồng của một trang web với Ruby on Rails.

##Link tham khảo:

https://www.learnenough.com/ruby-on-rails-4th-edition-tutorial/beginning#sec-introduction

https://guides.rubyonrails.org/getting_started.html
