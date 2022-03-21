# Part 1 - Tổng quan về Docker

## 1. Docker là gì ?
Khi nhắc tới Docker, ta sẽ thường đề cập tới 2 điều như:
- Công ty Docker, Inc
- Công nghệ Docker (Docker Technology)

**Docker** được phát triển bởi Docker, Inc vào năm 2013, một công ty công nghệ có trụ sở tại Mỹ. Nó là 1 phần mềm chạy trên Linux hoặc Windows, cho phép bạn dựng, kiểm thử và triển khai ứng dụng 1 cách nhanh chóng. Docker đóng gói phần mềm vào các đơn vị tiêu chuẩn hóa được gọi là container. Bằng cách sử dụng docker, bạn có thể nhanh chóng triển khai và thay đổi quy mô ứng dụng vào bất kỳ môi trường nào và biết chắc rằng mã của bạn sẽ có thể hoạt động được.

`Docker` được đặt tên xuất phát từ cách diễn đạt `dock worker`.

**Docker có 2 phiên bản chính:**
- Docker Community Editon – CE: Là phiên bản miễn phí
- Docker Enterprise – EE: Phiên bản này là phiên bản trả phí, khi sử dụng phiên bản này bạn sẽ có được sự hỗ trợ từ nhà phát hành.

## 2. Chức năng, vai trò của Docker
- Docker cho phép phát triển, di chuyển và chạy các ứng dụng dựa vào công nghệ ảo hóa trong linux
- Tự động triển khai các ứng dụng bên trong các container bằng cách cung cấp thêm một lớp trừu tượng và tự động hóa việc ảo hóa mức (OS)
- Docker có thể được sử dụng trên các hệ điều hành như: Windows, Linux, MacOS.

**Lợi ích của Docker:**
- Docker giúp cho việc vận chuyển phần mềm nhanh hơn trung bình 7 lần so mới người dùng không sử dụng docker
- Nhanh chóng tiển khai, khởi động và di chuyển.
- Bảo mật
- Hỗ trợ APIs để giao tiếp với các container
- Việc triển khai phần mềm, khắc phục sự cố dễ dàng hơn so được đóng vào container nhỏ
- Tiết kiệm tài nguyên và tiền bạc vì nó giúp chạy nhiều phần mềm hơn trên 1 máy chủ giúp tận dụng tối đa tài nguyên.

## 3. Docker Technology
Khi nhắc tới Docker, người ta thường nhắc tới Docker Technology hơn là công ty Docker.

### Một số lưu ý về Docker Technology:

<image src = "../images/01/docker01.png">

#### **Runtime**: 
- Runtime hoạt động ở mức thấp nhất. Chịu trách nhiệm khởi động hay dừng các container. Docker triển khai cấu trúc runtime theo tầng với runtime cấp cao (`containerd`) và runtime cấp thấp (`runc`) hoạt động cùng nhau.
- Runtime cấp thấp (`runc`) là cách triển khai tham chiếu của Open Container Initiative (OCI). Công việc của nó là giao tiếp với hệ điều hành bên dưới để khởi động và dừng các container. Mọi container chạy trên 1 node docker đều có 1 phiên bản `runc` quản lý nó.
- Runtime cấp cao (`containerd`) làm được nhiều thứ hơn với `runc`. Nó quản lý toàn bộ vòng đời của 1 container, bao gồm: 
    - Pulling images
    - Creating network interface
    - Quản lý các `runc` cấp thấp hơn

#### **Deamon**:
Docker deamon (hay còn gọi là dockerd) nằm phía trên containerd và thực hiện các tác vụ cấp cao hơn như: 
- managing images
- managing volumes
- managing networks
- exposing the docker remote API

#### **Orchestration**
Docker cũng có hỗ trợ riêng để quản lý các cluster, node đang chạy docker. Các cluster này gọi là `swarms`. Docker Swarm dễ sử dụng và nhiều công ty đang sử dụng nó trong product. Tuy nhiên mọi người chọn sử dụng kubernets thay vì docker swarm.

