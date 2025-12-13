Cau 1:

import java.time.LocalDate;
import java.util.Scanner;

// Lớp trừu tượng Product
abstract class Product {
    private String name;
    protected float price;
    private String description;
    protected int quantity;

    public Product(String name, float price, String description, int quantity) {
        this.name = name;
        this.price = price;
        this.description = description;
        this.quantity = quantity;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getDescription() {
        return description;
    }

    public void setDescription(String description) {
        this.description = description;
    }

    public void showInfo() {
        System.out.println("Tên sản phẩm: " + name);
        System.out.println("Giá: " + price + " VND");
        System.out.println("Mô tả: " + description);
        System.out.println("Số lượng: " + quantity);
    }
}

// Lớp con Milk kế thừa từ Product
class Milk extends Product {
    private LocalDate expirationDate;

    public Milk(String name, float price, String description, int quantity, LocalDate expirationDate) {
        super(name, price, description, quantity);
        this.expirationDate = expirationDate;
    }

    public void checkExpired() {
        if (expirationDate.isBefore(LocalDate.now())) {
            System.out.println("Sản phẩm đã hết hạn sử dụng!");
        } else {
            System.out.println("Sản phẩm vẫn còn hạn sử dụng.");
        }
    }

    @Override
    public void showInfo() {
        super.showInfo();
        System.out.println("Hạn sử dụng: " + expirationDate);
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Nhập tên sản phẩm: ");
        String name = sc.nextLine();

        System.out.print("Nhập giá: ");
        float price = sc.nextFloat();
        sc.nextLine();

        System.out.print("Nhập mô tả: ");
        String desc = sc.nextLine();

        System.out.print("Nhập số lượng: ");
        int quantity = sc.nextInt();
        sc.nextLine();

        System.out.print("Nhập hạn sử dụng (yyyy-mm-dd): ");
        String dateStr = sc.nextLine();
        LocalDate expDate = LocalDate.parse(dateStr);

        // Tạo đối tượng Milk và hiển thị thông tin
        Milk milk = new Milk(name, price, desc, quantity, expDate);
        System.out.println("Thông tin sản phẩm");
        milk.showInfo();
        System.out.println("Kiểm tra hạn sử dụng");
        milk.checkExpired();

        sc.close();
    }
}


Câu 5
import java.util.*;
import java.util.function.*;
import java.util.stream.*;

class Product {
    String name;
    double price;

    Product(String name, double price) {
        this.name = name;
        this.price = price;
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int N = Integer.parseInt(sc.nextLine());
        List<Product> inputList = new ArrayList<>();

        for (int i = 0; i < N; i++) {
            String[] parts = sc.nextLine().split(" ");
            inputList.add(new Product(parts[0], Double.parseDouble(parts[1])));
        }


        Supplier<List<Product>> supplier = () -> inputList;


        Predicate<Product> priceFilter = p -> p.price >= 100;


        Function<Product, Product> nameToUpper = p -> new Product(p.name.toUpperCase(), p.price);


        Comparator<Product> priceComparator = Comparator.comparingDouble(p -> p.price);


        Consumer<Product> printer = p -> System.out.println(p.name + " " + p.price);


        supplier.get().stream()
            .filter(priceFilter)
            .map(nameToUpper)
            .sorted(priceComparator)
            .forEach(printer);
    }
}
