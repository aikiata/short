## 介绍

一个使用 Cloudflare Pages 创建的 URL 缩短器

*Demo* : [https://d.131213.xyz/](https://d.131213.xyz/)



### 利用Cloudflare pages部署


1. fork本项目
2. 登录到[Cloudflare](https://dash.cloudflare.com/)控制台.
3. 在帐户主页中，选择`pages`> ` Create a project` > `Connect to Git`
4. 选择你创建的项目存储库，在`Set up builds and deployments`部分中，全部默认即可。
5. 点击`Save and Deploy`，稍等片刻，你的网站就部署好了。
6. 创建D1数据库参考[这里](https://github.com/x-dr/telegraph-Image/blob/main/docs/manage.md)
7. 执行sql命令创建表（在控制台输入框粘贴下面语句执行即可）

```sql
DROP TABLE IF EXISTS links;
CREATE TABLE IF NOT EXISTS links (
  `id` integer PRIMARY KEY NOT NULL,
  `url` text,
  `slug` text,
  `ua` text,
  `ip` text,
  `status` int,
  `create_time` DATE
);
DROP TABLE IF EXISTS logs;
CREATE TABLE IF NOT EXISTS logs (
  `id` integer PRIMARY KEY NOT NULL,
  `url` text ,
  `slug` text,
  `referer` text,
  `ua` text ,
  `ip` text ,
  `create_time` DATE
);

```
8. 选择部署完成short项目，前往后台依次点击`设置`->`函数`->`D1 数据库绑定`->`编辑绑定`->变量名称填写：`DB` 命名空间 `选择你提前创建好的D1` 数据库绑定

9. 重新部署项目，完成。


### API

#### 短链生成

```bash
# POST /create
curl -X POST -H "Content-Type: application/json" -d '{"url":"https://131213.xyz"}' https://d.131213.xyz/create

# 指定slug
curl -X POST -H "Content-Type: application/json" -d '{"url":"https://131213.xyz","slug":"scxs"}' https://d.131213.xyz/create

```



> response:

```json
{
  "slug": "<slug>",
  "link": "http://d.131213.xyz/<slug>"
}
```

====================
TIẾNG VIỆT

## Giới thiệu

Một công cụ rút gọn liên kết sử dụng Cloudflare Pages và D1 SQL Database.

*Demo*: [https://go.bibica.net/](https://go.bibica.net/)

### Triển khai với Cloudflare Pages

1. Fork dự án này.
2. Đăng nhập vào [Cloudflare](https://dash.cloudflare.com/).
3. Trên trang chính của tài khoản, chọn `Workers & Pages` > `Create` > `Pages` > `Connect to Git`.
4. Chọn kho lưu trữ dự án bạn đã tạo, giữ tất cả các tùy chọn mặc định.
5. Nhấn `Save and Deploy`, sau một thời gian ngắn, trang web của bạn sẽ được triển khai.
6. Tạo cơ sở dữ liệu D1 tham khảo [tại đây](https://github.com/x-dr/telegraph-Image/blob/main/docs/manage.md).
7. Thực hiện lệnh SQL để tạo bảng (đi tới tab `Console`, dán các câu lệnh dưới vào hộp đầu vào của bảng điều khiển và `Execute`):

    ```sql
    DROP TABLE IF EXISTS links;
    CREATE TABLE IF NOT EXISTS links (
      `id` integer PRIMARY KEY NOT NULL,
      `url` text,
      `slug` text,
      `ua` text,
      `ip` text,
      `status` int,
      `create_time` DATE
    );
    DROP TABLE IF EXISTS logs;
    CREATE TABLE IF NOT EXISTS logs (
      `id` integer PRIMARY KEY NOT NULL,
      `url` text ,
      `slug` text,
      `referer` text,
      `ua` text ,
      `ip` text ,
      `create_time` DATE
    );
    ```

8. Sau khi triển khai xong dự án rút gọn, vào bảng điều khiển, chọn `Settings` -> `Functions` -> `D1 database bindings` -> `Edit bindings` -> Variable name: `DB`, D1 database `chọn cơ sở dữ liệu D1` bạn đã tạo trước đó.

9. Triển khai lại dự án (có thể edit bất cứ nội dung gì từ dự án trên Github để nó tự đồng bộ lại, hoặc vào `Deployments` > `View details`, sẽ thấy phần `Mange deployment`, chọn Retry deployment để build lại cũng được)
10. Hoàn tất.

### API

#### Tạo liên kết rút gọn

```bash
# POST /create
curl -X POST -H "Content-Type: application/json" -d '{"url":"https://go.bibica.net"}' https://go.bibica.net/create
```
> Nó sẽ tạo ngẫu nhiên các slug

#### Chỉ định slug
```bash
curl -X POST -H "Content-Type: application/json" -d '{"url":"https://dash.cloudflare.com/","slug":"dash-cloudflare"}' https://go.bibica.net/create
```
> Phản hồi:
```json
{
  "slug": "<slug>",
  "link": "http://go.bibica.net/dash-cloudflare"
}
```


