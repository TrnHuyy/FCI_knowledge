# Workshop v2

Nội dung: Cloud Testing

- [ ]  Anh muốn xem các ông lớn cloud nó đang **thực hiện cloud testing như nào**
- [x]  **các kĩ thuật test xung quanh**, **apply như nào**,
- [ ]  **best practice**
- [ ]  **đánh giá số liệu** nếu có

Outline:

- Định nghĩa cloud testing, lợi ích
- Phân loại, các công cụ phổ biến
- Một số practice của cloud testing của những cloud lớn như AWS, Azure, GCC
- Đánh giá

## Cloud Testing

### Giới thiệu cloud computing - điện toán đám mây

- Cloud computing là gì?
    
    Cloud computing là một mô hình điện toán cho phép truy cập đến các tài nguyên điện toán (như máy chủ, lưu trữ, cơ sở dữ liệu, mạng, phần mềm và các dịch vụ khác) theo yêu cầu thông qua Internet mà không cần quản lý trực tiếp hoặc tương tác với các nhà cung cấp dịch vụ này
    
- Các loại cloud
    - Private cloud - đám mây riêng tư
        
        Private Cloud là mô hình triển khai mà các dịch vụ và hạ tầng điện toán đám mây được sử dụng riêng bởi một tổ chức. Private cloud có thể được quản lý bởi tổ chức nội bộ hoặc bởi một nhà cung cấp dịch vụ bên ngoài.
        
        Ưu điểm: bảo mật cao, có toàn quyền kiểm soát và tuỳ chỉnh hạ tầng và dịch vụ theo nhu cầu
        
        Nhược điểm: chi phí cao, khả năng mở rộng hạn chế
        
    - Public cloud
        
        Public Cloud là mô hình triển khai mà các dịch vụ và hạ tầng điện toán đám mây được cung cấp bởi các nhà cung cấp dịch vụ đám mây công cộng qua Internet. Tài nguyên trong public cloud được chia sẻ giữa nhiều người dùng hoặc tổ chức khác nhau.
        
        Ưu điểm: chi phí thấp, khả năng mở rộng linh hoạt, dịch vụ toàn diện và đa dạng từ IaaS đến SaaS
        
        Nhược điểm: rủi ro về bảo mật, phụ thuộc vào nhà cung cấp đám mây
        
    - Hybrid cloud - đám mây lai
        
        Hybrid Cloud là sự kết hợp giữa public cloud và private cloud, cho phép các tổ chức chia sẻ dữ liệu và ứng dụng giữa hai môi trường này. Mô hình này tận dụng được lợi thế của cả hai loại cloud.
        
        Ưu điểm: linh hoạt - dùng public cho tác vụ ko nhạy cảm và private cho dịch vụ quan trọng, tối ưu hoá chi phí và tài nguyên
        
        Nhược điểm: quản lý phức tạp, việc di chuyển giữa các đám mây gặp vấn đề bảo mật
        
    - Community cloud - đám mây cộng đồng
        
        Community Cloud là mô hình triển khai trong đó hạ tầng và dịch vụ được chia sẻ giữa nhiều tổ chức có yêu cầu và mục tiêu chung, thường thuộc cùng một ngành hoặc cộng đồng.
        
        Ưu điểm: chia sẻ chi phí, hợp tác và tiêu chuẩn hoá các quy trình và hệ thống
        
        Nhược điểm: quyền kiểm soát hạn chế, bảo mật và quyền riêng tư
        
- Lợi ích và rủi ro khi sử dụng cloud
    - Lợi ích:
        
        Tiết kiệm chi phí, chỉ trả tiền cho những gì sử dụng
        
        Tính linh hoạt và mở rộng, mở rộng nhanh chóng và khả năng phục hồi tốt
        
        Khả năng tiếp cận toàn cầu, truy cập từ bất cứ đâu chỉ cần có Internet
        
        Tăng hiệu suất và hiệu quả, cập nhật liên tục
        
        Tính khả dụng cao với các giải pháp dự phòng và khắc phục sự cố
        
    - Rủi ro:
        
        Bảo mật và quyền riêng tư, có rủi ro mất dữ liệu nếu bảo mật ko đúng cách
        
        Phụ thuộc vào nhà cung cấp
        
        Hiệu suất và kết nối mạng, phụ thuộc vào đường truyền và độ trễ của Internet
        
        Tuân thủ và quản lý, phải đảm bảo tuân thủ quy định về bảo mật và riêng tư, quản lý dữ liệu gặp khó khăn do ở nhiều địa điểm
        
        Khả năng tương thích và tích hợp, có thể dịch vụ cloud ko tương thích với hệ thống
        

