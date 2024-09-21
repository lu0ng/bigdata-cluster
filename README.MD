# Created by lu0ng

ĐIỀU KIỆN YÊU CẦU ĐỂ SỬ DỤNG :

3 VM (ubuntu server 20.04) với 4-8GB RAM mỗi máy

Mỗi VM dư ít nhất 15GB Disk trước khi chạy

Cấu hình IP tĩnh cho tất cả các VM trong cụm (Hướng dẫn tại đây)

Ansible (tại VM master trong cụm hoặc ngoài máy thật)

SCRIPT NÀY SẼ CÀI ĐẶT VÀ CẤU HÌNH
Hadoop Cluster : (3.2.1) - 1 namenode và 2 datanode
Spark (3.4.3)
Elasticsearch Cluster
Kibana

CÁC BƯỚC SỬ DỤNG

0: Xác định IP trên các VM của bạn rồi thay thế vào thư mục hosts.ini(IP & PassUser) và setup-full.yml(IP & NameUser)

<img width="521" alt="Screen Shot 2024-09-22 at 02 16 46" src="https://github.com/user-attachments/assets/e357e77e-8cb5-45b2-b686-ef511822807f">

# Với file setup-full.yml : 1 và 5 thay đổi thành tên user của bạn - 2 là ip master - 3 là ip node 1 - 4 là ip node 2

<img width="528" alt="Screen Shot 2024-09-22 at 02 16 49" src="https://github.com/user-attachments/assets/a10e3697-294b-4e37-8fe4-79ed39232b52">

# Thay đổi phần ansible_host cùng với ảnh bên trên, phần ansible_become_pass thay đổi thành mật khẩu của user đó

1: ssh-keygen -t rsa

2: Copy qua 3 VM
 ssh-copy-id <user>@<IP Master>
 ssh-copy-id <user>@<IP Node1>
 ssh-copy-id <user>@<IP Node2>

 3: Chạy lệnh và nhâm nhi 1 cốc CF cho tới khi hoàn tất :V
ansible-playbook -i hosts.ini setup-full.yml

4: tắt shell hiện tại và mở lên 1 shell mới sau đó dùng lệnh
- hdfs namenode -format 
- start-dfs.sh
- start-yarn.sh
- hdfs dfs -mkdir /spark-logs
- spark/sbin/start-history-server.sh

# Chia sẻ nhớ ghi nguồn ! Xin cảm ơn
# Gmail : lvl.music.99@gmail.com
