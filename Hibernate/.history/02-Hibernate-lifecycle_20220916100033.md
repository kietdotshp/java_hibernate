# Sơ đồ của Hibernate lifecycle:
<p align="center">
<img width = 500 src="./image/hibernate-lifecycle.png">
</p>

(1) Transient: Trường hợp bạn tạo mới một đối tượng java từ một Entity, đối tượng đó có tình trạng là Transient. Hibernate không biết về sự tồn tại của nó. Nó nằm ngoài sự quản lý của Hibernate.

(2) Persistent: Trường hợp bạn lấy ra đối tượng Entity bằng method get, load hoặc find, bạn có được một đối tượng nó tương ứng với 1 record dưới database. Đối tượng này có trạng thái Persistent. Nó được quản lý bởi Hibernate. Khi đối tượng ở trạng thái persistent, tất cả các thay đổi mà bạn thực hiện đối với đối tượng này sẽ được áp dụng cho các bản ghi và các trường cơ sở dữ liệu tương ứng khi flush session.

(3) Transient -> Persistent: Session gọi một trong các method save, saveOrUpdate, persist, merge sẽ đẩy đối tượng Transient vào sự quản lý của Hibernate và đối tượng này chuyển sang trạng thái Persistent. Tùy tình huống nó sẽ insert hoặc update dữ liệu vào DB.

(4) Persistent -> Detached: Session gọi evict(..) hoặc clear() để đuổi các đối tượng có trạng thái persistent (bền vững) ra khỏi sự quản lý của Hibernate, giờ các đối tượng này sẽ có trạng thái mới là Detached (Bị tách ra).  Nếu nó không được đính (Attached) trở lại, nó sẽ bị bộ gom rác của Java quét đi theo cơ chế thông thường.

(5) Detached -> Persistent: Sử dụng update(..), saveOrUpdate(..), merge(..) sẽ đính trở lại các đối tượng Detached vào lại. Tùy tình huống nó sẽ tạo ra dưới DB câu lệnh update hoặc insert. Các đối tượng sẽ trở về trạng thái Persistent (bền vững).

(6) Persistent -> Removed: Session gọi method remove(..), delete(..) để xóa một bản ghi, đối tượng persistent giờ chuyển sang trạng thái Removed (Đã bị xóa).

HQL không thao tác với bảng trong db mà thao tác với class được ánh xạ với bảng đó trong db

# Thao tác với Hibernate
[Tham khảo](https://gpcoder.com/6548-hibernate-lifecycle/)