### Các loại service trong cloud

- Software as a Service
    
    SaaS cung cấp các ứng dụng phần mềm qua Internet. Người dùng truy cập các ứng dụng này thông qua trình duyệt web mà không cần cài đặt hoặc quản lý phần mềm trên máy tính cá nhân.
    
    Đặc điểm: 
    
    - Các ứng dụng được quản lý và duy trì hoàn toàn bởi nhà cung cấp dịch vụ.
    - Người dùng chỉ cần truy cập và sử dụng ứng dụng thông qua Internet.
- Platform as a Service
    
    PaaS cung cấp một nền tảng cho phép các nhà phát triển xây dựng, triển khai và quản lý ứng dụng mà không phải quản lý cơ sở hạ tầng bên dưới.
    
    Đặc điểm:
    
    - Cung cấp các công cụ và dịch vụ phát triển, triển khai và quản lý ứng dụng.
    - Bao gồm các môi trường runtime, hệ điều hành, cơ sở dữ liệu và máy chủ ứng dụng.
- Infrastructure as a Service
    
    IaaS cung cấp các tài nguyên cơ sở hạ tầng cơ bản như máy chủ, lưu trữ và mạng. Người dùng có thể thuê các tài nguyên này và quản lý chúng tương tự như quản lý hạ tầng vật lý truyền thống.
    
    Đặc điểm:
    
    - Cung cấp máy ảo (VM), lưu trữ, mạng và các tài nguyên cơ sở hạ tầng khác.
    - Người dùng chịu trách nhiệm quản lý hệ điều hành, ứng dụng và dữ liệu chạy trên các tài nguyên này.
- Network as a Service
    
    NaaS cung cấp các dịch vụ mạng qua Internet, cho phép các tổ chức triển khai và quản lý các tài nguyên mạng mà không cần đầu tư vào phần cứng vật lý.
    
    Đặc điểm:
    
    - Cung cấp các dịch vụ mạng như VPN, firewall, và quản lý lưu lượng mạng.
    - Giúp tối ưu hóa và quản lý các tài nguyên mạng một cách linh hoạt và hiệu quả.
- Communications as a Service
    
    CaaS là một mô hình dịch vụ cloud cung cấp các giải pháp truyền thông trên nền tảng đám mây.
    
    Đặc điểm:
    
    - Cung cấp các dịch vụ truyền thông như gọi điện thoại, nhắn tin, hội nghị video, và các dịch vụ khác mà không cần phải đầu tư vào phần cứng hoặc phần mềm riêng lẻ

### Kiểm thử phần mềm

- Software development Process - quy trình phát triển phần mềm
    
     Là một chuỗi các bước có hệ thống được thực hiện để tạo ra phần mềm chất lượng cao. Quy trình này giúp các nhà phát triển tổ chức, lên kế hoạch và quản lý các dự án phát triển phần mềm một cách hiệu quả.
    
    Gồm các giai đoạn chính: Yêu cầu → Thiết kế → Lập trình → Kiểm thử → Triển khai → Bảo trì
    
    Các mô hình phát triển phần mềm phổ biến:
    
    Thác nước, Xoắn ốc, Agile, Scrum…
    
- Software testing giới thiệu
    
     Là quá trình đánh giá và xác minh rằng phần mềm hoặc ứng dụng đáp ứng các yêu cầu và hoạt động như mong đợi.
    
    Mục tiêu của kiểm thử phần mềm là xác định các lỗi (bugs), cải thiện chất lượng phần mềm và đảm bảo rằng phần mềm đáp ứng các yêu cầu đã được xác định.
    
