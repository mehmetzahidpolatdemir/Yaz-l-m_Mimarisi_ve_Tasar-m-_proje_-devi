# Yazılım Mimarisi ve Tasarımı Proje Ödevi
Merhabalar Bu benim Yazılım-Mimarisi-ve-Tasarımı Proje ödevim bu ödevimde -> Tasarım Desenleri; • Yaratılış (Yaratımsal), • Yapısal (Yapısal), • Davranışsal (Davranışsal) olmak üzere 3 konuya ayrılıyor benden istenen 2 konu ile ilgili örnek vermek bu projemde boyutunda anlatacağım.

## Yazılım Mimarisi ve Tasarımı
Yazılım Mimarisi ve Tasarımı Dersi  

## Fabrika Metod(Factory Method) Tasarım Deseni
Factory (Fabrika) tasarım deseni, istemci tarafından verilen bilgilere göre nesne oluşumunu soyutlayarak merkezi bir yerden kontrol etmemizi sağlar. Sınıflar, arayüz üzerinden türetilir. Böylece, istemci ile işi yapacak olan nesne birbirinden ayrılarak gevşek bağlılık sağlanmış olur. Oluşturulacak nesnelerden birbirine benzer olanlar aynı arayüzden türetilerek gruplanır. Fabrika deseni, aynı zamanda sistemimizde tanımladığımız soyut sınıflardan örnekler oluşturmamızı sağlar. Fabrika deseni, Java’da en çok kullanılan desenlerden birisidir.
![Image of Class](https://github.com/mehmetzahidpolatdemir/Yaz-l-m_Mimarisi_ve_Tasar-m-_proje_-devi/blob/master/Factory%20Method.jpg?raw=true)

Farklı bir şekilde anlatmak istersek --->

## Fabrika metod tasarım deseni Nedir?

Fabrika metod tasarım deseni, creational tasarım desenlerinden biridir. Bu tasarım deseni bir nesne yaratmak için arayüz sağlar, fakat hangi sınıftan nesne yaratılacağını, alt sınıfların belirlemesine olanak tanır.

## Ne zaman Kullanılır?

Super sınıf ve alt sınıfların olduğu bir uygulamada, alt sınıfların yaratılma işlemini client yani istemci sınıfında yapılmasını engellemek için kullanılır.

## Nasıl Kullanılır?

Üst sınıfta implement edilmemiş bir metod bulunacak. Bu metod alt sınıflar tarafından implement edilecek. Alt sınıfın yaratılacak nesneyi belirleme işlemi, implement edilmemiş bu metod sayesinde gerçekleştirilecektir.

Not: Üst sınıfta implement edilmemiş bir metod bulunacağı için bu sınıfın türü ya abstract tanımlanmalı ya da interface olmalıdır.

## Faydaları Nedir?

1. Birbirine daha az bağımlı(loosely coupled) sınıflar oluşturmaya imkan tanıdığı ve Factory sınıfı ve onun alt sınıflarına nesne yaratma işlemi taşındığı için daha az karmaşık kod yazılır. Böyle bir kodun bakımı ise daha kolay olacaktır.
2. İstemci (Client) kod, sadece Product interface ile ilgilenir ve bu sayede somut(concrete) Product'lar, client kodu değiştirmeden rahatça eklenebilir.

## Gerekenler

Türü abstract veya interface olan bir süper(base) fabrika sınıfı
En az bir tane alt fabrika sınıfı
En az bir tane Product(ürün) sınıfı
Test sınıfı

## Örnek Kullanım Alanları

1. java.util.Calendar#getInstance()
2. java.util.ResourceBundle#getBundle()
3. java.text.NumberFormat#getInstance()
4. java.nio.charset.Charset#forName()


### ----- Şimdi kod ile anlatım yapalım-----


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
# Structural  Tasarım Deseni

## Bridge(Köprü) Yapısal Tasarım Deseni

Bridge (Köprü) tasarım deseni, yapısal tasarım desenlerinden birisidir. Soyutladığımız nesneler ile işi gerçekleyecek somut nesneler arasında köprü kurar. Soyut sınıflar ve işi yapacak sınıfları birbirinden ayırdığı için iki sınıf tipinde yapılcak bir değişiklik birbirini etkilemez. Hangi sınıfın kullanılacağına çalışma zamanında karar verilir. Bu mekanizma sayesinde çalışma alanında, gerçek işi yapan sınıf değiştirilebilir.
![Image of Class](https://github.com/mehmetzahidpolatdemir/Yaz-l-m_Mimarisi_ve_Tasar-m-_proje_-devi/blob/master/Bridge_Tasar%C4%B1m.jpg?raw=true)

Görüldüğü gibi temel olarak 5 yapı bulunmaktadır.

Implemantor arayüzü ile operasyonlar tanımlanır ve ConcreteImplemantor lar bu arayüzden türeyerek operasyonları gerçekleştirir. Abstraction abstract sınıfı ise içinde Implemantor arayüzünden referans barındırarak Implemantor daki operasyonları çalıştırır. RefinedAbstraction ise Abstraction u uygulayan gerçek sınıf veya senaryoya göre sınıflardır. Client ise Abstraction ve Implemantor türlerinden nesneleri üreterek yapıyı kullanır.

Bridge tasarım deseni ile ilgili basit bir örnek uygulama geliştirelim bunu yapmamızın nedeni size uygulama üzerinde anlatarak kavramınızı kolaylaştırmak . Uygulamamızda veri tabanı yapısını ele alalım. Uygulamamız birden fazla veri tabanı desteği veriyor olsun ve execute, connection açma gibi operasyonlar her veri tabanı için farklı olsun. Uygulamamızın class diyagramı aşağıdadır.

![Image of Class](https://github.com/mehmetzahidpolatdemir/Yaz-l-m_Mimarisi_ve_Tasar-m-_proje_-devi/blob/master/BridgeClassDiagram.png?raw=true)

Uygulamamızın kodları aşağıdadır.
//Implementor
abstract class DbImplementor
```java
abstract class DbImplementor
{
    public abstract void Execute(string Sql);
    public abstract void OpenCon(string SqlCon);
}
```
//ConcreteImplementor
```java
class SqlServerImplementor : DbImplementor
{
    public override void Execute(string Sql)
    {
        Console.WriteLine("\"{0}\" - SqlServer işletildi.", Sql);
    }
    public override void OpenCon(string SqlCon)
    {
        Console.WriteLine("\"{0}\" - Sql Server Con. Açıldı.", SqlCon);
    }
}
  
```
//ConcreteImplementor
```java
class OracleImplementor : DbImplementor
{
    public override void Execute(string Sql)
    {
        Console.WriteLine("\"{0}\" - oracle işletildi.", Sql);
    }
    public override void OpenCon(string SqlCon)
    {
        Console.WriteLine("\"{0}\" - oracle Con. Açıldı.", SqlCon);
    }
}
```
//Abstraction
```java
abstract class DbAbstraction
{
    protected DbImplementor implementor;
    public DbAbstraction(DbImplementor imp)
    {
        Implementor = imp;
    }
```
// Property
```java
public DbImplementor Implementor
    {
        set { implementor = value; }
    }
    public abstract void Exec(string Sql);
    public abstract void ConOpen(string ConStr);
}
```
//RefinedAbstraction
```java
class DbRefinedAbstraction : DbAbstraction
{
    public DbRefinedAbstraction(DbImplementor imp)
        : base(imp)
    {
    }
    public override void Exec(string Sql)
    {
        implementor.Execute(Sql);
    }
    public override void ConOpen(string ConStr)
    {
        implementor.OpenCon(ConStr);
    }
}
```
//client
```java
class Program
{
    static void Main(string[] args)
    {
        DbAbstraction absDb = new DbRefinedAbstraction(new SqlServerImplementor());
        absDb.ConOpen("e-ticaret db");
        absDb.Exec("select * from Urun");
        absDb = new DbRefinedAbstraction(new OracleImplementor());
        absDb.ConOpen("e-ticaret db");
        absDb.Exec("select * from Urun");

        Console.ReadKey();
    }
}

```

# Kısaca Şöyle Diyebiliriz --->
Bridge Design Pattern diyor ki; soyutlaşmış (abstract) bir yapıyı, implementasyondan ayır. Böylece bağımsız olarak geliştirilebilir iki yapı elde edersin.

Gelin bu cümleyi yukarıdaki model üzerinde düşünerek iyice bir anlayalım. İmplementasyondan kastettiği en sonda elde edeceğiniz sınıf olacaktır. Diyelim ki bu sınıf, DesktopSalesReport isimli sınıf olsun. Gelelim soyutlaşmış yapıyı belirleme kısmına… Hemen şunu sorarak zihnimizi berraklaştıralım; yukarıdaki modelde WebEmpPerformanceReport ile DesktopSalesReport sınıfları ortak bir atadan türediklerine göre birbirleriyle akrabalar öyle değil mi? Bakın tam bu noktadaki kırılmayı görebiliyor musunuz? Belirttiğim iki sınıf geliştirilebilir bir modelde olabilmesi için akraba olmamalılar. Nitekim Web formatında oluşturulmuş çalışan performans raporu başka bir şey, masaüstü formatında oluşturulmuş satış raporu ise bambaşka.

O zaman şöyle bir tanım yapabilir miyiz? Bu iki sınıf da farklı iki formatta bir rapordur. O halde bakın ne açığa çıktı! Rapor Formatı, bu modelde soyutlaşmış bir yapıdır. Yani, satış ya da çalışan performans raporunu oluştururken, hangi formatta (Masaüstü veya web) kaydetmesi gerektiğini söylemem yeterli olacak. Bu durumu ayarlamak için IReportFormat isminde bir interface oluşturuyorum ve ilgili formatları bu interface’den implemente ediyorum:
