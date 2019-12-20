# Yazilim_Mimarisi_ve_Tasarimi_proje_odevi
Merhabalar Bu benim Yazılım-Mimarisi-ve-Tasarımı Proje ödevim bu ödevimde -> Tasarım Desenleri; • Yaratılış (Yaratımsal), • Yapısal (Yapısal), • Davranışsal (Davranışsal) olmak üzere 3 konuya ayrılıyor benden istenen 2 konu ile ilgili örnek vermek bu projemde boyutunda anlatacağım.

## Yazılım Mimarisi ve Tasarımı
Yazılım Mimarisi ve Tasarımı Dersi  

## Fabrika Metod(Factory Method) Tasarım Deseni
Factory (Fabrika) tasarım deseni, istemci tarafından verilen bilgilere göre nesne oluşumunu soyutlayarak merkezi bir yerden kontrol etmemizi sağlar. Sınıflar, arayüz üzerinden türetilir. Böylece, istemci ile işi yapacak olan nesne birbirinden ayrılarak gevşek bağlılık sağlanmış olur. Oluşturulacak nesnelerden birbirine benzer olanlar aynı arayüzden türetilerek gruplanır. Fabrika deseni, aynı zamanda sistemimizde tanımladığımız soyut sınıflardan örnekler oluşturmamızı sağlar. Fabrika deseni, Java’da en çok kullanılan desenlerden birisidir.
![Image of Class](https://github.com/mehmetzahidpolatdemir/Yaz-l-m_Mimarisi_ve_Tasar-m-_proje_-devi/blob/master/Factory%20Method.jpg?raw=true)
Farklı bir şekilde anlatmak istersek --->

Fabrika metod tasarım deseni Nedir?

Fabrika metod tasarım deseni, creational tasarım desenlerinden biridir. Bu tasarım deseni bir nesne yaratmak için arayüz sağlar, fakat hangi sınıftan nesne yaratılacağını, alt sınıfların belirlemesine olanak tanır.

Ne zaman Kullanılır?

Super sınıf ve alt sınıfların olduğu bir uygulamada, alt sınıfların yaratılma işlemini client yani istemci sınıfında yapılmasını engellemek için kullanılır.

Nasıl Kullanılır?

Üst sınıfta implement edilmemiş bir metod bulunacak. Bu metod alt sınıflar tarafından implement edilecek. Alt sınıfın yaratılacak nesneyi belirleme işlemi, implement edilmemiş bu metod sayesinde gerçekleştirilecektir.

Not: Üst sınıfta implement edilmemiş bir metod bulunacağı için bu sınıfın türü ya abstract tanımlanmalı ya da interface olmalıdır.

Faydaları Nedir?

1. Birbirine daha az bağımlı(loosely coupled) sınıflar oluşturmaya imkan tanıdığı ve Factory sınıfı ve onun alt sınıflarına nesne yaratma işlemi taşındığı için daha az karmaşık kod yazılır. Böyle bir kodun bakımı ise daha kolay olacaktır.
2. İstemci (Client) kod, sadece Product interface ile ilgilenir ve bu sayede somut(concrete) Product'lar, client kodu değiştirmeden rahatça eklenebilir.

Gerekenler

Türü abstract veya interface olan bir süper(base) fabrika sınıfı
En az bir tane alt fabrika sınıfı
En az bir tane Product(ürün) sınıfı
Test sınıfı

Örnek Kullanım Alanları

1. java.util.Calendar#getInstance()
2. java.util.ResourceBundle#getBundle()
3. java.text.NumberFormat#getInstance()
4. java.nio.charset.Charset#forName()
----- Şimdi kod ile anlatım yapalım-------

```java
public interface Computer {
    void name();
    void since(int year);
}
```
Neden bu interface’i oluşturduk diye sorarsanız yazının başında da bahsettiğim gibi birbirine benzeyen sınıf kavramından bahsettim bizim örneğimizde de benzerlik durumu bu interface üzerinden belirlenecek.

```java
public class Mac implements Computer {

    @Override
    public void name() {
        System.out.println("Bilgisayarın Markası Mac");
    }

    @Override
    public void since(int year) {
        System.out.println(year + " senesinde alınmış.");
    }

}

}
```
```java
public class Asus implements Computer {

    @Override
    public void name() {
        System.out.println("Bilgisayarın Markası Asus");
    }

    @Override
    public void since(int year) {
        System.out.println(year + " senesinde alınmış.");
    }

}
```
yukarı da gördüğünüz üzere birden fazla bilgisayar sınıfı mevcut fakat bu sınıflar Computer interface’inden kalıtarak bir benzerlik durumu sergiliyorlar.
Gelelim bu sınıfları oluşturacak fabrika sınıfımıza.

```java
public class ComputerFactory {
    public static Computer createComputer(Class aClass) throws IllegalAccessException, InstantiationException {
            return (Computer) aClass.newInstance();
    }
}
```
görüldüğü üzere ComputerFactory sınıfının bir tane static metodu var bu yordam diğer sınıfları oluştururken her seferinde tekrar tekrar oluşturmak yerine statik bir biçimde daha optimize olarak oluşturmaktadır.
Farkettiyseniz metod bir tane Class type parametresi alıyor. Bu parametre hangi sınıfı oluştutmak istediğimizi anlamak için ama fabrika sınıfı hangi sınıfı oluşturduğunu bilmiyor sadece Computer interface’inden türeyen bir sınıf olduğunu biliyor, ki dönüş tipi Computer tipinde.

```java
public class Main {

    public static void main(String[] args) {

        try {
            Asus asus = (Asus) ComputerFactory.createComputer(Asus.class);
            asus.since(1234);
            asus.name();

            Mac mac = (Mac) ComputerFactory.createComputer(Mac.class);
            mac.name();

        } catch (Exception e) {
            e.printStackTrace();
        }

    }
}
```
son olarak main metodumuzda sınıfları oluşturuyoruz createComputer metoduna Class type geçtiğimize dikkat edin, bu kısmı farklı örneklerde farklı varyasyonlar görebilirsiniz.
Özetleyecek olursak bir sınıf oluşturur iken arada bir interface kullanarak kullanacağınız sınıfları kümeleyebilirsiniz, bununla birlikte araya bir factory (fabrika) sınıfı ekleyerek kodunuzu daha soyut bir biçimde daha anlaşılabilir bir biçimde yazabilirsiniz.