## 4. Một số khái niệm khi sử dụng Docker
### 4.1. Dockerfile
- Docker image có thể được tạo ra tự động bằng cách đọc các chỉ dẫn trong Dockerfile
- Dockerfile phải được đặt tên chính xác là `Dockerfile` (chữ `D` viết hoa). Mọi tên khác đều không hợp lệ.

    <image src = "../images/01/docker02.png">

### 4.2. Docker image
- Image trong docker còn được gọi là mirror, nó là 1 đơn vị đóng gói chứa mọi thứ cần thiết để 1 ứng dụng chạy.
- Image docker có thể lấy về từ các image registry, thao tác này được gọi là pulling. Thao tác pulling image sẽ thực hiện tải image về máy chủ docker, nơi docker sử dụng nó để chạy một hoặc nhiều container.
- Image được tạo thành từ nhiều layer xếp chồng lên nhau, bên trong image là 1 hệ điều hành bị cắt giảm và tất cả các phụ thuộc cần thiết để chạy 1 ứng dụng.

    <image src = "../images/01/docker03.png">

### 4.3. Registry
- Docker registry là nơi lưu trữ các docker image với 2 chế độ là **public** và **private**.
- Là nơi cho phép chia sẻ các image template để sử dụng trong quá trình làm việc với Docker.
- Registry phổ biến nhất là Docker Hub, nhưng vẫn tồn tại các registry khác.

    <image src = "../images/01/docker04.png">

### 4.4. Docker container
- Một container được tạo từ một docker image. Ta có thể `create`, `start`, `stop`, `move` hoặc `delete` dựa trên Docker API hoặc Docker CLI.

    <image src = "../images/01/docker05.png">

- Trong mô hình container, hệ điều hành yêu cầu tất cả các tài nguyên phần cứng. Trên hệ điều hành, ta cài đặt container engine là docker. Sau đó, công cụ container sẽ lấy các tài nguyên hệ điều hành và ghép chúng lại thành các cấu trúc riêng biệt được gọi là container.

- Mỗi container bao gồm mọi thứ cần thiết để chạy được nó: code, runtime, system tools, system libraries, setting. Mỗi container như 1 hệ điều hành thực sự, bên trong mỗi container sẽ chạy 1 ứng dụng.
    
    <image src = "../images/01/docker06.png">

- Container thực hiện ảo hóa hệ điều hành để tách biệt và phân bổ tài nguyên cho cho các container.

    <image src = "../images/01/docker07.png">

**Quá trình đưa 1 ứng dụng chạy trong container có thể được mô tả theo các bước dưới đây**
1. Thực hiện code app và cài đặt các phụ thuộc của nó
2. Tạo Dockerfile mô tả ứng dụng, các phụ thuộc và cách để chạy ứng dụng đó
3. Build thành Docker image
4. Push image vào registry (tùy chọn)
5. Chạy container từ image

    <image src = "../images/01/docker08.png">

## 5. Kiến trúc, các thành phần trong Docker
### 5.1. Các thành phần
Docker Engine là ứng dụng dạng Client-Server với các thành phần chính sau đây:
- Server hay còn được gọi là docker daemon chịu trách nhiệm tạo, quản lý các Docker object như: `image`, `containers`, `networks`, `volume`.
- REST API được `docker daemon` sử dụng để cung cấp các api cho client sử dụng để thao tác với docker
- Client là thành phần đầu cuối cung cấp một tập hợp các câu lệnh sử dụng API để người dùng thao tác với Docker. VD: `docker image`, `docker ps`, `docker network`, ..

    <image src = "../images/01/docker09.png">

### 5.2. Kiến trúc Docker
Client sẽ sử dụng Docker REST API để tương tác với Docker daemon.

<image src = "../images/01/docker10.png">

- Docker client sử dụng kiến trúc client-server. Docker client sẽ giao tiếp với Docker daemon các công việc building, running và distributing các Docker container.
- Docker daemon nghe các yêu cầu từ REST API và quản lý các đối tượng Docker như: Containers, Image, Networks và Volume. Một daemon cũng có thể liên lạc với các daemons khác để quản lý Docker services.
- Docker registries để cho các docker image đăng ký lưu trữ qua Docker Hub để bạn hoặc người khác có thể kéo về 1 cách dễ dàng.

## Tham khảo:
- https://hocchudong.com/phan-1-gioi-thieu-tong-quan-ve-docker/

