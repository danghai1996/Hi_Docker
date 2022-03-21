# Part 3 - Docker image

# 1. Tổng quan về Docker image
Docker image là 1 đơn vị đóng gói chứa mọi thứ cần thiết để chạy 1 ứng dụng. Nó bao gồm application code, application dependencies, OS contructs. 

Ta có thể lấy docker image từ các registry. Registry phổ biến nhất là Docker Hub, nhưng vẫn tồn tại các registry khác.

Docker image được tạo thành từ nhiều lớp xếp chồng lên nhau và được biểu diễn dưới dạng 1 đối tượng duy nhất. Bên trong image là 1 HĐH bị cắt giảm và tất cả các phụ thuộc cần thiết để chạy ứng dụng.

# 2. Docker image
Docker image được gọi là `build-time`, còn container được gọi là `run-time`

<image src = "../images\03\Screenshot_1.png">

## 2.1. Image và Container
Để bắt đầu 1 hoặc nhiều container từ image, ta có thể sử dụng `docker container run` hoặc `docker service create`. 

Khi bạn bắt đầu container bằng 1 image, 2 phần image và container trở nên phụ thuộc vào nhau và không thể thực hiệnn xóa image nếu vẫn còn container đang sử dụng image đó. Nếu vẫn cố gắng xóa image mà chưa dừng hoặc xóa các container đang sử dụng image đó thì có thể gây ra lỗi.

## 2.2. Docker image are usually small
Mục đích của container là chạy 1 ứng dụng hoặc dịch vụ duy nhất. Có nghĩa là ứng dụng nó chỉ cần code vầ các phụ thuộc của nó để có thể chay, mà không cần các thứ khác. Dẫn đến image tước bỏ tất cả những phần không thiết yếu.

## 2.4. Registry
Docker image được lưu ở 1 nơi tập trung gọi là image registries. Điều này giúp cho việc chia sẻ và truy cập tới image được dễ dàng.

Nơi lưu trữ phổ biến các image là Docker Hub.

