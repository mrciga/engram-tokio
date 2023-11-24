# Engram Tokio Chain Testnet (Dencun Fork)

#### Yeni RPC network bilgileri:

```
Network Name: Engram Tokio Dencun Testnet
New RPC URL: https://tokioswift.engram.tech/
Chain ID: 131
Symbol: tGRAM
Block explorer URL: https://tokioscan-v2.engram.tech/
```

#### Daha önceden node kurduysak, aşağıdaki komutları sırası ile çalıştırarak eski repoyu silelim :

```
cd tokio-docker
docker compose down -v
cd ..
rm -rf tokio-docker
```

#### Node kurulumu için repoyu yükleyelim :

```
git clone https://github.com/engram-network/tokio-docker.git
cd tokio-docker
git checkout dencun
chmod +x ./scripts/*.sh
./scripts/install-asdf.sh
mkdir -p execution consensus validator
```

#### Eğer daha önceden cüzdan oluşturmadıysak aşağıdaki komut ile yeni bir cüzdan oluşturuyoruz ve çıkan mnemonicleri saklıyoruz :

```
eth2-val-tools mnemonic
```

#### Çıkan mnemonicleri tilki cüzdana ekleyip cüzdan adresimiz ile aşağıdaki linkten daha önce almadıysak 33 tGRAM talep edelim : 

```
https://faucet-tokio.engram.tech/  
```

#### Aşağıdaki komutu girerek deposit dosyasını yapılandıralım :

```
nano ./scripts/validator-deposit-data.sh
```

#### Açılan dosyada aşağıdaki alanları değiştirelim :

```
withdrawals-mnemonic: Tırnak içine mnemonicleri yazalım 
validators-mnemonic: Tırnak içine mnemonicleri yazalım 
from: Cüzdan adresimizi yazalım
privatekey: Cüzdan adresimizin private keyini yazalım
```

#### Aşağıdaki komutu girerek deposit işlemini tamamlıyoruz :

```
bash ./scripts/validator-deposit-data.sh
```

#### Deposit işlemini başarılı bir şekilde tamamladıktan sonra aşağıdaki komut ile validator oluşturuyoruz :

```
./scripts/validator-build.sh
```

#### Çıkan ekranda soruları aşağıdaki şekilde yanıtlıyoruz :

```
1.soru enter
2.soru 0
3.soru mnemoniclerimizi yazalım (tırnak olmadan)
4.soru testnet
5.soru şifre oluşturalım
6.soru şifreyi tekrar yazalım
```

#### Docker değişkenlerini yapılandırıyoruz :

```
sudo nano docker-compose.yml
```

#### Açılan dosyada aşağıdaki alanları değiştirelim :

```
identity=nickname belirleyip yazın
enr-address=sunucunuzun ip adresini yazın
graffiti=discord kullanıcı adınızı yazın
ethstats=nickname belirleyip yazın
```

#### Eğer kurulu değilse aşağıdaki komut ile docker kuruyoruz :

```
./scripts/install-docker.sh
```

#### Aşağıdaki komutu çalıştırarak node'umuzu başlatalım :

```
docker compose up -d
```

#### Aşağıdaki komut ile loglara bakıyoruz, node'un sync olmasını kontrol ediyoruz :

```
docker logs lighthouse_cl -f
```

#### Aşağıdaki adresten kendimizi kontrol ediyoruz :

```
https://nodewatch.engram.tech
```

Eğer doğru bir şekilde kurulumu tamamladıysanız nodunuzun ismini aktif validatörler içinde göreceksiniz.

