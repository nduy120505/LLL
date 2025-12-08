1. Toán tử tích chập trong lọc ảnh hoạt động như thế nào?
Về mặt lý thuyết, toán tử tích chập hoạt động bằng cách trượt một cửa sổ nhỏ (gọi là mặt nạ hoặc kernel) quét qua toàn bộ các điểm ảnh của ảnh gốc. Tại mỗi vị trí, giá trị điểm ảnh mới ở trung tâm cửa sổ được tính bằng tổng của các tích giữa giá trị điểm ảnh gốc và hệ số tương ứng trong mặt nạ. Quá trình này giúp biến đổi tính chất của ảnh như làm mờ hoặc làm sắc nét.

2. Sự khác biệt giữa bộ lọc trung vị (Median) và bộ lọc trung bình (Mean) là gì?
Bộ lọc Trung bình: Là bộ lọc tuyến tính. Nó tính trung bình cộng của các điểm ảnh trong cửa sổ. Nhược điểm là làm nhòe ảnh và mờ các biên (cạnh) của vật thể.
Bộ lọc Trung vị: Là bộ lọc phi tuyến. Nó sắp xếp các giá trị trong cửa sổ và chọn giá trị nằm giữa. Ưu điểm nổi bật là loại bỏ nhiễu muối tiêu cực cực tốt và bảo toàn được độ sắc nét của các biên (cạnh) tốt hơn bộ lọc trung bình.
3. Giá trị cường độ sáng của ảnh phụ thuộc vào những yếu tố nào?
Về mặt vật lý, cường độ sáng tại một điểm ảnh được quyết định bởi hai yếu tố:
Nguồn sáng chiếu tới: Lượng năng lượng ánh sáng chiếu vào vật thể.
Hệ số phản xạ: Đặc tính bề mặt của vật thể quyết định bao nhiêu phần trăm ánh sáng được phản xạ lại mắt người hoặc cảm biến (ví dụ gương phản xạ nhiều, nhung đen phản xạ ít).
4. Giải thuật Otsu chạy bao nhiêu vòng lặp với ảnh mã hoá 8 bits? Giải thích.
Giải thuật sẽ chạy 256 vòng lặp (hoặc 256 lần kiểm tra).
Giải thích: Ảnh 8-bit có các mức xám từ 0 đến 255. Để tìm ngưỡng tối ưu, thuật toán phải thử lần lượt từng giá trị từ 0 đến 255 làm ngưỡng tạm thời, sau đó tính toán phương sai tại mỗi ngưỡng để tìm ra kết quả tốt nhất.
5. Cho ảnh F(x,y), giải thích cách xác định ảnh đầu ra g(x,y) sử dụng bộ lọc trung vị, không sử dụng các biên.
Để tìm giá trị mới cho một điểm ảnh:
Đặt cửa sổ lọc (ví dụ 3x3) có tâm nằm tại điểm ảnh đó.
Lấy tất cả các giá trị điểm ảnh nằm trong cửa sổ.
Sắp xếp các giá trị này theo thứ tự tăng dần hoặc giảm dần.
Lấy giá trị nằm chính giữa dãy số (trung vị) gán cho điểm ảnh đầu ra.
Lưu ý: "Không xử lý biên" nghĩa là ta bỏ qua các điểm ảnh ở viền ngoài cùng của ảnh, nơi mà cửa sổ lọc không thể đặt trọn vẹn vào trong ảnh được.
6. Nêu khái niệm và tác dụng của phép biến đổi âm bản (Negative transformation) trong xử lý ảnh?
Khái niệm: Là kỹ thuật đảo ngược mức xám của ảnh (vùng sáng thành tối, vùng tối thành sáng), tương tự như phim âm bản trong nhiếp ảnh truyền thống.
Tác dụng: Giúp làm nổi bật các chi tiết màu trắng hoặc xám nhạt nằm trên một nền tối rộng lớn, thường được dùng để phân tích ảnh y tế (như phim X-quang).
7. Phương pháp Otsu là một kỹ thuật phân ngưỡng tự động dựa trên Histogram (Lược đồ xám). Hãy nêu ngắn gọn nguyên lý hoạt động của thuật toán Otsu để giải thích tại sao phương pháp này lại tìm được ngưỡng 𝑇 tối ưu để tách ảnh thành hai lớp (Tiền cảnh/Hậu cảnh)?
Phương pháp Otsu là kỹ thuật tìm ngưỡng tự động dựa trên lược đồ xám (Histogram). Nguyên lý cốt lõi là chia ảnh thành hai lớp (nền và vật thể) sao cho sự tách biệt giữa hai lớp này là lớn nhất. Về mặt toán học, nó tìm ngưỡng T sao cho phương sai giữa các lớp (between-class variance) đạt giá trị cực đại. Khi đó, xác suất phân tách sai giữa vật thể và nền là thấp nhất.

