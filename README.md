
[Source](https://developers.google.com/web/tools/chrome-user-experience-report/ "Permalink to Chrome User Experience Report  |  Tools for Web Developers  |  Google Developers")

# Báo cáo trải nghiệm người dùng Chrome 

![][1]

Báo cáo trải nghiệm người dùng Chrome cung cấp chỉ số trải nghiệm người dùng cho cách người dùng Chrome trong thế giới thực trải nghiệm các điểm đến phổ biến trên web.

## Phương pháp luận 

Báo cáo trải nghiệm người dùng Chrome được hỗ trợ bởi việc đo lường số liệu trải nghiệm người dùng chính trên web công cộng, được tổng hợp từ những người dùng đã chọn tham gia đồng bộ hóa lịch sử duyệt web của họ, chưa thiết lập cụm mật khẩu đồng bộ hóa và có bật [báo cáo thống kê sử dụng][2]. Dữ liệu kết quả được cung cấp qua:

1. [PageSpeed Insights][3], cung cấp chỉ số trải nghiệm người dùng cấp URL cho các URL phổ biến được trình thu thập dữ liệu web của Google biết đến.
2. [Public Google BigQuery project][4], tổng hợp các chỉ số trải nghiệm người dùng theo nguồn, tất cả các nguồn được trình thu thập dữ liệu web của Google biết và chia nhỏ trên nhiều khía cạnh được nêu bên dưới.

### Các chỉ số

Chỉ số được cung cấp bởi Báo cáo trải nghiệm người dùng Chrome công khai được lưu trữ trên Google BigQuery được cung cấp bởi các API nền tảng web chuẩn được trình duyệt hiện đại hiển thị và được tổng hợp theo độ phân giải gốc. Chủ sở hữu trang web muốn phân tích chi tiết hơn (phân giải cấp độ URL) và hiểu rõ hơn về hiệu suất trang web của họ và có thể sử dụng cùng một API để thu thập dữ liệu đo lường thực tế chi tiết (RUM) cho trang web của chính họ.

Để được hướng dẫn về chỉ số nào cần theo dõi và tối ưu hóa và các phương pháp hay nhất về cách diễn giải dữ liệu đo lường của người dùng thực, hãy tham khảo tài liệu [tâm điểm hiệu suất người dùng][5] của chúng tôi .

#### First Paint

Được định nghĩa bằng [Paint Timing API][6] và [available in Chrome M60+][7]:

> "First Paint báo cáo thời gian trình duyệt render lần đầu tiên sau khi điều hướng. Điều này không bao gồm background paint mặc định, nhưng bao gồm background paint không mặc định. Đây là thời điểm quan trọng đầu tiên mà các developer quan tâm đến khi tải trang - khi trình duyệt bắt đầu render trang. "."

#### First Contentful Paint

Được định nghĩa bằng [Paint Timing API][8] và [available in Chrome M60+][7]:

> "First Contentful Paint báo cáo thời gian khi trình duyệt render bất kỳ text, hình ảnh nào (bao gồm hình nền ), non-white canva hoặc SVG. Điều này bao gồm text với các webfonts đang chờ xử lý. Đây là lần đầu tiên người dùng có thể bắt đầu thấy nội dung trang."

#### DOMContentLoaded

Được định nghĩa bởi [HTML specification][9]:

> "The DOMContentLoaded báo cáo thời gian khi tài liệu HTML ban đầu đã được tải và phân tích cú pháp hoàn toàn, mà không cần đợi stylesheet, hình ảnh và khung phụ để kết thúc tải." - [MDN][10].

#### onload

Được định nghĩa bởi [HTML specification][11]:

> "Sự kiện tải được kích hoạt khi trang và các tài nguyên phụ thuộc của nó tải xong." - [MDN][12].

### Các khía cạnh

Hiệu suất của nội dung web có thể thay đổi đáng kể dựa trên loại thiết bị, thuộc tính của mạng và các biến khác. Để giúp phân đoạn và hiểu trải nghiệm người dùng trên các phân đoạn chính như vậy, Báo cáo trải nghiệm người dùng Chrome cung cấp các khía cạnh sau.

#### Loại kết nối hiệu quả

Định nghĩa bởi [Network Information API][13] và [available in Chrome M62+][14]:

> "Cung cấp loại kết nối hiệu quả ("slow-2g", "2g", "3g", "4g", or "offline") được xác định bởi các giá trị vòng lặp và băng thông dựa trên các quan sát đo lường của người dùng thực."

#### Loại thiết bị

Phân loại thiết bị thô ("phone", "tablet", or "desktop"),được [kết nối thông qua User-Agent][15].

#### Quốc gia

Vị trí địa lý của người dùng ở cấp quốc gia, được suy ra theo địa chỉ IP của họ. Các quốc gia được xác định theo các code [ISO 3166-1 alpha-2][16] tương ứng.

### Định dạng dữ liệu

Báo cáo được cung cấp qua  [Google BigQuery][17] dưới dạng tập hợp các tập dữ liệu chứa các chỉ số trải nghiệm người dùng được tổng hợp thành độ phân giải gốc. Mỗi tập dữ liệu đại diện cho một quốc gia duy nhất, `country_rs` đại diện dữ liệu trải nghiệm người dùng cho người dùng ở Serbia (`rs` là mã [ISO 31611-1][16] của Serbia). Ngoài ra, có một tập dữ liệu tổng hợp toàn cầu (`all`) thu thập trải nghiệm trên toàn thế giới. Mỗi hàng trong tập dữ liệu chứa bản ghi trải nghiệm người dùng cùng với một nguồn cụ thể, được chia theo các khía cạnh chính.

| ----- |
| Dimension |  
| `origin` |  "https://example.com" |  
| `effective_connection_type.name` |  4G |  
| `form_factor.name` |  "phone" |  
| `first_paint.histogram.start` |  1000 |  
| `first_paint.histogram.end` |  1200 |  
| `first_paint.histogram.density` |  0.123 | 

Ví dụ, bảng bên trên hiển thị một mẫu bản ghi từ báo cáo trải nghiệm người dùng Chrome, chỉ ra rằng 12.3% lượt tải trang có đo lường "first paint time" nằm trong khoảng 1000-1200 milli giây khi tải "http://example.com" trên thiết bị "điện thoại" qua kết nối như "4G". Để đạt các các giá trị tổng hợp trải nghiệm người dùng lần đầu dưới 1200 mili giây, bạn có thể thêm tất cả các bản ghi có giá trị "end" của biểu đồ nhỏ hơn hoặc bằng 1200.

## Bắt đầu

Báo cáo trải nghiệm người dùng Chrome được cung cấp dưới dạng một project công khai trên [Google BigQuery][17]. Để truy cập project, Bạn cần có một tài khoản Google và Google Cloud Project: [tham khảo hướng dẫn từng bước của chúng tôi][18] và [hướng dẫn về cách truy vấn project][19].

## Mẹo phân tích & thực hành tốt nhất 

### Xem xét sự khác biệt về lượng truy cập trên mỗi nguồn

Các số liệu được cung cấp bởi Báo cáo trải nghiệm người dùng Chrome được cung cấp bởi dữ liệu đo lường người dùng thực. Kết quả là, dữ liệu phản ánh cách người dùng thực sự trải nghiệm nguồn truy cập và không giống như thử nghiệm tổng hợp hoặc địa phương nơi thử nghiệm được thực hiện trong điều kiện cố định và mô phỏng, nắm bắt đầy đủ các yếu tố bên ngoài hình thành và đóng góp cho trải nghiệm người dùng cuối cùng.

Ví dụ: sự khác biệt về số lượng người dùng truy cập nguồn cụ thể có thể đóng góp những khác biệt có ý nghĩa cho trải nghiệm người dùng. Nếu trang web thường xuyên được nhiều khách truy cập hơn với các thiết bị hiện đại hơn hoặc thông qua mạng nhanh hơn, kết quả có thể xuất hiện "nhanh" ngay cả khi trang web không được tối ưu hóa tốt. Ngược lại, một trang web được tối ưu hóa tốt thu hút một lượng người dùng rộng hơn hoặc truy cập có số lượng người dùng lớn hơn trên các thiết bị hoặc mạng chậm hơn, có thể xuất hiện "chậm".

Khi thực hiện các so sánh trực tiếp giữa các nguồn, điều quan trọng là phải thống kê và kiểm soát lưu lượng người dùng khác nhau: phân chia theo khía cạnh được cung cấp, ví dụ như là loại thiết bị và loại kết nối, cùng với đó xem xét những yếu tốt bên ngoài như là lượng kết nối, các quốc gia mà từ đó nguồn được truy cập v.v.

### Xem xét sự khác biệt kích thước truy cập giữa các nguồn

Báo cáo trải nghiệm người dùng Chrome tổng hợp dữ liệu cho mỗi nguồn, với các giá trị "mật độ" trên tất cả các biểu đồ khía cạnh-chỉ số tổng hợp với giá trị là "1.0". Điều này cung cấp thông tin chi tiết về phân phối trải nghiệm trên các thứ nguyên chính cho một nguồn duy nhất,

Tuy nhiên, khi tổng hợp dữ liệu từ nhiều nguồn, ví dụ theo ngành hoặc theo khu vực địa lý, hãy cẩn thận với các loại kết luận được rút ra: việc tăng mật độ cho cùng một chỉ số trên nhiều nguồn không tính đến sự khác biệt về lưu lượng tương đối trên nguồn.

Ví dụ: trang web A có thể có mười triệu khách truy cập, trong khi trang web B có mười nghìn. Trong cả hai trường hợp, mật độ biểu đồ cho mỗi nguồn có tổng  là "1.0" và tập dữ liệu không cung cấp bất kỳ số liệu tuyệt đối nào về lưu lượng của nguồn riêng lẻ, hoặc sự khác biệt về kích thước lưu lượng tương đối so với nguồn. Kết quả là, nếu bạn cộng các mật độ từ A và B, và tính trung bình kết quả, bạn sẽ coi chúng là bằng nhau mặc dù A có lưu lượng lớn hơn gấp 1000 lần.
### Xem xét sự khác biệt về truy cập của Chrome

Chrome Báo cáo trải nghiệm người dùng Chrome được hỗ trợ bởi đo lường người dùng thực được tổng hợp từ người dùng Chrome đã chọn tham gia đồng bộ hóa lịch sử duyệt web của họ, chưa thiết lập cụm mật khẩu đồng bộ hóa và đã bật báo cáo thống kê sử dụng.Lưu lượng có thể không đại diện cho phần lớn người dùng trên một nguồn cụ thể và nhiều nguồn có thể có sự khác biệt về lưu lượng. Hơn nữa, dữ liệu này không tính đến người dùng có trình duyệt khác nhau và sự khác biệt trong việc chấp nhận trình duyệt ở các khu vực địa lý khác nhau.

Do đó, hãy cẩn thận với các loại kết luận được rút ra khi nhìn vào mặt cắt ngang của nguồn và khi so sánh nguồn cá nhân: tránh sử dụng so sánh tuyệt đối và xem xét các yếu tố khác được nêu trong các phần ở trên.


  
