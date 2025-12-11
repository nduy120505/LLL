LinkedList+ArrayList
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.List;

public class ListPerformanceTest {

    static final int N = 100000; // Số lượng phần tử: 100.000

    public static void main(String[] args) {
        System.out.println("--- BẮT ĐẦU TEST VỚI " + N + " PHẦN TỬ ---\n");

        // --- Test ArrayList ---
        List<Integer> arrayList = new ArrayList<>();
        long start = System.nanoTime();
        
        // 1. Thêm phần tử vào ArrayList
        for (int i = 0; i < N; i++) {
            arrayList.add(i);
        }
        long endAdd = System.nanoTime();
        
        // 2. Xóa phần tử đầu tiên (index 0) khỏi ArrayList
        while (!arrayList.isEmpty()) {
            arrayList.remove(0);
        }
        long endRemove = System.nanoTime();

        printResult("ArrayList", (endAdd - start), (endRemove - endAdd));


        // --- Test LinkedList ---
        List<Integer> linkedList = new LinkedList<>();
        start = System.nanoTime();

        // 1. Thêm phần tử vào LinkedList
        for (int i = 0; i < N; i++) {
            linkedList.add(i);
        }
        endAdd = System.nanoTime();

        // 2. Xóa phần tử đầu tiên (index 0) khỏi LinkedList
        while (!linkedList.isEmpty()) {
            linkedList.remove(0);
        }
        endRemove = System.nanoTime();

        printResult("LinkedList", (endAdd - start), (endRemove - endAdd));
    }

    // Hàm hỗ trợ in kết quả
    private static void printResult(String type, long addDuration, long removeDuration) {
        System.out.println("Cấu trúc: " + type);
        // Chuyển đổi nanosecond sang millisecond để dễ đọc
        System.out.printf("  - Thời gian thêm %d phần tử: %.2f ms%n", N, addDuration / 1_000_000.0);
        System.out.printf("  - Thời gian xóa (từ đầu) %d phần tử: %.2f ms%n", N, removeDuration / 1_000_000.0);
        System.out.println("------------------------------------------------");
    }
}

HashSet+TreeSet
import java.util.*;

public class SetPerformanceTest {

    static final int N = 100000; // Số lượng phần tử
    static final int RANGE = 200000; // Khoảng giá trị (0 - 200,000)

    public static void main(String[] args) {
        // 1. Tạo tập dữ liệu ngẫu nhiên (dùng chung cho cả 2 để công bằng)
        System.out.println("Đang tạo dữ liệu ngẫu nhiên...");
        int[] data = new int[N];
        Random rand = new Random();
        for (int i = 0; i < N; i++) {
            data[i] = rand.nextInt(RANGE);
        }
        System.out.println("Đã tạo xong 100.000 số nguyên.\n");

        // 2. Test HashSet
        System.out.println("--- TEST HASHSET ---");
        Set<Integer> hashSet = new HashSet<>();
        performTest(hashSet, data);

        System.out.println();

        // 3. Test TreeSet
        System.out.println("--- TEST TREESET ---");
        Set<Integer> treeSet = new TreeSet<>();
        performTest(treeSet, data);
    }

    public static void performTest(Set<Integer> set, int[] data) {
        long start, end;

        // --- Thao tác THÊM (Add) ---
        start = System.nanoTime();
        for (int x : data) {
            set.add(x);
        }
        end = System.nanoTime();
        double addTime = (end - start) / 1_000_000.0;
        System.out.printf("Thời gian thêm %d phần tử: %.2f ms%n", N, addTime);

        // --- Kiểm tra THỨ TỰ LƯU TRỮ ---
        System.out.print("Dữ liệu lưu trữ (10 phần tử đầu): ");
        int count = 0;
        for (Integer i : set) {
            System.out.print(i + " ");
            count++;
            if (count >= 10) break; // Chỉ in 10 số đại diện
        }
        System.out.println("...");

        // --- Thao tác TÌM KIẾM (Contains) ---
        // Tìm lại chính các số trong data để đảm bảo xác suất tìm thấy cao
        start = System.nanoTime();
        for (int x : data) {
            set.contains(x);
        }
        end = System.nanoTime();
        double searchTime = (end - start) / 1_000_000.0;
        System.out.printf("Thời gian kiểm tra tồn tại (contains): %.2f ms%n", searchTime);

        // --- Thao tác XÓA (Remove) ---
        start = System.nanoTime();
        for (int x : data) {
            set.remove(x);
        }
        end = System.nanoTime();
        double removeTime = (end - start) / 1_000_000.0;
        System.out.printf("Thời gian xóa phần tử: %.2f ms%n", removeTime);
    }
}

HashMap+TreeMap
import java.util.*;

public class MapPerformanceTest {

    static final int N = 100000;       // Số lượng phần tử
    static final int KEY_RANGE = 200000; // Khoảng giá trị của Key

    public static void main(String[] args) {
        // 1. Chuẩn bị dữ liệu đầu vào (Dùng chung cho cả 2 Map để công bằng)
        System.out.println("Đang tạo dữ liệu ngẫu nhiên...");
        int[] keys = new int[N];
        int[] values = new int[N];
        Random rand = new Random();
        for (int i = 0; i < N; i++) {
            keys[i] = rand.nextInt(KEY_RANGE); // Key ngẫu nhiên
            values[i] = rand.nextInt(1000);    // Value ngẫu nhiên
        }
        System.out.println("Đã chuẩn bị xong dữ liệu.\n");

        // 2. Test HashMap
        System.out.println("====== TEST HASHMAP ======");
        performTest(new HashMap<>(), keys, values);

        System.out.println();

        // 3. Test TreeMap
        System.out.println("====== TEST TREEMAP ======");
        performTest(new TreeMap<>(), keys, values);
    }