- Software testing lifecycle
    
    Requirement Analysis - Phân tích và hiểu rõ các yêu cầu của phần mềm để xác định phạm vi và chiến lược kiểm thử.
    
    Test Planning - Lên kế hoạch cho các hoạt động kiểm thử, bao gồm xác định chiến lược, nguồn lực, và lịch trình.
    
    Test Design - Tạo các kịch bản kiểm thử và trường hợp kiểm thử dựa trên yêu cầu phần mềm.
    
    Environment setup - Chuẩn bị môi trường kiểm thử, bao gồm cài đặt phần mềm, phần cứng, và cấu hình hệ thống cần thiết.
    
    Test Execution - Thực hiện các trường hợp kiểm thử và ghi nhận kết quả.
    
    Test Cycle Closure - Đánh giá kết quả kiểm thử và chuẩn bị báo cáo tổng kết.
    
- Terminologies - thuật ngữ
    - Dry run
        
        Nó đề cập đến việc thực hiện một bài kiểm tra hoặc một quy trình mà không có đầu vào thực tế hoặc thực hiện trong môi trường không chính thức để xác minh tính đúng đắn và logic của quy trình đó.
        
        Đặc điểm: 
        
        chủ yếu tập trung vào kiểm tra logic
        
        thường thực hiện bằng tay
        
    - Playtest
        
        Nó đề cập đến quá trình thử nghiệm trò chơi để thu thập phản hồi từ người chơi nhằm cải thiện thiết kế, gameplay và trải nghiệm người dùng.
        
        Đặc điểm:
        
        người dùng thực tế, trải nghiệm thực tế
        
        phản hồi chi tiết
        
        liên tục và lặp lại
        
    

### Testing methods

- Static vs Dynamic
    
    Có 2 phương pháp kiểm thử chính:
    
    - Kiểm thử tĩnh - static
    - Kiểm thử động - dynamic
    
    | Đặc điểm | Kiểm thử tĩnh | Kiểm thử động |
    | --- | --- | --- |
    | Thực thi code | Không | Có |
    | Mục tiêu | Phát hiện lỗi trong tài liệu, code | Phát hiện lỗi trong quá trình thực thi |
    | Thời điểm | Giai đoạn sớm của phát triển | Sau khi có phiên bản phần mềm khả dụng |
    | Kỹ thuật  | Đánh giá tài liệu - Reviews và Phân tích tĩnh - Static analysis | Black box testing, White box testing |
    | Công cụ phổ biến | Công cụ phân tích mã như: SonarQube, PMD | Công cụ kiểm thử: Selenium, JUnit |
- White box testing
    
    Là phương pháp kiểm thử phần mềm mà người kiểm thử có hiểu biết về cấu trúc bên trong, mã nguồn và logic của hệ thống. Phương pháp này tập trung vào việc kiểm tra các đường đi trong mã nguồn, các nhánh và điều kiện.
    
    Đặc điểm:
    
    cần có hiểu biết về mã nguồn và cấu trúc bên trong của hệ thống, kiểm tra chi tiết nội bộ và tăng cường độ bao phủ - coverage của mã nguồn
    
    Một số kỹ thuật:
    
    kiểm thử đường đi - path testing
    
    kiểm thử điều kiện - condition testing
    
    kiểm thử dòng dữ liệu - data flow testing
    
    kiểm thử vòng lặp - loop testing
    
- Black box testing
    
    Là phương pháp kiểm thử phần mềm mà không cần biết về cấu trúc bên trong hoặc mã nguồn của hệ thống.
    
    Người kiểm thử tập trung vào việc kiểm tra các chức năng của phần mềm dựa trên các yêu cầu và đặc tả đã định, tập trung vào đầu vào và đầu ra
    
    Một số kỹ thuật: 
    
    kiểm thử chức năng - functional testing
    
    kiểm thử phân vùng tương đương - Equivalence Partitioning
    
    kiểm thử giá trị biên - Boundary Value Testing
    
    kiểm thử đồ thị chuyển trạng thái - State Transition Testing
    
