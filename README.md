## PHP YAZILI 1:2

> Database oluşturma kısımları lazımsa 'dubayok.md' dosyasına ulaşın. !buyuk ihtimalle amiguzelin icinde

#### Database Bağlantısı 
**baglanti.php** dosyası oluşturun devamında içine bunları yazın
```php
<?php
$servername = "localhost"; // MySQL sunucu adı
$username = "root"; // MySQL kullanıcı adı (genelde 'root' olur)
$password = ""; // MySQL şifre (genelde bos olur)
$database = "veritabani_adi"; // Kullanılacak veritabanı adı (olusturdugunuz veritabani adi)

// MySQLi bağlantısı oluşturulması
$conn = new mysqli($servername, $username, $password, $database);

// Bağlantı kontrolü
if ($conn->connect_error) {
    die("Bağlantı hatası: " . $conn->connect_error);
}
?>

```
#### Veri Ekleme !!!Fotografsiz!!!
**index.php** dosyasinin form kismi:
```html
<form action="ekle.php" method="post">
  <label for="ad">Ad:</label> 
  <input type="text" id="ad" name="ad" required>
    <br>
  <label for="soyad">Soyad:</label>
  <input type="text" id="soyad" name="soyad" required>
   <br>  
  <label for="email">E-Posta:</label>  
  <input type="email" id="email" name="email" required>  
  <br>  
  <input type="submit" value="Gönder">  
</form>
```


**ekle.php** dosyasinin icerigi:
```php
<?php
// Örnek veri
$ad = "John"; // $_POST['ad'];
$soyad = "Doe"; // $_POST['soyad'];
$email = "john.doe@example.com"; // $_POST['email'];

// Veri ekleme sorgusu (sql cumlesine phpMyAdmin->veritabaniniz->tablonuz->sql->insert adresinden ulasabilirisniz)
$sql = "INSERT INTO kullanicilar (ad, soyad, email) VALUES ('$ad', '$soyad', '$email')";

// Sorguyu çalıştırma
if ($conn->query($sql) === TRUE) {
    echo "Veri başarıyla eklendi"; 
} else {
    echo "Veri ekleme hatası: " . $conn->error;
}

// Bağlantıyı kapat
$conn->close();
?>


```
#### Veri Listeleme
**index.php** dosyasinda verilerin yazilacigi bolume ekleyin
***!!!!!!!!Tablo adina dikkat edin!!!!!!! (Ornekteki tablo adi 'kullanicilar')***
```php
<?php
// Veri listeleme sorgusu
$sql = "SELECT * FROM kullanicilar";
$result = $conn->query($sql);

// Verileri ekrana yazdırma
if ($result->num_rows > 0) {
    while($row = $result->fetch_assoc()) {
        echo "ID: " . $row["id"]. " - Ad: " . $row["ad"]. " - Soyad: " . $row["soyad"]. " - Email: " . $row["email"]. "<br>";
    }
} else {
    echo "Hiç veri bulunamadı";
}

// Bağlantıyı kapat
$conn->close();
?>

```
#### İd İle Belirli Bir Veri Çekme
**detay.php** sayfasi icin
```php
<?php
// Örnek id
$userId = 1;

// Veri çekme sorgusu
$sql = "SELECT * FROM kullanicilar WHERE id = $userId";
$result = $conn->query($sql);

// Veriyi ekrana yazdırma
if ($result->num_rows > 0) {
    $row = $result->fetch_assoc();
    echo "ID: " . $row["id"]. " - Ad: " . $row["ad"]. " - Soyad: " . $row["soyad"]. " - Email: " . $row["email"]; //verilerinizi bu bicimde istediginiz yere yazabilirsiniz yazmak istediginiz yere php etiketi acin ve echo ile $row["<tablodaki kolon adi>"]
} else {
    echo "Belirtilen ID'ye sahip veri bulunamadı";
}

// Bağlantıyı kapat
$conn->close();
?>
```

>bu surum versiyon 1.0 bunu okuyanin ta amina cakayim ben the enes ad(m)iguzel