    public static void performTest(Map<Integer, Integer> map, int[] keys, int[] values) {
        long start, end;

        // --- 1. Thao tác THÊM (Put) ---
        start = System.nanoTime();
        for (int i = 0; i < N; i++) {
            map.put(keys[i], values[i]);
        }
        end = System.nanoTime();
        System.out.printf("  - Thời gian thêm (put): %.2f ms%n", (end - start) / 1_000_000.0);

        // --- 2. Kiểm tra THỨ TỰ LƯU TRỮ ---
        System.out.print("  - Thứ tự key (10 phần tử đầu): ");
        int count = 0;
        // Duyệt qua keySet để xem thứ tự
        for (Integer key : map.keySet()) {
            System.out.print(key + " ");
            count++;
            if (count >= 10) break;
        }
        System.out.println("...");

        // --- 3. Thao tác LẤY GIÁ TRỊ (Get) ---
        start = System.nanoTime();
        for (int key : keys) {
            map.get(key);
        }
        end = System.nanoTime();
        System.out.printf("  - Thời gian lấy (get): %.2f ms%n", (end - start) / 1_000_000.0);

        // --- 4. Thao tác KIỂM TRA TỒN TẠI (ContainsKey) ---
        start = System.nanoTime();
        for (int key : keys) {
            map.containsKey(key);
        }
        end = System.nanoTime();
        System.out.printf("  - Thời gian kiểm tra key (containsKey): %.2f ms%n", (end - start) / 1_000_000.0);

        // --- 5. Thao tác XÓA (Remove) ---
        start = System.nanoTime();
        for (int key : keys) {
            map.remove(key);
        }
        end = System.nanoTime();
        System.out.printf("  - Thời gian xóa (remove): %.2f ms%n", (end - start) / 1_000_000.0);
    }
}

Thread
public class ThreadExercise {

    public static void main(String[] args) {
        System.out.println("--- Bắt đầu chương trình ---");

        // --- 1. Tạo Thread 1: Tính tổng từ 1 đến 1000 ---
        Thread thread1 = new Thread(() -> {
            System.out.println("[Thread-1] Đang tính tổng...");
            int sum = 0;
            for (int i = 1; i <= 1000; i++) {
                sum += i;
            }
            System.out.println("-> [Thread-1] Tổng các số từ 1 đến 1000 là: " + sum);
        });

        // --- 2. Tạo Thread 2: Tìm số nguyên tố lớn nhất < 1000 ---
        Thread thread2 = new Thread(() -> {
            System.out.println("[Thread-2] Đang tìm số nguyên tố...");
            int maxPrime = -1;
            
            // Duyệt ngược từ 999 về 2 để tìm số nguyên tố đầu tiên
            for (int i = 999; i >= 2; i--) {
                if (isPrime(i)) {
                    maxPrime = i;
                    break; // Tìm thấy số lớn nhất thì dừng ngay
                }
            }
            System.out.println("-> [Thread-2] Số nguyên tố lớn nhất nhỏ hơn 1000 là: " + maxPrime);
        });

        // --- 3. Khởi chạy 2 Thread ---
        thread1.start();
        thread2.start();
        
        System.out.println("--- Main thread đã gửi lệnh start() ---");
    }

    // Hàm hỗ trợ kiểm tra số nguyên tố
    public static boolean isPrime(int n) {
        if (n < 2) return false;
        // Chỉ cần kiểm tra đến căn bậc 2 của n để tối ưu hiệu năng
        for (int i = 2; i <= Math.sqrt(n); i++) {
            if (n % i == 0) return false;
        }
        return true;
    }
}

Luồng
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;

public class FileIOExercise {

    public static void main(String[] args) {
        String fileName = "raw.txt";
        String myName = "Nguyen Van A"; // Bạn thay tên mình vào đây

        System.out.println("--- BẮT ĐẦU CHƯƠNG TRÌNH ---\n");

        // --- a. Ghi dữ liệu bằng FileOutputStream ---
        // Sử dụng try-with-resources để tự động đóng file (close)
        try (FileOutputStream fos = new FileOutputStream(fileName)) {
            
            // FileOutputStream làm việc với byte, nên cần chuyển String sang byte[]
            byte[] data = myName.getBytes();
            
            fos.write(data);
            
            System.out.println("1. Đã ghi chuỗi \"" + myName + "\" vào file " + fileName);

        } catch (IOException e) {
            System.err.println("Lỗi khi ghi file: " + e.getMessage());
        }

        // --- b. Đọc dữ liệu bằng FileInputStream và In hoa ---
        System.out.print("2. Đọc file và chuyển thành in hoa: ");
        
        try (FileInputStream fis = new FileInputStream(fileName)) {
            
            int i;
            // Đọc từng byte một (byte = -1 nghĩa là hết file)
            while ((i = fis.read()) != -1) {
                // Ép kiểu int sang char để lấy ký tự
                char c = (char) i;
                
                // Chuyển ký tự thành in hoa và in ra màn hình
                System.out.print(Character.toUpperCase(c));
            }
            System.out.println(); // Xuống dòng cho đẹp

        } catch (IOException e) {
            System.err.println("Lỗi khi đọc file: " + e.getMessage());
        }
        
        System.out.println("\n--- KẾT THÚC ---");
    }
}