- Grey box testing
    
    Là sự kết hợp giữa Black Box và White Box.
    
    Phương pháp này thường được áp dụng khi người kiểm thử có một số hiểu biết hạn chế về cấu trúc bên trong của ứng dụng nhưng không có quyền truy cập hoặc không cần truy cập đầy đủ vào mã nguồn.
    
    Đặc điểm: kết hợp kỹ thuật của cả 2 kỹ thuật kia, tập trung vào các luồng dữ liệu và chức năng chính
    
    Một số kỹ thuật:
    
    kiểm thử dựa trên ma trận trạng thái - State Transition Testing
    
    kiểm thử vòng lặp - Loop Testing
    
    kiểm thử dựa trên biểu đồ luồng dữ liệu - Data Flow Diagrams Testing
    
    kiểm thử dựa trên sơ đồ lớp - Class Diagram Testing
    
- Visual testing
    
    Là phương pháp kiểm thử phần mềm tập trung vào giao diện người dùng (UI) và trải nghiệm người dùng (UX). 
    
    Mục tiêu chính của phương pháp này là đảm bảo rằng ứng dụng hiển thị đúng cách trên các thiết bị và trình duyệt khác nhau, và rằng các yếu tố giao diện không bị vỡ hoặc sắp xếp sai.
    
    Đặc điểm: kiểm tra giao diện người dùng, phát hiện lỗi giao diện, tự động hoá bằng công cụ so sánh hình ảnh như Applitools, Percy
    
- Sanity testing
    
    Là một loại kiểm thử nông, được thực hiện sau khi nhận được một bản build mới với những thay đổi nhỏ hoặc bug fixes. 
    
    Mục tiêu là xác minh nhanh rằng các chức năng cơ bản của ứng dụng vẫn hoạt động đúng sau các thay đổi đó.
    
    Đặc điểm: xác minh nhanh, không chi tiết, nhanh chóng và tiết kiệm thời gian
    
- Scalability testing
    
    Là quá trình kiểm thử phần mềm để xác định khả năng mở rộng của hệ thống khi tải công việc tăng lên. 
    
    Mục tiêu là đảm bảo rằng hệ thống có thể xử lý tăng trưởng về dữ liệu hoặc người dùng mà không bị giảm hiệu suất
    
    Đặc điểm: kiểm tra khả năng mở rộng, đo lường hiệu suất,  xác định điểm yếu
    
- Security testing
    
    Là quá trình kiểm thử phần mềm để xác định các lỗ hổng bảo mật và đảm bảo rằng dữ liệu và tài nguyên của hệ thống được bảo vệ khỏi các cuộc tấn công.
    
    Đặc điểm: xác định lỗ hổng bảo mật, đánh giá rủi ro
    
- Smoke testing
    
    Là một loại kiểm thử nông và rộng, được thực hiện để đảm bảo rằng các chức năng cơ bản của phần mềm hoạt động đúng trước khi tiến hành kiểm thử chi tiết hơn. 
    
    Mục tiêu là xác định nhanh chóng xem liệu một build phần mềm mới có đáng để tiếp tục kiểm thử hay không.
    
    Đặc điểm: kiểm tra các chức năng quan trọng nhất, thực hiện sớm , phát hiện các vấn đề lớn ngay từ đầu
    
- Stress testing
    
    Là quá trình kiểm thử phần mềm dưới các điều kiện tải công việc cực kỳ cao để xác định giới hạn của hệ thống và xem cách hệ thống phản ứng khi tải vượt quá mức dự kiến.
    
    Đặc điểm: kiểm tra khi tải cao, xác định điểm gãy và khả năng phục hồi
    
- Usability testing
    
    Là quá trình kiểm thử phần mềm để đánh giá mức độ dễ sử dụng và thân thiện với người dùng. Mục tiêu là đảm bảo rằng người dùng có thể sử dụng hệ thống một cách hiệu quả, hiệu suất và thoải mái.
    
    Đặc điểm: tập trung vào người dùng, đánh giá trải nghiệm người dùng, thu thập phản hồi
    
- Volume testing
    
    Là quá trình kiểm thử phần mềm để đánh giá hiệu suất khi xử lý một lượng lớn dữ liệu. Mục tiêu là xác định cách hệ thống hoạt động khi phải xử lý một khối lượng dữ liệu lớn hơn so với mức bình thường.
    
    Đặc điểm: đánh giá khả năng xử lý dữ liệu lớn, phát hiện các vấn đề về hiệu suất
    

### System testing

