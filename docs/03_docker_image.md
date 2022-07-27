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

Nơi lưu trữ phổ biến các image là [***Docker Hub***](https://hub.docker.com/).

Registry chứa 1 hoặc nhiều image repositories, trong image repositories chứa 1 hoặc nhiều version image. Như hình sau đây cho thấy cách registry lưu trữ các image.

![](..%5Cimages%5C03%5CScreenshot_2.png)

## 2.5. Docker hub Official and unofficial repositories
Docker Hub có 2 khái niệm là lưu trữ chính thức (official repositories) và lưu trữ không chính thức (unoffical repositories)

`Official repositories` đã được Docker kiểm tra và quản lý. `Unofficical repositories` không được quản lý bởi docker.

Một số `Official repositories`:
```
nginx: https://hub.docker.com/_/nginx/
busybox: https://hub.docker.com/_/busybox/
redis: https://hub.docker.com/_/redis/
mongo: https://hub.docker.com/_/mongo/
```

Một số `Unofficical repositories`:
```
nigelpoulton/tu-demo — https://hub.docker.com/r/nigelpoulton/tu-demo/
nigelpoulton/pluralsight-docker-ci — https://hub.docker.com/r/nigelpoulton/pluralsight-docker-ci/
```

## 2.5. Tên và tag của Docker image
Để pull 1 image từ repo chính thức, ta chỉ cần chỉ ra tên repo và tag như dưới đây:
```
docker image pull <repository>:<tag>
```

Để thêm 1 image từ repo không chính thức, cũng giống như repo chính thức nhưng ta thêm tên của người dùng docker hub hoặc tên của tổ chức .

Ví dụ:
```
docker image pull nigelpoulton/tu-demo:v2
```

Nếu thêm image từ 1 bên thứ 3, ta phải thêm trước kho lưu trữ tên của bên thứ 3 đó.
Ví dụ:
```
docker image pull gcr.io/google-containers/git-sync:v3.1.5
```

## 2.6. Image with multiple tag
Để pull tất cả các image trong 1 repo, sử dụng tùy chọn `-a` vào lệnh `docker image pull`

Ví dụ:
```
docker image pull -a mongo
```
```
root@haidd-u20-docker-68:~# docker image ls | grep mongo
mongo                                                      3           2f21415cb85f   12 months ago   453MB
mongo                                                      3-stretch   27d820d7098b   3 years ago     373MB
mongo                                                      3-jessie    b9406b8a16ec   3 years ago     368MB
mongo                                                      2           1999482cb0a5   5 years ago     391MB
mongo                                                      2.6         1999482cb0a5   5 years ago     391MB
mongo                                                      2.6.12      1999482cb0a5   5 years ago     391MB
mongo                                                      2.4         2affaf1f84e0   6 years ago     342MB
mongo                                                      2.4.14      2affaf1f84e0   6 years ago     342MB
mongo                                                      2.2         8558fe135d54   6 years ago     237MB
mongo                                                      2.2.7       8558fe135d54   6 years ago     237MB
mongo                                                      2.6.11      f36fb0070896   6 years ago     391MB
mongo                                                      2.6.10      54fb6f9984dd   6 years ago     393MB
mongo                                                      2.6.9       0eb5bcb2f408   7 years ago     392MB
mongo                                                      2.4.13      1bc8a1a8ad40   7 years ago     344MB
mongo                                                      2.6.8       f287f6ca320f   7 years ago     393MB
mongo                                                      2.6.7       0fa5e3f671a7   7 years ago     392MB
mongo                                                      2.4.12      ae5e97f89258   7 years ago     345MB
mongo                                                      2.8         4af37f2deb97   7 years ago     225MB
mongo                                                      2.8.0       4af37f2deb97   7 years ago     225MB
mongo                                                      2.8.0-rc5   4af37f2deb97   7 years ago     225MB
mongo                                                      2.8.0-rc4   c732b27ee3d6   7 years ago     224MB
mongo                                                      2.6.6       7632cab977f9   7 years ago     392MB
mongo                                                      2.8.0-rc3   84a5935d697f   7 years ago     224MB
mongo                                                      2.8.0-rc0   afb23b2838b9   7 years ago     224MB
mongo                                                      2.6.5       6e2f39336075   7 years ago     392MB
mongo                                                      2.7         1bc6f44f84be   7 years ago     217MB
mongo                                                      2.7.8       1bc6f44f84be   7 years ago     217MB
mongo                                                      2.7.7       e29d06d58a5e   7 years ago     237MB
mongo                                                      2.4.11      be2b25bde5f5   7 years ago     345MB
mongo                                                      2.6.4       d90d629f1e23   7 years ago     391MB
mongo                                                      2.7.6       18400f87db91   7 years ago     381MB
mongo                                                      2.4.10      9ee0bcea2cbf   7 years ago     345MB
mongo                                                      2.7.5       5f79484e67e9   7 years ago     379MB
mongo                                                      2.6.1       f4eb787e7fd8   7 years ago     748MB
```

## 2.7. Tìm kiếm image trên Docker Hub qua CLI
Lệnh `docker search` cho phép ta tìm kiếm trên Docker Hub từ CLI. 

Ví dụ để tìm các image `alpine` trên Docker Hub:
```
root@haidd-u20-docker-68:~# docker search alpine
NAME                               DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
alpine                             A minimal Docker image based on Alpine Linux…   8739      [OK]
alpine/git                         A  simple git container running in alpine li…   196                  [OK]
alpine/socat                       Run socat command in alpine container           79                   [OK]
alpine/helm                        Auto-trigger docker build for kubernetes hel…   53
alpine/bombardier                  Auto-trigger docker build for bombardier whe…   22
alpine/k8s                         Kubernetes toolbox for EKS (kubectl, helm, i…   19
puppet/puppet-agent-alpine         Puppet Agent as a Docker Image. Based on Alp…   17
alpine/httpie                      Auto-trigger docker build for `httpie` when …   16                   [OK]
docker/desktop-kubernetes          Kubernetes binaries for Desktop. Compiled fr…   12
alpine/terragrunt                  Auto-trigger docker build for terragrunt whe…   12
alpinelinux/docker-cli             Simple and lightweight Alpine Linux image wi…   4
puppet/r10k                        r10k on a Docker image. Based on Alpine         4
alpinelinux/alpine-gitlab-ci       Build Alpine Linux packages with Gitlab CI      3
alpine/curl                                                                        3
alpine/flake8                      Auto-trigger docker build for fake8 via trav…   2
alpine/openssl                                                                     2
grafana/alpine                     Alpine Linux with ca-certificates package in…   1
ibmcom/fhe-toolkit-alpine-amd64    The IBM Fully Homomorphic Encryption (FHE) T…   1
alpinelinux/gitlab-runner-helper   Helper image container gitlab-runner-helper …   1
armswdev/c-hello-world             Simple hello-world C program on Alpine Linux…   0
docker/tutum-test-alpine           Alpine 3.12 image                               0
rancher/alpine-git                                                                 0
ibmcom/fhe-toolkit-alpine-s390x    The IBM Fully Homomorphic Encryption (FHE) T…   0
alpinelinux/alpine-drone-ci        Build Alpine Linux packages with drone CI       0
ibmcom/alpine-helm-s390x                                                           0
```

Nếu chỉ muốn tìm những image chính thức thì thêm option `--filter "is-official=true"`

Ví dụ:
```
docker search alpine --filter "is-official=true"
```

## 2.8. Images và Layers
Images Docker là 1 loạt các layer read-only được kết nối với nhau. Mỗi layer bao gồm 1 hoặc nhiều file.

Thực tế, khi ta pull 1 image, ta sẽ thấy các layer của image đó.

Ví dụ:
```
root@haidd-u20-docker-68:~# docker image pull nigelpoulton/tu-demo:v2
v2: Pulling from nigelpoulton/tu-demo
5843afab3874: Pull complete
2dfaacf7024e: Pull complete
2dbba127c6aa: Pull complete
1a467efa2204: Pull complete
865369a531d5: Pull complete
d2a40eab4219: Pull complete
b7a31967f5c1: Pull complete
2660d2ef4202: Pull complete
05b2eaa6d9c1: Pull complete
Digest: sha256:af111729d35a09fd24c25607ec045184bb8d76e37714dfc2d9e55d13b3ebbc67
Status: Downloaded newer image for nigelpoulton/tu-demo:v2
docker.io/nigelpoulton/tu-demo:v2
```

Mỗi dòng kết thúc bằng `Pull complete` đại diện cho 1 layer đã được pull.

Ngoài ra, ta có thể xem chi tiết các layer bằng cách dùng lệnh `docker image inspect`

```
root@haidd-u20-docker-68:~# docker inspect nigelpoulton/tu-demo:v2
[
    {
        "Id": "sha256:c610c6a385559fe8d8f946704ae08a230ad4bbc1e05ab7dcb7170025a65cbfea",
        "RepoTags": [
            "nigelpoulton/tu-demo:v2"
        ],
        ...    
        },
        "RootFS": {
            "Type": "layers",
            "Layers": [
                "sha256:72e830a4dff5f0d5225cdc0a320e85ab1ce06ea5673acfe8d83a7645cbd0e9cf",
                "sha256:3ac08c726cd3ea8ea51baeb76fe9abe884a095d8ca7e09e0e21b4479c43a51e0",
                "sha256:b4ab05475db3d4e11fb76b9c431ace91fbebaa0226f6f983d727fc909af472eb",
                "sha256:25546d18ffa5e0663cbcb74221421ac9148a9cc3ae81f5b95301da90da01845b",
                "sha256:bb98cc4b4f24e5eddfe98d8cf2bd3dcfc5e713ac0856eb063db6aad6dec6aa02",
                "sha256:747608dbe4cefaa53b4050c48e2e81299ef864c747459522bbc946e0d4ee0040",
                "sha256:1a12de9afb9a8ef0c2077d1fd2b7aa6cbdb73a6db28d874f7f53b23f7a65d094",
                "sha256:961717c6162433bb8e2196b600335a6046fc4131979c06d8c65a185d7b92e8dc",
                "sha256:4a01f3f149a35afe60da09eaca35caa3b8e25942d0dfe13e6058f44f313d9901"
            ]
        },
        "Metadata": {
            "LastTagTime": "0001-01-01T00:00:00Z"
        }
    }
]
```

Docker sử dụng storage driver để chịu trách nhiệm cho việc xếp chồng các layer và trình bày chúng như 1 thế thống nhất. 

Ví dụ về storage driver bao gồm: 
- `AUFS`
- `overlay2`
- `devicemapper`
- `btrfs`
- `zfs`

## 2.9. Sharing image layers
Nhiều image có thể chia sẻ layer, nó dẫn đến hiệu quả về không gian và hiệu suất.

Khi pull image, các dòng kết thúc là Already exists tức là đã tồn tại.

Ví dụ:
```
2.8.0-rc4: Pulling from library/mongo
Image docker.io/library/mongo:2.8.0-rc4 uses outdated schema1 manifest format. Please upgrade to a schema2 image for better future compatibility. More information at https://docs.docker.com/registry/spec/deprecated-schema-v1/
a3ed95caeb02: Pull complete
ee48d0fb051e: Already exists
785429c6e4b2: Already exists
60f811ea05a5: Already exists
30eeb62267ea: Already exists
4a806b90a51b: Already exists
a91900b8023e: Pull complete
8aac0828f4dc: Pull complete
8a77cd9c2154: Pull complete
Digest: sha256:173da3f554052949ce3baec9740fae6e79eda91592029e46f7653aa956289376
```

## 2.10. Pulling images by digest
Sử dụng digests để xem thông tin chi tiết về image:
```
root@haidd-u20-docker-68:~# docker image ls --digests mongo
REPOSITORY   TAG         DIGEST                                                                    IMAGE ID       CREATED         SIZE
mongo        3           sha256:146c1fd999a660e697aac40bc6da842b005c7868232eb0b7d8996c8f3545b05d   2f21415cb85f   12 months ago   453MB
mongo        3-stretch   sha256:0a1d6cd8790b49ed471ed2197f37b3a812c4226962768603b024703f8b74260d   27d820d7098b   3 years ago     373MB
mongo        3-jessie    sha256:c2f6293248cb617bad30db9d2d569ba670ff4c5f9d7ed4764e1db8436fce0673   b9406b8a16ec   3 years ago     368MB
mongo        2           sha256:08e199598f4f874d14b4f90727dade0384b0fcfe8479355ed2cc5391c46e8ece   1999482cb0a5   5 years ago     391MB
mongo        2.6         sha256:08e199598f4f874d14b4f90727dade0384b0fcfe8479355ed2cc5391c46e8ece   1999482cb0a5   5 years ago     391MB
mongo        2.6.12      sha256:08e199598f4f874d14b4f90727dade0384b0fcfe8479355ed2cc5391c46e8ece   1999482cb0a5   5 years ago     391MB

...
```

Từ các giá trị của DIGEST, ta có pull image về như sau:
```
docker image pull mongo@sha256:146c1fd999a660e697aac40bc6da842b005c7868232eb0b7d8996c8f3545b05d
```

## 2.11. Multi-architecture images
Image Docker có thể hỗ trợ nhiều kiến trúc, có nghĩa là 1 image có thể chứa nhiều biến thể cho các kiến trúc khác nhau và đôi khi cho các hệ điều hành khác nhau.

Khi chạy 1 image hỗ trợ multi-architecture, docker sẽ tự động chọn 1 biến thể image phù hợp với hệ điều hành và kiến trúc của máy. Hầu hết các image đều cung cấp nhiều loại kiến trúc khác nhau.

Có nghĩa là 1 image chẳng hạn như `golang` có thể có image cho linux trên `x64`, hoặc các phiên bản khác nhau trên `ARM` và hơn thế nữa. Có nghĩa là khi bạn đứng trên bất kỳ nền tảng hoặc kiến trúc nào và thực hiện pull image, docker sẽ pull image chính xác phù hợp bới nền tảng hoặc kiến trúc đó.

Để làm được điều này, Registry API hỗ trợ 2 cấu trúc: 
- manifest lists
- manifests

![](..%5Cimages%5C03%5CScreenshot_3.png)

Hình trên cho thấy khi ta pull 1 image, nó sẽ dựa vào kiến trúc cpu của máy chủ docker để lựa chọn phiên bản phù hợp. Ta không cần phải chỉ ra rằng ta cần phiên bản `linux x64` hay `windows x64`, chỉ cần chạy các lệnh như bình thường và docker tự xử lý để có được 1 image phù hợp với nền tảng kiến trúc mà máy chủ docker đang chạy.

## 2.12. Xóa image
Khi không còn cần image trên docker của mình nữa, ta có thể xóa image sử dụng docker image rm. Khi xóa nó sẽ xóa tất cả các image và các layer của nó. Tuy nhiên, nếu 1 layer của image chia sẻ cho nhiều image khác thì layer đó sẽ không bị xóa đến khi tất cả các image tham chiếu đến nó bị xóa hết.

Ví dụ:
```
root@haidd-u20-docker-68:~# docker image rm mongo:3-stretch
Untagged: mongo:3-stretch
Untagged: mongo@sha256:0a1d6cd8790b49ed471ed2197f37b3a812c4226962768603b024703f8b74260d
Deleted: sha256:27d820d7098b15b0d6068602829923e6c4b41bcf0ade658ed0c1870c1de92cb8
Deleted: sha256:b1ee229e143880a1d73a1c0b7323d948561be5f61e1ef90375621dfc698f6c59
Deleted: sha256:8b4a1814b5345e4e9b8f2c83a278a2f50b3405f8a459199753b2dc3823d2b789
Deleted: sha256:6f7b7d4ee701d7bb8c98b197a6a04ad4d3fb3fe87e3073d6a3d60596b7961fb0
Deleted: sha256:f4aa99854347737a34b3a541a2a1362046b128dcd1168fb1b3cc789d55553d7b
Deleted: sha256:e373be77356629318055f4088676a04942a597ef66e5fa409d58b6d9216dbb93
Deleted: sha256:b9e28f8c7b5b375b831d835edbddcde369e184db1aa7c3d5e5245441e8b1a5de
Deleted: sha256:97a7562adc7a05b8689d822ff2e1d5cb191dd00c072a5798c81a3b533bc28678
Deleted: sha256:6fd508e0bc51dd486f70cf3d33523241c6c0fc9c2ae72e466f44e295f334b51a
Deleted: sha256:c22e25de1a389ee58fb7d89a4c3c4a5b3998ecefadcd464c51e338784577e0de
Deleted: sha256:5dacd731af1b0386ead06c8b1feff9f65d9e0bdfec032d2cd0bc03690698feda
```

Xóa nhiều image bằng ID của image:
Ví dụ:
```
docker image rm b9406b8a16ec 0fa5e3f671a7
```

Xóa tất cả các image ta sử dụng lệnh sau:
```
docker image rm $(docker image ls -q) -f
```

# 3. Tổng hợp một số lệnh thao tác với Docker image
- `docker image pull`: pull image từ repo 
- `docker image ls`: Liệt kê các image 
- `docker image inspect`: Cung cấp các thông tin của 1 image 
- `docker image rm`: Xóa 1 hoặc nhiều image