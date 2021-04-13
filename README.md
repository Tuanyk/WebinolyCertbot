Webinoly sử dụng Nginx và LetsEncrypt Certbot.

Khi thay đổi root path của website, ví dụ, từ /var/www/example.com/htdocs về /var/www/example.com/htdocs/public đối với các website dùng Code Igniter, thì phải setup lại nginx để nó bắt đúng thư mục gốc của website.

/etc/nginx/sites-available/example.com 

Chú ý phần root /var/www/example.com/htdocs đổi lại thành root /var/www/example.com/htdocs/public

Nếu sử dụng SSL, thì chú ý sửa file dưới để tránh trường hợp lỗi renew chứng chỉ SSL:

/etc/letsencrypt/renewal/example.com.conf

Nhớ sử lại như sau:

webroot_path = /var/www/examplle.com/htdocs/public

Đoạn dưới [[webroot_map]] xóa hết cũng ok.

Sau đó, vào terminal remote dưới quyền root, chạy một số lệnh sau:

(Ko rõ chỉ cần lệnh nào, chạy hết thì nó OK -> cứ chạy thôi)

certbot certonly --webroot -w /var/www/example.com/htdocs/public -d example.com -d www.example.com

certbot certonly --webroot -d example.com -d www.example.com

systemctl restart nginx

Check lại thì thấy chứng chỉ ssl đã được renew là ok !!!