Là một phương pháp theo dõi và đánh giá hành vi của sản phẩm hoặc hệ thống phần mềm hoàn chỉnh và đã được tích hợp đầy đủ, dựa vào đặc tả và các yêu cầu chức năng đã được xác định trước

System test được thử nghiệm trong hộp đen, tức là chỉ có các tính năng làm việc bên ngoài của phần mềm được đánh giá trong quá trình thử nghiệm này

- Ad Hoc testing
    
    Phương pháp kiểm thử không chính thức và không có kế hoạch trước. Người kiểm thử sử dụng kinh nghiệm và hiểu biết của mình để tìm ra lỗi mà không theo bất kỳ quy trình nào.
    
    Đặc điểm: ko có kế hoạch cụ thể, dựa trên kinh nghiệm, nhanh chóng và linh hoạt
    
- Compability test
    
    Quá trình kiểm thử để đảm bảo rằng phần mềm hoạt động tốt trên các nền tảng, hệ điều hành, trình duyệt, và thiết bị khác nhau.
    
    Đặc điểm: kiểm tra nhiều môi trường, kiểm tra phần mềm hoạt động với các phiên bản cũ/mới hơn của hệ điều hành hoặc phần mềm khác
    
- Exploratory testing
    
    phương pháp kiểm thử mà người kiểm thử đồng thời học về phần mềm và thiết kế các trường hợp kiểm thử khi thực hiện kiểm thử.
    
    Đặc điểm: tự do và linh hoạt, phát hiện lỗi mà các TH kiểm thử chuẩn ko phát hiện
    
- GUI testing
    
    Quá trình kiểm thử giao diện người dùng của phần mềm để đảm bảo rằng nó đáp ứng các tiêu chuẩn thiết kế và dễ sử dụng.
    
    Đặc điểm: kiểm tra yếu tố giao diện, đảm bảo tính nhất quán, dễ sử dụng
    
- Integration testing
    
    Quá trình kiểm thử các module hoặc thành phần riêng lẻ của phần mềm khi chúng được tích hợp lại với nhau để đảm bảo rằng chúng hoạt động đúng khi kết hợp
    
    Đặc điểm: kiểm tra tương tác giữa các thành phần, phát hiện lỗi khi module giao tiếp với nhau
    
- Load testing
    
    Quá trình kiểm thử phần mềm dưới điều kiện tải công việc nặng để xác định cách hệ thống hoạt động khi chịu tải lớn. 
    
    Đặc điểm: kiểm tra hiệu suất dưới tải, khả năng đáp ứng và phát hiện điểm nghẽn
    
- Recovery testing
    
    Quá trình kiểm thử để đảm bảo rằng phần mềm có thể phục hồi từ các sự cố, lỗi hoặc hỏng hóc và trở lại trạng thái hoạt động bình thường.
    
    Đặc điểm: kiểm tra khả năng phục hồi, đảm bảo tính liên tục và kiểm tra quy trình sao lưu và khôi phục
    

### Other software test

- Browser speed test
    
    Quá trình kiểm thử để đánh giá hiệu suất và tốc độ của trình duyệt khi tải và xử lý trang web.
    
    Mục tiêu là đảm bảo rằng trang web tải nhanh và hoạt động mượt mà trên các trình duyệt khác nhau.
    
    Đặc điểm: kiểm tra tốc độ tải trang, đánh giá hiệu suất của các lệnh JavaScript, đo lường thời gian tải của các tài nguyên hình ảnh, CSS
    
- Mobile device testing
    
    Quá trình kiểm thử phần mềm trên các thiết bị di động để đảm bảo rằng nó hoạt động đúng và tối ưu trên các loại thiết bị di động khác nhau, bao gồm cả điện thoại thông minh và máy tính bảng.
    
    Đặc điểm: đa dạng thiết bị, kiểm thử trải nghiệm người dùng nhất quán và kiểm thử hiệu suất ứng dụng trên mobile
    
- Monkey test
    
    Phương pháp kiểm thử phần mềm không có kế hoạch trước và không theo quy trình cụ thể. Người kiểm thử hoặc công cụ kiểm thử tự động sẽ thực hiện các hành động ngẫu nhiên trên phần mềm để tìm ra các lỗi hoặc hành vi bất thường.
    
    Đặc điểm: ngẫu nhiên và ko có kế hoạch, ko cần kiến thức chuyên sâu
    

