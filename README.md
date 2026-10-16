---


---

<hr>
<hr>
<h2 id="báo-cáo-phân-tích-input--output">1. Báo cáo phân tích Input / Output</h2>
<p>Input (văn bản thô):</p>
<ul>
<li>
<p>Thông tin về cảm biến độ ẩm đất loại cũ và loại mới.</p>
</li>
<li>
<p>Các lệnh Terminal dùng để cài đặt thư viện Python.</p>
</li>
<li>
<p>Đoạn code Python đọc độ ẩm và điều khiển máy bơm.</p>
</li>
<li>
<p>Danh sách công việc cần kiểm tra sau khi lắp đặt.</p>
</li>
</ul>
<p>Output (giao diện sau khi render Markdown):</p>
<ul>
<li>
<p>Tiêu đề và các mục được phân cấp rõ ràng.</p>
</li>
<li>
<p>Các lệnh như <code>pip install</code> và tên biến như <code>soil_moisture</code> được hiển thị bằng Inline Code.</p>
</li>
<li>
<p>Code Python được tô màu cú pháp khi trình xem Markdown hỗ trợ.</p>
</li>
<li>
<p>Bảng so sánh hai loại cảm biến dễ đọc.</p>
</li>
<li>
<p>Danh sách công việc có ô đánh dấu để theo dõi tiến độ.</p>
</li>
</ul>
<h2 id="source-code-file-readme.md">2. Source code file <code>README.md</code></h2>
<h1 id="hướng-dẫn-cài-đặt-cảm-biến-độ-ẩm-cho-trang-trại-lan">Hướng dẫn cài đặt cảm biến độ ẩm cho trang trại Lan</h1>
<h2 id="mục-đích">1. Mục đích</h2>
<p>Tài liệu này hướng dẫn cách lắp đặt cảm biến độ ẩm đất, kiểm tra dữ liệu và điều khiển máy bơm nước tự động bằng Python.</p>
<h2 id="chuẩn-bị-thiết-bị">2. Chuẩn bị thiết bị</h2>
<ul>
<li>
<p>Cảm biến độ ẩm đất loại cũ.</p>
</li>
<li>
<p>Cảm biến độ ẩm đất loại mới.</p>
</li>
<li>
<p>Raspberry Pi hoặc thiết bị điều khiển tương thích.</p>
</li>
<li>
<p>Máy bơm nước và mạch điều khiển phù hợp.</p>
</li>
<li>
<p>Dây nối và nguồn điện phù hợp với thiết bị.</p>
</li>
</ul>
<h2 id="cài-đặt-môi-trường">3. Cài đặt môi trường</h2>
<p>Mở Terminal và kiểm tra phiên bản Python bằng lệnh:</p>
<pre><code>python --version
</code></pre>
<p>Cài đặt thư viện điều khiển GPIO bằng lệnh:</p>
<pre><code>python -m pip install gpiozero
</code></pre>
<p>Lưu ý: Cần chọn thêm thư viện đọc cảm biến phù hợp với phần cứng đang sử dụng.</p>
<h2 id="bảng-so-sánh-cảm-biến">4. Bảng so sánh cảm biến</h2>

