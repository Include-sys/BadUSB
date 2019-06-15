# BadUSB

![BadUSB](http://i.imgur.com/eLdzMhR.jpg)


Baduino, HID aygıtlar taklit edilerek, ilgili İşletim Sistemi'ne komutların gönderilebildiği bir cihazdır. Öncesinden hazırlanmış bir takım script dosyalarını üzerinde bulunan depolama modülüne bağlı depolama cihazından okur ve çalıştırır.

<b>Donanım</b>

![Baduino](http://i.imgur.com/mnQKtk9.png)

Üstteki şekilde bağlantılar gösterilmekle birlikte devre elemanları şunlardır;

SparkFun Pro Micro 5V/16Mhz ya da 3.3V/8Mhz<br>
MicroSD Card Module<br>
DIP Switch(4'lü)<br>

Kart, MicroSD modülü ile SPI haberleşme standardını kullandığı için USB Host Conroller özelliğinı kullanamıyoruz, bu da demek oluyor ki hedef İşletim Sistemiyle dosya alışverişi yapma gibi bir seçeneğimiz yok.

DIP Switch'i daha önceden hazırlanmış olan scriptleri seçmek için kullanıyoruz.

<b>Yazılım</b>

Bölüm 1 - Yorumlayıcı

Komutlar

REM - Yorum satırı, bu satırdaki karakterler yorumlayıcı tarafından dikkate alınmaz.

STRING - Yazı girişi, bu satırdaki karakterler yorumlayıcı tarafından İşletim Sistemine "tuşa basma olayı" olarak gönderilir. Örneğin "STRING Merhaba Dünya" şeklinde bir komutumuz olsun. Metin belgesi açık şekilde Baduino bilgisayar takıldığında, metin belgesine "Merhaba Dünya" yazar. Herhangi bir yazı girişi alanına yazı yazdırır.

DELAY - Baduino ancak sizin bilgisayarınız kadar hızlıdır. Örneğin FTP'den 10MB boyutunda ki bir dosyayı indirirken bu işlemin 1 saniye gibi bir sürede gerçekleşmesini bekleyemezsiniz. Bu gibi durumlara karşı gecikmeyi olabildiğince fazla, gizlilik içinse olabildiğince kısa eklemeniz gerekmektedir. Eğer yetersiz bir gecikme süresi eklerseniz, yapılması beklenen işlem ve sonraki işlemler düzgün şekilde gerçekleşmeyecektir.

Yukarıda ki 3 temel komut dışında,

CTRL
SHIFT
CAPS
ENTER
BACKSPACE
SPACE
F1-12
ESC
.
.
.

tuşları script dosyalarında sıkça kullanılmıştır. Örneğin arama çubuğu ekranını açmak için Windows Logolu tuşu etkinleştiren "GUI" komutu yazılır. Başlat menüsü açılır bu şekilde. Bu bölümde aratılan bir program, örnek olarak "cmd", şu şekilde yönetici haklarıyla çalıştırılır.

DELAY 3000
GUI
DELAY 1000
STRING cmd
DELAY 500
CTRL SHIFT ENTER
DELAY 1000
ALT y

GUI, komutuyla Başlat Menüsü açılıyor.
STRING cmd ile "cmd" yazıyor.
CTRL SHIFT ENTER ile Yönetici olarak çalıştırmak için diyalog penceresi açıyor.
ALT y ile Açılan Diyalog Penceresinde "Evet" onayı veriyoruz.


Bu komutları birebir kendiniz girerek deneyince aldığınız sonuçlar aynı olacaktır. Baduino scriptleri, tamamen Fiziksel bir klavyeyi taklit ederek sisteme saldırı gerçekleştirir. Gecikmeler eklemeyi ihmal etmemeliyiz ve en dikkat edeceğiniz noktalar bu kısımdır.

Bölüm 2 - Nelere Dikkat Edilmeli

Dizin isimlerinde kesinlikle Türkçe karakterler(ğüçöşı,ĞÜŞİÇÖ) kullanılmamalıdır. Yorum satırlarında sakıncası yoktur. Kısaca Yorumlayıcının dikkate aldığı bütün satırlarda Türkçe karakterler kullanılmamalıdır.

Arduino IDE ile yeni yazılım atılırken,
Dosya -> Tercihler -> Ek Devre Kartları Yöneticisi URL'leri kısmına,
https://raw.githubusercontent.com/sparkfun/Arduino_Boards/master/IDE_Board_Manager/package_sparkfun_index.json
bu adres eklendikten sonra Arduino IDE yeniden başlatılıp,
Araçlar -> Kart kısımında "SparkFun Pro Micro" kartı seçildikten sonra yine Araçlar bölümüne gelen İşlemci seçeneğini ATmega32U4(5V, 16MHz) olarak seçtiğinizden emin olun.

Ayrıca "Kaynak Kod" dizininde bulunan Keyboard.cpp ve Keyboard.h dosyalarının da Baduino.ino dosyası ile aynı dizinde olduğuna emin olun.