### Cloud testing

- Introduction
    
    Là một phương pháp kiểm thử phần mềm sử dụng các tài nguyên và cơ sở hạ tầng đám mây (cloud computing) để thực hiện các hoạt động kiểm thử.
    
    Thay vì sử dụng tài nguyên máy tính và phần mềm cục bộ, cloud testing sử dụng các dịch vụ và tài nguyên có sẵn trên môi trường đám mây, giúp tăng khả năng mở rộng, linh hoạt và tiết kiệm chi phí trong quá trình kiểm thử.
    
- Need for cloud testing
    
    Nhu cầu cho việc kiểm thử đám mây phát sinh do nhiều yếu tố, bao gồm sự phát triển không ngừng của lĩnh vực phát triển phần mềm và những lợi ích mà cloud computing mang lại.
    
- Form of cloud testing
    - Testing a SaaS in a cloud
        
        Đây là quá trình kiểm thử một ứng dụng phần mềm dưới dạng Dịch vụ (SaaS - Software as a Service) được triển khai và chạy trên một môi trường đám mây. 
        
        Trong trường hợp này, các chuyên gia kiểm thử thực hiện kiểm thử chức năng, hiệu suất và bảo mật, yêu cầu phi chức năng của ứng dụng SaaS trên cơ sở hạ tầng đám mây.
        
    - Testing of a cloud
        
        Đây là quá trình kiểm thử chính của cơ sở hạ tầng đám mây. 
        
        Trong trường hợp này, các chuyên gia kiểm thử tập trung vào đánh giá và kiểm tra các tính năng, tính sẵn sàng và tính khả dụng của dịch vụ đám mây như mạng, lưu trữ, tính toán và dịch vụ khác.
        
    - Testing inside a cloud
        
        Đây là quá trình kiểm thử ứng dụng và hệ thống được triển khai và chạy trên một môi trường đám mây. 
        
        Trong trường hợp này, các chuyên gia kiểm thử thực hiện các loại kiểm thử khác nhau như kiểm thử tích hợp, kiểm thử hiệu suất và kiểm thử bảo mật trong một môi trường đám mây.
        
        Nhà cung cấp dịch vụ đám mây mới có thể thực hiện loại kiểm thử này
        
    - Testing over clouds
        
        Nó kiểm tra các ứng dụng triển khai trên đám mây trên nhiều đám mây khác nhau, bao gồm các đám mây riêng tư, công cộng và lai dựa trên các yêu cầu và thông số kỹ thuật của dịch vụ ứng dụng cấp hệ thống - 1 ứng dụng nhưng thay các cloud khác nhau để so sánh
        
        Điều này thường được thực hiện bởi các nhà cung cấp hệ thống ứng dụng dựa trên đám mây.
        
- Type of cloud testing
    - Stress test
        
        Kiểm thử nhằm đánh giá sức chịu đựng của hệ thống khi đối mặt với điều kiện làm việc vượt quá giới hạn bình thường, chẳng hạn như tải cao, số lượng người dùng lớn hoặc tình huống không mong muốn.
        
    - Load test
        
        Kiểm thử nhằm đánh giá hiệu suất của hệ thống khi phải xử lý một lượng công việc lớn. Kiểm thử này giúp xác định khả năng của hệ thống để xử lý tải lớn mà không ảnh hưởng đến hiệu suất và thời gian phản hồi.
        
    - Performance test
        
        Kiểm thử hiệu suất nhằm đánh giá hiệu suất của hệ thống trong các điều kiện tiêu chuẩn và tải cao. Mục tiêu của kiểm thử này là đảm bảo rằng hệ thống đáp ứng được yêu cầu về thời gian phản hồi, tải trọng và hiệu suất tổng thể.
        
    - Functional test
        
        Kiểm thử chức năng nhằm đảm bảo rằng phần mềm hoạt động đúng theo các yêu cầu chức năng đã được xác định. Các kịch bản kiểm thử chức năng được thực hiện để kiểm tra tính đúng đắn của các chức năng cụ thể.
        
    - Latency test
        
        Kiểm thử độ trễ nhằm đánh giá thời gian mà hệ thống hoặc ứng dụng phản hồi dưới điều kiện mạng khác nhau. Kiểm thử này giúp đảm bảo rằng ứng dụng hoặc dịch vụ có thể hoạt động hiệu quả trong mọi điều kiện mạng.
        
    - Browser performance test
        
        Kiểm thử hiệu suất trình duyệt nhằm đánh giá hiệu suất của trang web hoặc ứng dụng web trên các trình duyệt khác nhau. Mục tiêu là đảm bảo rằng trang web hoạt động mượt mà và hiệu quả trên mọi nền tảng và trình duyệt.
        
    - Compatibility test
        
        Kiểm thử tương thích nhằm đảm bảo rằng phần mềm hoạt động đúng trên các nền tảng và môi trường khác nhau, bao gồm hệ điều hành, trình duyệt, thiết bị và mạng. Kiểm thử này đảm bảo rằng phần mềm có thể hoạt động đúng trên mọi môi trường sử dụng.
        