8. Nắn chỉnh biến dạng hình học là gì ? Tại sao phải nắn chỉnh biến dạng hình học ?
Khái niệm: Là quá trình khôi phục lại không gian hình học của ảnh về đúng tỷ lệ thực tế thông qua các phép biến đổi toạ độ và nội suy.
Lý do: Ảnh thu được thường bị méo do góc chụp nghiêng, độ cong của ống kính camera hoặc tốc độ di chuyển của vệ tinh. Việc nắn chỉnh là bắt buộc để có thể đo đạc kích thước chính xác hoặc chồng ghép các bản đồ ảnh lên nhau.
9. Nếu một ảnh cần chuyển thành ảnh nhị phân chỉ có 2 thành phần 0 và 1 thì cần làm những gì? Giải thích.
Cần thực hiện kỹ thuật Phân ngưỡng (Thresholding).
Ta chọn một giá trị ngưỡng T cụ thể. Sau đó duyệt qua từng điểm ảnh: nếu giá trị điểm ảnh lớn hơn hoặc bằng T thì gán thành 1 (trắng), nếu nhỏ hơn T thì gán thành 0 (đen). Kết quả là ảnh chỉ còn hai màu đen và trắng.
10. Bạn hiểu thế nào là lấy mẫu? Giải thích nó trong xử lý ảnh?
Lấy mẫu là quá trình chuyển đổi không gian ảnh liên tục thành không gian rời rạc. Một bức ảnh thực tế là liên tục, để đưa vào máy tính, ta phải chia nó thành một lưới các ô vuông nhỏ (các điểm ảnh). Mật độ lấy mẫu càng cao (lưới càng dày) thì độ phân giải không gian của ảnh càng tốt, ảnh càng sắc nét.

11. Tăng cường ảnh là gì? Liệt kê một số phương pháp miền không gian để tăng cường ảnh.
Khái niệm: Là quá trình xử lý làm cho ảnh có chất lượng tốt hơn (theo cảm nhận mắt người) hoặc phù hợp hơn cho các bước xử lý máy tính tiếp theo so với ảnh gốc.
Các phương pháp miền không gian: Biến đổi hàm mũ (Gamma correction), Cân bằng lược đồ xám (Histogram Equalization), Lọc làm trơn (Smoothing), Lọc làm sắc nét (Sharpening).
12. Giải thích quá trình làm mịn ảnh bằng lọc trung vị?
Quá trình này làm mịn ảnh bằng cách loại bỏ các giá trị ngoại lai (outliers). Khi một điểm ảnh bị nhiễu (quá sáng hoặc quá tối so với vùng lân cận), việc sắp xếp và lấy giá trị trung vị sẽ thay thế điểm nhiễu đó bằng một giá trị thực tế hơn từ các điểm xung quanh. Do không dùng phép tính trung bình cộng, nên các cạnh sắc của vật thể không bị san phẳng (làm mờ) mà vẫn giữ được độ sắc nét.

13. Xử lý ảnh là gì ? Hãy nêu hai mô hình biểu diễn ảnh cơ bản?
Khái niệm: Là lĩnh vực sử dụng máy tính và các giải thuật toán học để thao tác trên ảnh số nhằm cải thiện chất lượng hoặc trích xuất thông tin hữu ích.
Hai mô hình:
Mô hình Raster (Ma trận điểm ảnh - phổ biến nhất).
Mô hình Vector (Biểu diễn bằng công thức toán học).
14. Giải thích sự khác nhau giữa phép lọc thông thấp (low-pass filter) và lọc thông cao (high-pass filter) trong xử lý ảnh. Nêu một ứng dụng thực tế của mỗi loại lọc.
Lọc thông thấp (Low-pass): Chỉ cho các thành phần tần số thấp (vùng ảnh thay đổi chậm, đồng màu) đi qua và chặn tần số cao. Kết quả làm ảnh bị mờ đi, mịn hơn. Ứng dụng: Khử nhiễu.
Lọc thông cao (High-pass): Chỉ cho các thành phần tần số cao (vùng thay đổi đột ngột như cạnh, biên) đi qua và chặn tần số thấp. Kết quả làm ảnh nổi bật các đường biên. Ứng dụng: Làm sắc nét ảnh, phát hiện biên.
15. Đầu vào của hệ thống xử lý ảnh là gì?
Đầu vào là một ảnh số (digital image) hoặc tín hiệu thị giác từ cảm biến đã được số hóa thành ma trận hai chiều các con số.

16. Histogram là gì?
Histogram (Lược đồ xám): Là biểu đồ thể hiện sự phân bố tần suất của các mức xám trong ảnh. Nó cho biết có bao nhiêu điểm ảnh ở mỗi mức độ sáng tối khác nhau. Nhìn vào histogram, ta có thể đánh giá được ảnh đang bị quá sáng, quá tối hay có độ tương phản tốt hay không.

