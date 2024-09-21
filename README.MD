# Created by lu0ng

ĐIỀU KIỆN YÊU CẦU ĐỂ SỬ DỤNG : 
3 VM (ubuntu server 20.04) với 4-8GB RAM mỗi máy
Mỗi VM dư ít nhất 15GB Disk trước khi chạy
Cấu hình IP tĩnh cho tất cả các VM trong cụm (Hướng dẫn tại đây)
Ansible (tại VM master trong cụm hoặc ngoài máy thật)

SCRIPT NÀY SẼ LÀM NHỮNG GÌ ?
Hadoop Cluster (3.2.1) - 1 namenode và 2 datanode
Spark 3.4.3 - tại server master
Elasticsearch Cluster - tại cả 3 server
Kibana

CÁC BƯỚC SỬ DỤNG
0: Xác định IP trên các VM của bạn rồi thay thế vào thư mục hosts.ini(IP & PassUser) và setup-full.yml(IP & NameUser)
1: ssh-keygen -t rsa
2: Copy qua 3 VM
 ssh-copy-id <user>@<IP Master>
 ssh-copy-id <user>@<IP Node1>
 ssh-copy-id <user>@<IP Node2>
 3: Chạy lệnh dưới và nhâm nhi 1 cốc CF cho tới khi hoàn tất :V
ansible-playbook -i hosts.ini setup-full.yml

4: tắt shell hiện tại và mở lên 1 shell mới sau đó dùng lệnh
- hdfs namenode -format 
- start-dfs.sh
- start-yarn.sh
- hdfs dfs -mkdir /spark-logs
- spark/sbin/start-history-server.sh

# Chia sẻ nhớ ghi nguồn (lu0ng.online) ! Xin cảm ơn
# Gmail : lvl.music.99@gmail.com