<table>
<thead>
<tr>
<th align="left">Tiêu chí</th>
<th align="left">Cảm biến loại cũ</th>
<th align="left">Cảm biến loại mới</th>
</tr>
</thead>
<tbody>
<tr>
<td align="left"><strong>Nguyên lý</strong></td>
<td align="left">Điện trở thay đổi theo độ ẩm</td>
<td align="left">Đo điện dung của đất</td>
</tr>
<tr>
<td align="left"><strong>Khả năng chống ăn mòn</strong></td>
<td align="left">Thấp hơn</td>
<td align="left">Thường tốt hơn</td>
</tr>
<tr>
<td align="left"><strong>Độ bền</strong></td>
<td align="left">Dễ bị ảnh hưởng bởi môi trường đất</td>
<td align="left">Thường có tuổi thọ cao hơn</td>
</tr>
<tr>
<td align="left"><strong>Giá thành</strong></td>
<td align="left">Thường rẻ</td>
<td align="left">Thường cao hơn</td>
</tr>
<tr>
<td align="left"><strong>Ứng dụng</strong></td>
<td align="left">Thử nghiệm, mô hình đơn giản</td>
<td align="left">Theo dõi độ ẩm lâu dài</td>
</tr>
</tbody>
</table><p><em>Lưu ý: Đặc điểm thực tế còn phụ thuộc vào mẫu cảm biến cụ thể.</em></p>
<h2 id="code-python-điều-khiển-máy-bơm">5. Code Python điều khiển máy bơm</h2>
<p>Ví dụ dưới đây minh họa cách điều khiển máy bơm dựa trên giá trị độ ẩm. Hàm đọc cảm biến cần được thay bằng hàm tương thích với thiết bị thực tế.</p>
<pre><code>from gpiozero import OutputDevice
from time import sleep
</code></pre><h1 id="chân-gpio-điều-khiển-mạch-máy-bơm">Chân GPIO điều khiển mạch máy bơm</h1>
<p>PUMP_PIN = 17</p>
<h1 id="ngưỡng-độ-ẩm-cần-tưới-">Ngưỡng độ ẩm cần tưới (%)</h1>
<p>MOISTURE_THRESHOLD = 30</p>
<h1 id="khởi-tạo-chân-điều-khiển-máy-bơm">Khởi tạo chân điều khiển máy bơm</h1>
<p>pump = OutputDevice(PUMP_PIN, active_high=True,<br>
initial_value=False)</p>
<p>def read_soil_moisture():<br>
# Thay bằng code đọc cảm biến thực tế.<br>
# Giá trị minh họa: độ ẩm đất 25%.<br>
soil_moisture = 25<br>
return soil_moisture</p>
<p>try:<br>
while True:<br>
soil_moisture = read_soil_moisture()</p>
<pre><code>    print(f"Do am dat: {soil_moisture}%")

    if soil_moisture &amp;lt; MOISTURE_THRESHOLD:
        pump.on()
        print("Dat kho - Bat may bom")
    else:
        pump.off()
        print("Do am du - Tat may bom")

    sleep(5)
</code></pre>
<p>except KeyboardInterrupt:<br>
print(“Da dung chuong trinh”)</p>
<p>finally:<br>
pump.off()<br>
pump.close()<br>
</p>
<p><strong>Giải thích:</strong></p>
<ul>
<li>
<p><code>soil_moisture</code> lưu giá trị độ ẩm đất.</p>
</li>
<li>
<p><code>MOISTURE_THRESHOLD</code> là ngưỡng độ ẩm để quyết định tưới.</p>
</li>
<li>
<p><code>pump.on()</code> bật máy bơm thông qua mạch điều khiển.</p>
</li>
<li>
<p><code>pump.off()</code> tắt máy bơm.</p>
</li>
<li>
<p><code>sleep(5)</code> giúp chương trình kiểm tra độ ẩm sau mỗi 5 giây.</p>
</li>
</ul>
<p>Lưu ý: Đây là code minh họa. Cần thay hàm <code>read_soil_moisture()</code> bằng cách đọc cảm biến thực tế và kiểm tra chân GPIO, mạch điều khiển trước khi vận hành. Không nối máy bơm công suất lớn trực tiếp vào chân GPIO.</p>
<h2 id="task-list-kiểm-tra-thiết-bị">6. Task List kiểm tra thiết bị</h2>
<ul>
<li>
<p>Kiểm tra cảm biến đã được nối đúng chân.</p>
</li>
<li>
<p>Kiểm tra nguồn điện của cảm biến.</p>
</li>
<li>
<p>Kiểm tra mạch điều khiển máy bơm.</p>
</li>
<li>
<p>Cài đặt Python và thư viện cần thiết.</p>
</li>
<li>
<p>Kiểm tra giá trị độ ẩm đọc được.</p>
</li>
<li>
<p>Thử nghiệm bật và tắt máy bơm an toàn.</p>
</li>
<li>
<p>Kiểm tra máy bơm khi đất khô và khi đất đủ ẩm.</p>
</li>
<li>
<p>Lưu code và tài liệu vào GitHub.</p>
</li>
</ul>
<h2 id="lưu-ý-về-ký-tự-escape-trong-markdown">7. Lưu ý về ký tự Escape trong Markdown</h2>
<p>Khi muốn hiển thị ký tự đặc biệt mà không kích hoạt định dạng Markdown, có thể sử dụng dấu gạch chéo ngược <code>\</code>.</p>
<p>Ví dụ:</p>
<ul>
<li>
<p>Viết <code>\*</code> để hiển thị dấu sao <code>*</code> thay vì tạo định dạng in nghiêng.</p>
</li>
<li>
<p>Viết <code>\#</code> để hiển thị dấu <code>#</code> thay vì tạo tiêu đề.</p>
</li>
</ul>
<h2 id="kết-luận">8. Kết luận</h2>
<p>Markdown giúp tài liệu hướng dẫn dễ đọc và dễ quản lý. Inline Code làm nổi bật tên biến và câu lệnh, Code Block giúp trình bày chương trình Python, Table hỗ trợ so sánh cảm biến và Task List giúp kiểm tra tiến độ lắp đặt.</p>

