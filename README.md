# MongoDB-Sharding

I.	Thiết lập Replication
1.	Chuẩn bị Thư mục: Tạo các thư mục dữ liệu riêng biệt cho 3 node
2.	Khởi động Node (Instance): Khởi động 3 instance MongoDB (cổng 27017, 27018, 27019)
  <img width="940" height="501" alt="image" src="https://github.com/user-attachments/assets/b8ff1f12-b9e9-42e5-83ab-cb0c35e52597" />
3.	Khởi tạo Replica Set: Sử dụng mongosh để kết nối vào cổng 27017 và chạy lệnh rs.initiate() để biến node này thành PRIMARY.
   <img width="940" height="481" alt="image" src="https://github.com/user-attachments/assets/539c4793-fbeb-4bc8-a780-b297e63ce144" />
4.	Thêm Node Phụ: Chạy lệnh rs.add() để thêm 2 node còn lại (27018, 27019) vào Replica Set dưới vai trò SECONDARY. Kiểm tra: Xác nhận Replica Set hoạt động ổn định với 1 PRIMARY và 2 SECONDARY
   <img width="940" height="476" alt="image" src="https://github.com/user-attachments/assets/c344d194-e102-4749-bf43-e6ebb406c3b6" />
II. Thiết lập Sharding (Sharded Cluster)
1. Thiết lập Config Servers: Khởi động và khởi tạo một Replica Set mới (cfg_rs) trên các cổng 27020, 27021, 27022 với tùy chọn --configsvr để lưu trữ metadata của Cluster.
   <img width="1892" height="1006" alt="image" src="https://github.com/user-attachments/assets/ef3f0c42-e5a2-4730-8604-27c2562ef04a" />
2. Khởi động Query Router: Khởi động mongos (cổng 27030) và cấu hình nó trỏ đến 3 Config Servers (cfg_rs). mongos là giao diện mà client kết nối.
   <img width="1462" height="747" alt="image" src="https://github.com/user-attachments/assets/f995cf6b-26a8-48ed-8141-1edeebac5d64" />
   <img width="1460" height="325" alt="image" src="https://github.com/user-attachments/assets/64abdbf4-2e0c-4079-bfe8-76affba317e2" />
3. Thêm Shard: Kết nối vào mongos và chạy lệnh sh.addShard() để thêm Replica Set rs0 vào Cluster dưới vai trò Shard.
   <img width="1448" height="671" alt="image" src="https://github.com/user-attachments/assets/414a6b62-70d3-4b9f-a4ac-a1d5ced082ff" />



