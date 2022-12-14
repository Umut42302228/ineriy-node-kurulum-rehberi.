
<h1 align="center">Inery-Testnet-Kurulum-Rehberi


### Inery, verileri merkezden dağıtmak için blok zinciri teknolojisini kullanmak ve aynı zamanda veri ihlallerini azaltmak ve güvenliği sağlamak için benimsenen blok zinciri sinerjisine sahip dağıtılmış bir veritabanını temsil eder. Bu yaklaşım, kullanıcı verilerini güvence altına alır ve yaygın bir kullanıma sahiptir.

### Güvenli depolama, ilaç, tedarik zincirleri, finans, bankacılık vb. alanlarda kullanılabilir. Inery platformu uygulaması, sürekli olarak bilgisayar tarafından okunabilir bir forma dönüştürülen verilerin depolanması işlevi görür. Bu şekilde, verilerin güvenli bir şekilde saklanması ve değer sözleşmeleriyle bağlanmasıyla Inery Blockchain, verilerin en yüksek şeffaflık ve güvenlikle depolanmasını, değiştirilmesini ve aktarılmasını sağlar.

### Inery yazılımı, merkezi olmayan blok zinciri teknolojisinden yararlanmak isteyen herhangi bir işletme için mükemmel bir çözümü temsil ediyor. Bu nedenle Inery, veritabanlarının merkeziyetsizliği ele almak için özel olarak tasarlanmıştır.

### Sistem Gereksinimleri 

|CPU | RAM  | Disk  | 
|----|------|----------|
|   6| 12GB  | 500GB    |

 
  
  # 1. adım
Öncelikle [Buradan](https://testnet.inery.io/dashboard/) sitesine girip kayıt ''Sign Up'' butonuyla kayıt olmamız gerekiyor. Kayıt aşamasından sonra bizden sunucumuza dair birtakım bilgileri istediği için, sunucuyu temin ettikten sonra kayıt işlemine devam etmemiz gerekiyor.
<br/><br>
![inery2](https://user-images.githubusercontent.com/111747226/199738064-451761ea-99cc-4250-8cdf-bcbcbc2aa463.png)

  Görseldeki adımları tamamlamak için; Aşağıdaki görseldeki gibi suncunuzdan bilgilerinizi temin edebilirsiniz. Contabo üzerinden gösterlim; "Reverse DNS Managment" sekmesine basıyoruz. Sonrasında gelen sayfada hem IP adresiniz karşında da ServerName kısmı var bunları kopyalayıp kayıt olurken yukarıdaki görselde gösterilen yerlere yazıyoruz.
 <br/><br> 
 ![inery3](https://user-images.githubusercontent.com/111747226/199739053-1e982aef-64ef-4843-9f26-ce4719e9da2c.png)
 
 ### Kayıt işlemi tamamladıktan sonra kendi sayfanızdaki bölümden test tokeni claim ediyoruz. Sonrasında, Node kurulum adımlarına geçebiliriz.
 
   # 2. adım Nore Kurulumu
   
  ## Root yetkisi alalım. Contabo gibi sunucu kullanıyorsanız bunu yapmanıza gerek yok.
  ```
  sudo su
  cd
  ```
  
 ## Sunucu güncellemesi yapıyoruz 
  
  ```
 sudo apt update && sudo apt upgrade -y
  ```
  
 ## Kütüphane kurulumunu yapalım
  
 ```
sudo apt-get install -y make bzip2 automake libbz2-dev libssl-dev doxygen graphviz libgmp3-dev \
autotools-dev libicu-dev python2.7 python2.7-dev python3 python3-dev \
autoconf libtool curl zlib1g-dev sudo ruby libusb-1.0-0-dev \
libcurl4-gnutls-dev pkg-config patch llvm-7-dev clang-7 vim-common jq libncurses5
 ```
 
## Firewall için düzenleme yapıyoruz node çalışacak portları açmamız gerekiyor.
   ```
sudo apt-get install firewalld 
sudo systemctl start firewalld 
sudo systemctl enable firewalld 
sudo firewall-cmd --set-default-zone=public 
sudo firewall-cmd --zone=public --add-port=22/tcp --permanent 
sudo firewall-cmd --zone=public --add-port=8888/tcp --permanent 
sudo firewall-cmd --zone=public --add-port=9010/tcp --permanent 
sudo firewall-cmd --reload 
sudo systemctl restart firewalld
 ```
 ## Githubdan gerekli dosyaları indiriyoruz.
   ```
git clone https://github.com/inery-blockchain/inery-node
 ```
## Kurulum klasörüne giriyoruz.
   ```
cd inery-node/inery.setup
 ```
## Uygulama izinlerini değiştirelim
   ```
chmod +x ine.py
 ``` 
## Binary'i aktarıyoruz.
   ```
./ine.py --export
 ``` 
## Bilgileri güncelleyelim.
   ```
cd; source .bashrc; cd -
 ``` 
## Config dosyasının içine girelim.
   ```
sudo nano tools/config.json
 ``` 
## Gerekli kısımlar değiştiriyoruz. Config dosyası içindeki bu bölümün gerekli ayarları kayıt olduğunuz Inery dashboard üzerinden ulaşabilirsiniz. oradaki bilgileri Aşağıdak kod parçasında gördüğünüz örnekteki yerlere yazıyoruz. 
   ```
"MASTER_ACCOUNT":
{
    "NAME": "AccountName",
    "PUBLIC_KEY": "PublicKey",
    "PRIVATE_KEY": "PrivateKey",
    "PEER_ADDRESS": "IP:9010",
    "HTTP_ADDRESS": "0.0.0.0:8888",
    "HOST_ADDRESS": "0.0.0.0:9010"
}
 ``` 
 ### Gerekli düzenlemeyi yaptıktan sonra CRTL+X yaptıktan sonra Y basıp ENTER ile değişkliği kayıt ediyoruz.
 
## Screen oluşturulım.
   ```
screen -R inery
 ```
## Node Başlatıyoruz.
   ```
./ine.py --master
 ```
 ### Node'u başlattıktan sonra Sync olmayı beklememiz gerekiyor. CTRL+C kullanmıyoruz CRTL+A+D ile screeni kapatabiliriz.