17. Nhiễu ảnh do đâu mà có?
Nhiễu xuất hiện do các yếu tố khách quan trong quá trình tạo và truyền ảnh:
Do cảm biến thu nhận (nhiễu nhiệt, nhiễu điện tử).
Do môi trường (ánh sáng yếu, bức xạ).
Do quá trình truyền tín hiệu (nhiễu đường truyền).
18. Sự khác biệt của xử lý ảnh trong miền tần số và xử lý ảnh trong miền không gian.
Miền không gian: Tính toán trực tiếp trên giá trị các điểm ảnh (pixel) của ảnh gốc.
Miền tần số: Chuyển đổi ảnh sang không gian tần số (thường dùng biến đổi Fourier), xử lý trên phổ tần số đó, rồi biến đổi ngược lại về ảnh. Phương pháp này hiệu quả cho các bài toán lọc toàn cục hoặc loại bỏ nhiễu có tính chu kỳ.
19. Nêu sơ đồ tổng quát của một hệ thống xử lý ảnh
Quy trình chuẩn gồm các bước: Thu nhận ảnh $\rightarrow$ Tiền xử lý (Tăng cường/Khôi phục) $\rightarrow$ Phân đoạn ảnh $\rightarrow$ Biểu diễn & Mô tả $\rightarrow$ Nhận dạng & Nội suy.

20. Vấn đề nào trong xử lý ảnh là quan trọng nhất, tại sao.
Phân đoạn ảnh (Segmentation) thường được coi là bước quan trọng và khó nhất.
Lý do: Mục đích cuối cùng của xử lý ảnh thường là để máy tính "hiểu" đối tượng. Nếu khâu phân đoạn (tách đối tượng ra khỏi nền) bị sai, máy tính sẽ nhận diện nhầm đối tượng, dẫn đến tất cả các bước phân tích, đo đạc phía sau đều vô nghĩa.


Code GGE 
// ================== KHỞI TẠO MA TRẬN ẢNH I (8x8) ==================
var I = ee.Array([
  [35, 24, 78, 89, 53, 68, 87, 34],
  [46, 23, 57, 56, 45, 32, 23, 68],
  [143, 15, 123, 46, 56, 45, 67, 88],
  [224, 156, 231, 65, 23, 65, 123, 90],
  [12, 167, 241, 45, 23, 45, 78, 75],
  [124, 25, 47, 88, 36, 75, 12, 25],
  [12, 82, 21, 26, 48, 55, 64, 46],
  [53, 56, 28, 32, 77, 89, 76, 36]
]);

print('Ảnh gốc I', I);

// ======================================================
// CÂU 1 – BIẾN ĐỔI GAMMA: I_gamma = c * I^r
// ======================================================
var c = 1.0;
var r = 0.5;
var I_gamma = I.pow(r).multiply(c);
print('Ảnh sau biến đổi gamma (I_gamma)', I_gamma);

// ======================================================
// CÂU 2 – CÂN BẰNG HISTOGRAM TỰ TÍNH
// ======================================================

var L = 256;
var rows = 8;
var cols = 8;
var N = rows * cols;

// --- Bước 1: "Làm phẳng" và CHUYỂN SANG LIST ---
// ee.Array không map được, phải chuyển sang ee.List
var flatArray = I.reshape([N]); 
var flatList = flatArray.toList(); // Chuyển Array 1D thành List số

// --- Bước 2: Tính histogram ---
var grayLevels = ee.List.sequence(0, L - 1);

var histList = grayLevels.map(function(g) {
  g = ee.Number(g);
  // flatArray.eq(g) trả về mảng 0 và 1. reduce(sum) để đếm số lượng số 1.
  var count = flatArray.eq(g)
              .reduce(ee.Reducer.sum(), [0])
              .get([0]);
  return count;
});

print('Histogram', histList);

// --- Bước 3: PDF ---
var pdfList = histList.map(function(cnt) {
  return ee.Number(cnt).divide(N);
});

// --- Bước 4: CDF (Cộng dồn) ---
var cdfList = ee.List(pdfList).iterate(
  function(val, acc) {
    acc = ee.List(acc);
    val = ee.Number(val);
    var cumPrev = ee.Number(acc.get(-1));
    var cumNew = cumPrev.add(val);
    return acc.add(cumNew);
  },
  ee.List([0])
);
// Bỏ phần tử 0 khởi tạo
cdfList = ee.List(cdfList).slice(1);

// --- Bước 5: Bảng ánh xạ s = round((L-1)*CDF) ---
// index là mức xám cũ, value là mức xám mới
var mappingList = cdfList.map(function(cdf) {
  return ee.Number(cdf).multiply(L - 1).round().int(); 
});

print('Bảng ánh xạ (Mapping List)', mappingList);

// --- Bước 6: Áp dụng ánh xạ cho ảnh I ---

//  Dùng flatList (là ee.List) để map
//  mỗi pixel cũ (v), lấy giá trị tại vị trí v trong mappingList

var I_eq_flat_list = flatList.map(function(v) {
  v = ee.Number(v).int(); // Đảm bảo index là số nguyên
  return mappingList.get(v); // Lấy giá trị mới từ bảng ánh xạ
});

// --- Bước 7: Chuyển List trở lại Ma trận 8x8 ---
var I_eq = ee.Array(I_eq_flat_list).reshape([rows, cols]);

print('Ảnh sau cân bằng histogram (I_eq)', I_eq);