- Steps in cloud testing - Cloud testing lifecycle
    
    ![Untitled](Workshop%20v2%20ec17ab850aad48e480f2e54b1af28baa/Untitled.png)
    
    Vòng đời:
    
    - Develop User Scenario: phát triển các kịch bản người dùng
    - Design Test Cases: thiết kế các test case
    - Select Cloud Service Procider: chọn môi trường test, ở đây là chọn nhà cung cấp dịch vụ đám mây
    - Setup Infrastructure: thiết lập cơ sở hạ tầng trên đám mây để test
    - Leverage Cloud Servers: Sử dụng các máy chủ trên đám mây để chạy test
    - Start testing: chyayj test
    - Monitor testing goals: đo lường các mục tiêu thử nghiệm
    - Delivery results: đưa ra kết quả
- Key and tool in cloud testing
    - Key để thành công
    - Tools:
        - BlazeMeter
        - BrowserStack
        - LoadStorm
        - Testsigma
        - Sauce Labs
        - Nessus
        - App Perfect
        - Jenkin Dev@Cloud
        - Visual studio app center
        - AWS Device Farm
- Benefit
    - Tiết kiệm chi phí:
        
        Không cần đầu tư vào cơ sở hạ tầng phần cứng
        
    - Khả năng mở rộng - main benefit
        
        Dễ dàng tăng hoặc giảm tài nguyên kiểm thử theo nhu cầu
        
        Điều này có nghĩa là thử nghiệm có thể được tiến hành trên quy mô lớn, sử dụng nhiều cấu hình và phần cứng khác nhau
        
    - Tính linh hoạt:
        
        Có thể kiểm thử ở bất cứ đâu và vào bất kỳ thời điểm nào
        
    - Hiệu quả:
        
        Tăng tốc độ triển khai và thực hiện các bài kiểm thử nhờ sức mạnh tính toán của đám mây
        
    - Bảo mật:
        
         Cung cấp tính bảo mật và độ tin cậy được cải thiện vì các nhà cung cấp đám mây hàng đầu có các biện pháp bảo mật mạnh mẽ để bảo vệ dữ liệu và ứng dụng của bạn
        
    - Cập nhập công nghệ mới nhất:
        
        Thử nghiệm trên đám mây có thể giúp bạn cập nhật các công nghệ thử nghiệm mới nhất và các phương pháp hay nhất từ các nhà cung cấp đám mây hàng đầu (nhiều công cụ và dịch vụ thử nghiệm có thể giúp bạn tự động hóa và tối ưu hóa quy trình thử nghiệm của mình, đồng thời luôn đi đầu trong đổi mới thử nghiệm)
        
        Bên cạnh đó, có thể dễ dàng áp dụng công nghệ mới nhờ tính linh hoạt của đám mây
        
- Limitation
    - Bảo mật và quản lý rủi ro
    - Phụ thuộc vào kết nối Internet
    - Kiểm soát và quản lý tài nguyên: Cloud testing có thể gặp khó khăn trong việc kiểm soát và quản lý tài nguyên kiểm thử khi sử dụng các dịch vụ đám mây công cộng, đặc biệt là khi cần thay đổi quy mô và cấu hình.
    - Phụ thuộc vào nhà cung cấp dịch vụ đám mây