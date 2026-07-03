# Power Cloud MKII – Ürün Özellikleri Dokümanı

| | |
|---|---|
| **Doküman Adı** | Power Cloud MKII – Ürün Özellikleri Dokümanı |
| **Doküman Versiyonu** | 1.0 |
| **Hazırlanma Tarihi** | 03.07.2026 |
| **Hazırlayan** | Özer Kavi |
| **Şirket** | ENKO Elektronik |

## Doküman Geçmişi

| Tarih | Versiyon | Değişikliği Yapan | Açıklama |
|---|---|---|---|
| 03.07.2026 | 1.0 | Özer Kavi | Dokümanın ilk sürümü oluşturuldu. |

## İçindekiler

- [1. Genel Bakış](#1-genel-bakış)
- [2. Çalışma Dizini ve Dosya Yapısı](#2-çalışma-dizini-ve-dosya-yapısı)
  - [2.1. Klasör Yapısı](#21-klasör-yapısı)
  - [2.2. Dosya Kategorileri](#22-dosya-kategorileri)
- [3. Yazılım Sayfaları](#3-yazılım-sayfaları)
- [4. JSON Dosyaları ve Davranışları](#4-json-dosyaları-ve-davranışları)
  - [4.1. device.json](#41-devicejson)
  - [4.2. paramDeviceName.json](#42-paramdevicenamejson)
  - [4.3. Parametre Detaylı Açıklama Dosyası (paramDeviceName.md)](#43-parametre-detaylı-açıklama-dosyası-paramdevicenamemd)
  - [4.4. designDeviceName.json](#44-designdevicenamejson)
  - [4.5. languageDeviceName.json](#45-languagedevicenamejson)
  - [4.6. quickConfig.json](#46-quickconfigjson)
  - [4.7. configWizard.json](#47-configwizardjson)
  - [4.8. diagramDeviceName.json ve DeviceName.svg](#48-diagramdevicenamejson-ve-devicenamesvg)
  - [4.9. userMessages.json](#49-usermessagesjson)
  - [4.10. deviceNotes.json](#410-devicenotesjson)
  - [4.11. deviceDocuments.json](#411-devicedocumentsjson)
- [5. Loglama Mekanizmaları](#5-loglama-mekanizmaları)
- [6. Firmware Update ve Otomatik Parametre Yedeği](#6-firmware-update-ve-otomatik-parametre-yedeği)

---

## 1. Genel Bakış

Power Cloud MKII, ENKO Elektronik tarafından tasarlanan ve üretilen elektronik cihazlarla Modbus RTU ve Modbus TCP protokolleri üzerinden haberleşen bir PC yazılımıdır. Yazılım; cihazlardan veri okuma ve yazma, anlık veri loglama, raporlama, alarm ve event kayıtlarının izlenmesi, firmware güncelleme ve parametre güncelleme işlemlerini gerçekleştirir.

Yazılımın temel mimarisi JSON tabanlıdır. Her cihaz modeli için önceden hazırlanmış JSON tanım dosyaları bulunur; yazılım hangi cihaza bağlanırsa, o cihaza özel sayfalar bu JSON dosyalarına göre dinamik olarak oluşturulur. Böylece tek bir yazılım, farklı cihazlara farklı ve cihaza özel arayüzler sunar.

JSON dosyalarının büyük bölümü internette (sunucuda) tutulur ve yazılım her açılışta versiyon kontrolü yaparak güncel dosyaları otomatik indirir. Bu sayede bir cihaza yeni bir parametre veya özellik eklendiğinde yalnızca sunucudaki ilgili JSON dosyasının güncellenmesi yeterlidir; kullanıcı yazılımı bir sonraki açışında güncellemeyi otomatik olarak almış olur. Yazılımın kendisinin yeniden dağıtılmasına gerek kalmaz.

JSON dosyalarının davranışları bu dokümanda tanımlanmıştır. Design dosyalarının iç yapısı ve format detayları ise ayrı bir dokümanda ([design-json-format-guide](../design-json-format-guide/README.md)) tanımlıdır.

## 2. Çalışma Dizini ve Dosya Yapısı

### 2.1. Klasör Yapısı

Yazılımın çalışma dizini altında aşağıdaki klasörler bulunur:

| Klasör | İçerik |
|---|---|
| `json/` | JSON dosyalarının indirildiği klasör (device, param, default design, quickConfig, configWizard vb.). |
| `design/` | Özel hazırlanmış design dosyalarının indirildiği klasör (uiFiles ve DESIGN_UPDATE ile gelen dosyalar). |
| `documents/` | Cihaz dokümanlarının indirildiği klasör. Parametre detaylı açıklama dosyaları (paramDeviceName.md) da bu klasöre elle konulur. |
| `translation/` | Power Cloud arayüz dil dosyalarının (translation_*.json) indirildiği klasör. |
| `log/` | System Log dosyalarının günlük olarak kaydedildiği klasör. |
| `temp/` | Firmware update öncesi otomatik alınan parametre yedeklerinin (.prl) tutulduğu klasör. |

### 2.2. Dosya Kategorileri

Power Cloud'un kullandığı dosyalar dört kategoride toplanır. Her cihaz için özel hazırlanmış veya genel kullanılan dosyalar bulunur.

> **Önemli:** Yalnızca **device**, **param** ve **design** dosyaları zorunludur. Diğer tüm dosyalar opsiyoneldir; bu dosyalar olmasa da Power Cloud çalışır.

#### 2.2.1. Genel Dosyalar

| Dosya | Çalışma Şekli | Açıklama |
|---|---|---|
| device.json | İnternetten otomatik indirilir | Tüm cihazların bilgilerinin bulunduğu dosya. |
| quickConfig.json | İnternetten otomatik indirilir | Tüm cihazların hızlı konfigürasyon bilgilerinin tutulduğu dosya. |
| configWizard.json | İnternetten otomatik indirilir | Tüm cihazların konfigürasyon sihirbazı bilgilerinin tutulduğu dosya. Kullanıcı ile soru-cevap şeklinde ilerler. |
| userMessages.json | Sunucuda durur, indirilmez; kontrolü ENKO'dadır | Kullanıcıya gönderilen mesajların bulunduğu dosya. |
| deviceNotes.json | Sunucuda durur, indirilmez; kontrolü ENKO'dadır | Cihazlara özel notların bulunduğu dosya. |
| deviceDocuments.json | Sunucuda durur, indirilmez; kontrolü ENKO'dadır | Cihazlara özel doküman listesi. Listedeki dokümanlar istenildiğinde internetten indirilir. |

#### 2.2.2. Cihaza Özel Dosyalar

Dosya adları cihaz adıyla birlikte oluşturulur (örn. `paramDAVR100.json`). Tümü internetten otomatik indirilir.

| Dosya | Açıklama |
|---|---|
| paramDeviceName.json | Parametre bilgilerinin bulunduğu dosyadır. Parametreler cihaz versiyonuna göre tanımlanır. Alarm ve event tanımları da bu dosyadadır. |
| designDeviceName.json | Varsayılan (default) design dosyasıdır. Cihaza özel sayfa tasarımları bu dosyada tanımlıdır. |
| languageDeviceName.json | Cihazın kendi ekran metinleri için dil dosyasıdır. |
| diagramDeviceName.json | Wiring diagram (bağlantı şeması) için cihazın etkileşim tanımlarıdır. |
| DeviceName.svg | Wiring diagram için cihazın bağlantı şeması görselidir. |

#### 2.2.3. Power Cloud Dil Dosyaları

Programın kendi arayüzünde kullanılan metinlerin farklı dillerdeki karşılıklarının bulunduğu dosyalardır (translation_English.json, translation_German.json, translation_Chinese.json vb.). Sunucuya yeni bir dil dosyası eklendiğinde kullanıcı bilgisayarına otomatik indirilir.

#### 2.2.4. Özel Hazırlanmış Design Dosyaları

Varsayılan design dosyaları dışında hazırlanmış genel veya özel design dosyalarıdır. İnternetten otomatik indirilir ve `design/` klasörüne kaydedilir.

## 3. Yazılım Sayfaları

Power Cloud MKII'de bulunan sayfalar, işlevlerine göre gruplanmış olarak aşağıda listelenmiştir.

### 3.1. Bağlantı ve Haberleşme

| Sayfa | Açıklama |
|---|---|
| Communication Settings | Bağlantı ayarlarının (Modbus RTU / Modbus TCP) yapıldığı sayfa. |

### 3.2. İzleme ve Kayıt

| Sayfa | Açıklama |
|---|---|
| Log Data | Anlık veri loglama ayarları. CSV, TXT ve SQL formatlarında kayıt yapılabilir. |
| Chart Page | Grafik izleme sayfası. |
| Alarm Log | Cihazın alarm geçmişinin görüntülendiği sayfa. |
| Event Log | Cihazın event (olay) geçmişinin görüntülendiği sayfa. |
| System Log | Kullanıcının yazılımda yaptığı tüm işlemlerin loglandığı sayfa (bkz. [Bölüm 5.1](#51-system-log)). |
| Offline Monitor | Cihaz bağlantısı olmadan, cihaza özel sayfaların önizlemesinin yapıldığı sayfa. |

### 3.3. Cihaz Yapılandırma

| Sayfa | Açıklama |
|---|---|
| Quick Config | Hızlı konfigürasyon sayfası. En sık kullanılan parametrelerin yapılandırılmasını sağlar (bkz. [Bölüm 4.6](#46-quickconfigjson)). |
| Configuration Wizard | Soru-cevap akışıyla ilerleyen konfigürasyon sihirbazı. Verilen cevaplara göre farklı konfigürasyonlar uygulanır (bkz. [Bölüm 4.7](#47-configwizardjson)). |
| Task Scheduling | Cihaz için görev tanımlama sayfası. |
| Device Language | Cihazın kendi ekran dilinin değiştirildiği sayfa (bkz. [Bölüm 4.5](#45-languagedevicenamejson)). |
| Import Param | Dosyadan (.prl) içe aktarılan parametrelerin görüntülendiği ve istenirse cihaza yazıldığı sayfa. |
| Firmware Update | Cihaz firmware güncellemesinin yapıldığı sayfa (bkz. [Bölüm 6](#6-firmware-update-ve-otomatik-parametre-yedeği)). |
| Background Image | Cihaz açılış resminin konfigüre edildiği sayfa. |

### 3.4. Cihaz Bilgi ve Dokümantasyon

| Sayfa | Açıklama |
|---|---|
| Diagram | Cihazın bağlantı şemasının (wiring diagram) görüntülendiği etkileşimli sayfa (bkz. [Bölüm 4.8](#48-diagramdevicenamejson-ve-devicenamesvg)). |
| Device Document | Bağlı cihaza ait dokümanların listelendiği ve indirildiği sayfa (bkz. [Bölüm 4.11](#411-devicedocumentsjson)). |
| Device Notes | Cihaza ait önemli notların ve SSS bilgilerinin görüntülendiği sayfa (bkz. [Bölüm 4.10](#410-devicenotesjson)). |
| User Messages | Kullanıcıya gönderilen mesajların görüntülendiği sayfa (bkz. [Bölüm 4.9](#49-usermessagesjson)). |

### 3.5. Kişiselleştirme ve Araçlar

| Sayfa | Açıklama |
|---|---|
| Design Editor | Kullanıcının sayfa tasarlayabildiği editör. Yapılan tasarıma göre design JSON dosyasını otomatik oluşturur; elle JSON yazmaya gerek kalmaz. |
| Theme | Yazılım temasının değiştirildiği sayfa. |
| Generate Language File | Kullanıcıya özel dil dosyasının oluşturulduğu sayfa. |

## 4. JSON Dosyaları ve Davranışları

### 4.1. device.json

Yazılımın tanıdığı tüm cihazların bilgilerinin bulunduğu dosyadır. Yazılımın bir cihaza bağlanabilmesi için o cihazın device.json içinde tanımlı olması gerekir. Dosya ayrıca, en başta yer alan özel bir "software" kaydı ile Power Cloud'un genel dosya güncelleme kontrolünü de içerir.

#### 4.1.1. Bağlantı Ön Koşulu

Yazılım, bağlandığı cihazı tanımak için sabit adreslerden okuma yapar:

| Adres | Okunan Bilgi | Açıklama |
|---|---|---|
| 9989 | Cihaz adı (name) | 10 register okunur ve ASCII olarak çözümlenir. Okunan ad, device.json içindeki `name` alanı ile eşleşmelidir. |
| 9975 | Cihaz versiyonu | Param dosyasındaki parametreler versiyon bazlı tanımlandığından, cihaz versiyonu bu adresten okunabilmelidir. |

> **Önemli:** Versiyon bilgisi 0 (sıfır) gelirse param dosyasından hiçbir parametre alınamaz ve ekranlar boş kalır.

#### 4.1.2. Cihaz Kaydı – Zorunlu Alanlar

Aşağıdaki alanlar tanımlı ise yazılım cihaza bağlanır. Bunların dışındaki tüm alanlar opsiyoneldir.

```json
{
  "name": "AMF-L",
  "fileVersion": 2,
  "type": "device",
  "deviceType": "Generator",
  "bMAddress": 19
}
```

| Alan | Açıklama |
|---|---|
| name | Cihaz adı. Cihazın içinde ASCII olarak tanımlı olmalıdır (bkz. Bağlantı Ön Koşulu). |
| type | Kayıt tipi. `"device"` cihazı temsil eder, `"software"` Power Cloud ile ilgili bilgileri temsil eder. |
| deviceType | Cihazların gruplanması için kullanılır (örn. Generator). |
| bMAddress | Boot mode adresidir. Yazılım firmware update yapacağı zaman bu adresi set ederek cihazı boot moduna sokar. |
| fileVersion | Cihaza ait param ve design dosyaları bu versiyon ile takip edilir. Lokaldeki versiyondan farklı ise yazılım, dosyaların güncellendiğini kabul eder ve ilgili cihaz için param ve design dosyalarını internetten yeniden indirir. |

#### 4.1.3. Opsiyonel Bloklar

Opsiyonel blokların ortak davranışı şudur: özellik `true` olarak tanımlandığında ilgili buton veya sayfa yazılım arayüzünde görünür hale gelir. Yani device.json, arayüzde hangi özelliklerin gösterileceğini de belirler.

**rtc** (true/false): Cihazda RTC (gerçek zaman saati) olduğunu ifade eder. True ise ekranda RTC set butonu görünür. `rtcOptions` tanımlı değilse ortak kararlaştırılmış varsayılan değerler kullanılır.

| rtcOptions Alanı | Açıklama |
|---|---|
| yearFormat | Yıl formatı: `"2digit"` veya `"4digit"`. |
| addresses | Hangi zaman bilgisinin (year, month, day, hour, minute, second) hangi adrese yazılacağını tanımlar. |

**taskScheduling** (true/false): Cihazda görev zamanlama özelliği olduğunu ifade eder. True ise ekranda Task Scheduling butonu görünür.

| taskSchedulingOptions Alanı | Açıklama |
|---|---|
| taskCount | Tanımlanabilecek görev sayısını ifade eder. Tanımlı değilse 1 kabul edilir. |
| functionParamBaseID | Task fonksiyon bilgilerinin hangi adresten itibaren alınacağını ifade eder. Mutlaka tanımlı olmalıdır. |

**eventLog / alarmLog** (true/false): Cihazda ilgili log özelliğinin olduğunu ifade eder. True ise ekranda ilgili sayfa/buton görünür. Okuma mantığı her iki log için ortaktır: yazılım, okumak istediği kaydın numarasını `indexAddress` alanına yazar; ardından ilgili kayıt `startAddress` – `endAddress` aralığından okunur.

| Options Alanı | Açıklama |
|---|---|
| startAddress | Kayıtların okunmaya başlanacağı adres. |
| endAddress | Kayıt okuma aralığının bittiği adres. |
| indexAddress | Okunacak kaydın index (kayıt numarası) bilgisinin yazıldığı adres. |
| logCount | Cihazda tutulan maksimum kayıt sayısı (örn. 30). |

**background**: Cihaz açılış ekranı (Background Image) yapılandırma özelliklerini tanımlar.

| Alan | Açıklama |
|---|---|
| backgroundImage | true/false. Cihazda açılış resmi özelliği olduğunu ifade eder. True ise ekranda Background Image butonu görünür. |
| imageSize | Resim boyutu (width, height). Belirtilen boyut dışında resim tanımlanmasını engeller. |
| backgroundColor | Arka plan rengi seçiminin olup olmayacağını tanımlar. |
| progressBarColor | Progress bar rengi seçiminin olup olmayacağını tanımlar. |
| qrCode | QR kod özelliğinin olup olmayacağını tanımlar. |
| qrCodeMaxLength | Maksimum QR kod karakter sayısı. |
| maxPacketSize | Verinin kaçar paket halinde yazılacağını tanımlar. Varsayılan 64'tür. |
| rgbaFormat | Resim verisinin hangi renk sıralaması ile yazılacağını tanımlar (örn. `"bgra"`). |

**deviceID**: Her cihaz için benzersiz (uniq) 64 karakterlik kodun okunma şeklini tanımlar. Yazılım bu bilgiyi cihazdan okur ve ekranda gösterir. Kod, her register'da iki karakter olacak şekilde 32 register'da tutulur. Varsayılan çalışma şekli: 9972 adresine sırasıyla index bilgisi yazılır (1'den 32'ye), 9973 adresinden veri okunur. deviceID bloğu tanımlıysa aşağıdaki alanlara göre okuma yapılır:

| Alan | Açıklama |
|---|---|
| type | `"block"` veya `"index"`. Varsayılan `"index"`tir. `"block"` ise belirtilen adresten blok olarak 32 register okunur. |
| readAddress | Okuma adresi. |
| writeAddress | Index yazma adresi. |

64 karakterlik deviceID verisinin içeriği:

| Karakter Sayısı | Bilgi |
|---|---|
| 2 | Hafta bilgisi |
| 2 | Yıl bilgisi |
| 16 | Stok kodu |
| 2 | BOM |
| 2 | Gerber |
| 6 | HHN |
| 6 | Seri no |
| 4 | Software no |
| 4 | Bootloader software no |
| 20 | Rezerve |

**enableGClassTest** (true/false): Grafik ekranında G-Class butonlarının gösterimini tanımlar. DAVR ürünleri için kullanılır.

#### 4.1.4. Örnek – Tüm Alanları İçeren Cihaz Kaydı

```json
{
  "name": "AMF-L",
  "fileVersion": 2,
  "type": "device",
  "deviceType": "Generator",
  "bMAddress": 19,
  "rtc": true,
  "rtcOptions": {
    "yearFormat": "2digit",
    "addresses": {
      "year": 201, "month": 202, "day": 203,
      "hour": 204, "minute": 205, "second": 206
    }
  },
  "taskScheduling": true,
  "taskSchedulingOptions": {
    "taskCount": 3,
    "functionParamBaseID": 379
  },
  "eventLogOptions": {
    "startAddress": 1801, "endAddress": 766,
    "indexAddress": 1800, "logCount": 30
  },
  "alarmLog": true,
  "alarmLogOptions": {
    "startAddress": 1701, "endAddress": 766,
    "indexAddress": 1700, "logCount": 30
  },
  "background": {
    "backgroundImage": true,
    "imageSize": { "width": 108, "height": 108 },
    "backgroundColor": true,
    "progressBarColor": true,
    "maxPacketSize": 64,
    "qrCode": true,
    "qrCodeMaxLength": 1500,
    "rgbaFormat": "bgra"
  },
  "deviceID": {
    "type": "block",
    "readAddress": 168,
    "writeAddress": 169
  },
  "enableGClassTest": true
}
```

#### 4.1.5. Software Kaydı ve Genel Dosya Güncelleme Mekanizması

device.json dosyasının en başında `type` değeri `"software"` olan özel bir kayıt bulunur. Bu kayıt, üç ayrı versiyon numarası ile üç farklı dosya grubunun güncellemesini tetikler:

```json
{
  "name": "POWER CLOUD MKII",
  "type": "software",
  "sharedFileVersion": 1,
  "translationVersion": 1,
  "uiFileVersion": 1,
  "uiFiles": [
    "customDesign_AMFL.json"
  ],
  "translations": [
    "Chinese"
  ]
}
```

| Alan | Değiştiğinde Yapılan İşlem |
|---|---|
| sharedFileVersion | quickConfig.json ve configWizard.json dosyaları yeniden indirilir (ortak dosyalar değişmiş demektir). Dosyalar `json/` klasörüne iner. |
| translationVersion | `translations` dizisindeki diller için dil dosyaları indirilir. Örneğin dizide "Chinese" varsa translation_Chinese.json adıyla indirilir. Dosyalar `translation/` klasörüne iner. |
| uiFileVersion | `uiFiles` dizisindeki dosyalar indirilir. Bunlar özel hazırlanmış design dosyalarıdır. uiFiles içine doğrudan dosya adı yazılır (örn. `"customDesign_AMF.json"`). Dosyalar `design/` klasörüne iner. |

Bu mekanizma, cihaz kayıtlarındaki `fileVersion` mantığı ile tutarlıdır: cihaz kayıtlarındaki fileVersion cihaza özel param/design dosyalarının güncellemesini tetiklerken, software kaydındaki bu üç versiyon genel dosyaların güncellemesini tetikler.

### 4.2. paramDeviceName.json

Cihaza ait parametrelerin, alarm ve event tanımlarının bulunduğu dosyadır. Parametreler cihaz versiyonuna göre tanımlanır; cihazdan okunan versiyon bilgisine göre uygun parametreler bu dosyadan alınır.

#### 4.2.1. Parametre Alanları

```json
{
  "id": 102,
  "modbusAddress": 102,
  "version": 4013,
  "name": "AVR Autostart",
  "group": "Configuration",
  "unit": "",
  "unitParamId": 100,
  "dataLength": 1,
  "signed": false,
  "view": "decimal",
  "coef": 0,
  "minValue": 0,
  "maxValue": 1,
  "defaultValue": 0,
  "valueMask": [
    { "value": 0, "mask": "Disabled" },
    { "value": 1, "mask": "Enabled" }
  ],
  "dataOperation": {
    "operation": "",
    "operationValue": ""
  },
  "comment": "AVR auto start setting. If enabled AVR will start as soon as there is no errors.",
  "readOnly": false,
  "relation": []
}
```

| Alan | Açıklama |
|---|---|
| id | Parametre kimliği. |
| modbusAddress | Parametrenin Modbus adresi. |
| version | Parametrenin geçerli olduğu cihaz versiyonu. Cihazdan okunan versiyon ile eşleştirilir. |
| name | Parametre adı. |
| group | Parametrenin ait olduğu grup. Ekranda gruplama için kullanılır. |
| unit | Birim bilgisi. |
| unitParamId | Birim bilgisinin hangi parametrenin değerinden alınacağı(BAR/PSI geçişleri için). |
| dataLength | Veri uzunluğu (register sayısı). |
| signed | İşaretli/işaretsiz veri bilgisi (true/false). |
| view | Gösterim biçimi. Tanımsız ise varsayılan `"decimal"` kabul edilir. Diğer seçenekler: `"ascii"` ve `"hexadecimal"`. |
| coef | Katsayı. Değer = ham değer × 10^coef olarak hesaplanır. |
| minValue / maxValue | Parametreye girilebilecek minimum ve maksimum değerler. |
| defaultValue | Varsayılan değer. |
| valueMask | Ham değerin ekranda metin karşılığıyla gösterilmesini sağlar (örn. 0 = Disabled, 1 = Enabled). |
| dataOperation | Cihazdan okunan ham değere uygulanan dönüşüm işlemi (bkz. 4.2.2). |
| comment | Parametre açıklaması. Parameter-setting sayfasında gösterilir. |
| readOnly | true ise parametre yalnızca okunabilir. |
| relation | Parametreler arası ilişki/doğrulama kuralları (bkz. 4.2.3). |

#### 4.2.2. Değer Hesaplama: coef, dataOperation ve İşlem Sırası

> **İşlem sırası:** Ham değer → önce **coef** uygulanır (değer × 10^coef) → sonra **dataOperation** uygulanır → sonuç ekranda gösterilir.

Örnek: Ham değer 2048, coef = 1, dataOperation `/1024` ise: 2048 × 10 = 20480 → 20480 / 1024 = **20** olarak kabul edilir.

```json
"dataOperation": {
  "operation": "/",
  "operationValue": "1024"
}
```

Bu tanımda, okunan parametre değeri 1024'e bölünür ve bu şekilde kabul edilir. Operation işlemleri (hem dataOperation hem relation için ortaktır):

| Operation | İşlem |
|---|---|
| `+` | değer + operationValue |
| `-` | değer − operationValue |
| `*` | değer × operationValue |
| `/` | değer / operationValue. operationValue 0 ise işlem uygulanmaz. |
| `1/` | operationValue / değer (ters oran). Değer 0 ise sonuç geçersiz kabul edilir. |

#### 4.2.3. Relation – Parametreler Arası Doğrulama

Bir parametreye girilen değer, `relation` dizisinde tanımlı kurallar ile kontrol edilir. Bir parametrede birden fazla relation kuralı tanımlanabilir.

```json
"relation": [
  {
    "relatedParamId": 73,
    "relatedValue": 9,
    "condition": "gt",
    "errorType": "warning",
    "message": "Mesaj bilgisi",
    "operation": "-",
    "operationValue": 0
  },
  {
    "relatedValue": 9,
    "condition": "lt",
    "errorType": "block",
    "message": "ffff"
  }
]
```

**Referans değer önceliği:** `relatedParamId` tanımlıysa, kıyaslama referansı olarak ilgili parametrenin güncel değeri alınır. Tanımlı değilse `relatedValue` sabit değeri kullanılır.

**Operation uygulaması:** Referans değer üzerine operation + operationValue işlemi uygulanır. Örneğin relatedParamId = 73, operation = `"-"`, operationValue = 10, condition = `"gt"` ise: girilen değer, P73'ün değerinin 10 eksiğinden büyük olmak zorundadır.

| Condition | Anlamı |
|---|---|
| eq | Değer, referansa eşit olmalıdır. |
| neq | Değer, referansa eşit olmamalıdır. |
| gt | Değer, referanstan büyük olmalıdır. |
| lt | Değer, referanstan küçük olmalıdır. |
| gte | Değer, referanstan büyük veya eşit olmalıdır. |
| lte | Değer, referanstan küçük veya eşit olmalıdır. |

| errorType | Davranış |
|---|---|
| block | message bilgisi gösterilir ve işlem engellenir (değer cihaza yazılmaz). |
| warning | message bilgisi gösterilir ancak işlem yapılır (değer cihaza yazılır). |

#### 4.2.4. Alarm ve Event Tanımları

Alarm ve event tanımları, aynı param dosyası içinde `alarms` ve `events` dizileri olarak tutulur. Cihazdan okunan alarm/event kayıtlarındaki ID'ler bu tanımlarla eşleştirilerek Alarm Log ve Event Log sayfalarında açıklamalı olarak gösterilir.

```json
"alarms": [
  { "alarmId": 44, "alarmComment": "S2: Sensor Signal Too High" },
  { "alarmId": 45, "alarmComment": "S2: Sensor Positive Wire Fault" },
  { "alarmId": 46, "alarmComment": "S2: Sensor Negative Wire Fault" },
  { "alarmId": 47, "alarmComment": "S2: Sensor Problem" }
],
"events": [
  { "eventId": 1, "eventComment": "S1 Status Change" },
  { "eventId": 2, "eventComment": "S1 Daily Log" },
  { "eventId": 3, "eventComment": "S1 Status Change" },
  { "eventId": 4, "eventComment": "S1 Oil Signal Change" }
]
```

**severity:** Alarm/event tanımlarına eklenebilen opsiyonel alandır. Beş seviye alır: `critical`, `high`, `medium`, `low`, `info`. Severity yalnızca görsel ayrım sağlar; kayıt satırı seviyesine göre farklı renkte gösterilir (critical kırmızı, high turuncu, medium sarı, low yeşil, info mavi tonlarında).

### 4.3. Parametre Detaylı Açıklama Dosyası (paramDeviceName.md)

Bir parametreye tıklandığında parameter-setting sayfası açılır; bu sayfada parametre bilgileri ve comment görünür, parametre değeri buradan set edilir. Ayrıca, varsa parametreyle ilişkilendirilmiş dokümanlar da bu sayfada gösterilir (bkz. [Bölüm 4.11](#411-devicedocumentsjson)).

Comment alanının kısa açıklamasının yetmediği durumlar için parametrelere Markdown formatında detaylı açıklama eklenebilir. Markdown dosyasında açılan parametreye ait bir bölüm varsa, bu içerik parameter-setting sayfasında görüntülenir. Markdown sayesinde tablolar, önemli notlar, ilişkili parametreler ve sorun giderme adımları gibi zengin içerikler tanımlanabilir.

| Özellik | Açıklama |
|---|---|
| Dosya adı | paramDeviceName.md (örn. paramDAVR100.md) |
| Konum | Çalışma dizinindeki `documents/` klasörü |
| Dağıtım | İnternetten otomatik indirilmez; klasöre elle (manuel) konulur. Otomatik güncelleme mekanizmasının dışındadır. |
| Zorunluluk | Opsiyoneldir. Dosya yoksa yazılım normal çalışır; yalnızca detaylı açıklama bölümü görünmez. |

**Başlık formatı ve versiyon mantığı:** Her parametre bölümü `## PARAM_minVersiyon_paramId` formatında bir başlıkla açılır. Örneğin `## PARAM_4000_112` ifadesi, 112 numaralı parametrenin açıklaması anlamına gelir ve 4000 ve üzeri versiyonlu cihazlarda geçerlidir; 3000 versiyonlu bir cihaza bağlanıldığında bu açıklama görünmez.

Aynı parametre için farklı versiyonlarda birden fazla bölüm tanımlanabilir (örn. PARAM_3000_112 ve PARAM_4000_112). Bu durumda cihaz versiyonuna uyan **en yüksek versiyonlu** bölüm gösterilir: 3500 versiyonlu cihazda PARAM_3000_112, 4200 versiyonlu cihazda PARAM_4000_112 görünür.

Örnek dosya yapısı:

```markdown
# Parameter Documentation

---

## PARAM_4000_111
### Motor Speed Control

**Description:**
This parameter controls the target speed of the motor in RPM...

**Operating Ranges:**

| Speed Range   | Application          | Cooling Status       |
|---------------|----------------------|----------------------|
| 0-500 RPM     | Low speed operations | Fan cooling required |
| 500-1500 RPM  | Normal operations    | Natural cooling      |

**Troubleshooting:**
1. If motor doesn't reach target speed:
   - Check power supply voltage
   ...

---

## PARAM_4000_112
### Motor Temperature
...
```

### 4.4. designDeviceName.json

Cihaza ait tüm sayfa tasarımlarının tanımlandığı dosyadır. Cihaza özel dinamik ekranlar bu dosyaya göre oluşturulur.

Dosyanın iç yapısı ve format detayları bu dokümanın kapsamında değildir; ayrıntılar için [design-json-format-guide](../design-json-format-guide/README.md) dokümanına bakınız.

Design dosyasını elle yazmak zorunlu değildir. Yazılım içindeki **Design Editor** sayfası üzerinden görsel tasarım yapıldığında, editör sayfa tasarımına karşılık gelen JSON dosyasını otomatik olarak oluşturur. Yani design dosyası iki şekilde elde edilebilir: elle yazarak (format kılavuzuna göre) veya Design Editor ile otomatik üreterek.

### 4.5. languageDeviceName.json

Cihazın kendi ekranında görünen metinlerin farklı dillerde gösterilmesini sağlayan dosyadır. Her metnin bir id'si vardır; yeni metin cihaza bu id üzerinden gönderilir. Device Language sayfasının veri kaynağıdır.

```json
{
  "id": 1,
  "length": 16,
  "pixel": 120,
  "font": "Calibri",
  "fontSize": "16",
  "text_1": "Çıkışlar",
  "text_2": "Outputs"
}
```

| Alan | Açıklama |
|---|---|
| id | Metin kimliği. Metin cihaza bu id üzerinden gönderilir. |
| length | Tanımlıysa metin en fazla bu kadar karakteri destekler. |
| pixel | length tanımlı değilse kullanılır: cihazda bu metin için ayrılan piksel genişliğidir. |
| font / fontSize | length tanımlı değilse kullanılır: metin bu font tipinde ve boyutunda hesaplanır; ayrılan piksel genişliğine sığan kadarı gösterilir. |
| text_1 | Metnin Türkçe karşılığı (sabit). |
| text_2 | Metnin İngilizce karşılığı (sabit). |

**Karakter sınırı mantığı:** `length` tanımlıysa karakter bazlı sınır uygulanır. `length` tanımlı değilse piksel bazlı sınırlama devreye girer: metin, belirtilen font ve fontSize ile hesaplanır ve cihazda ayrılan piksel genişliğine sığan kadarı gösterilir.

### 4.6. quickConfig.json

Hızlı konfigürasyon işlemine yarar. Cihazdaki tüm parametreler yerine en çok/sık kullanılan parametrelerin hızlıca yapılandırılmasını sağlar. Quick Config sayfasının veri kaynağıdır.

```json
{
  "device": "DAVR100", "version": 1000, "name": "Quick Configuration",
  "itemList": [
    { "paramId": 100, "message": "RMS Voltage should be set according to sense terminal connections." },
    { "paramId": 122, "message": "Sensing Mode should be set according to sense terminal connections." },
    { "paramId": 110, "message": "" },
    { "paramId": 111, "message": "" },
    { "paramId": 117, "message": "UFRO Knee Point should be set accordingly for 50 / 60Hz systems." },
    { "paramId": 400, "message": "OEX Current Limit should be set to 1PU (100%) for the OEX to operate correctly." }
  ]
}
```

| Alan | Açıklama |
|---|---|
| device | Tanım, bu isimdeki cihaza bağlanıldığında geçerlidir. |
| version | Tanım, bu versiyon **ve üzeri** cihazlar için geçerlidir. |
| name | Tanım, hızlı konfigürasyon listesinde bu isimle görünür. |
| itemList | Gösterilecek parametrelerin listesi. Her satırda `paramId` (param dosyasındaki parametre) yer alır. `message` doluysa o parametrenin yanında açıklayıcı bilgi olarak gösterilir; boşsa yalnızca parametre görünür. |

**Çoklu tanım ve versiyon davranışı:** Aynı cihaz için farklı `name` değerleriyle birden fazla tanım yapılarak farklı hızlı yapılandırma setleri sunulabilir; kullanıcı listeden istediğini seçer. Versiyon koşulunu sağlayan (cihaz versiyonu ≥ tanımın version değeri) **tüm tanımlar** listelenir.

### 4.7. configWizard.json

Kullanıcıyı soru-cevap akışıyla yönlendirerek konfigürasyon yapan sihirbaz tanımlarını içerir. Configuration Wizard sayfasının veri kaynağıdır. Üst seviye alanlar (device, version, name) ve çoklu tanım/versiyon davranışı quickConfig ile aynıdır: aynı cihaz için farklı isimlerle birden fazla wizard tanımlanabilir; versiyon koşulunu sağlayan tüm wizard'lar listelenir.

```json
{
  "device": "DAVR100",
  "version": 4031,
  "name": "Generator Setup Wizard",
  "steps": [
    {
      "id": "step1",
      "question": "What is the generator connection type?",
      "description": "Select the connection type of your generator's sensing terminals.",
      "options": [
        {
          "label": "3-Phase 4-Wire",
          "description": "Three phase sensing with neutral connection.",
          "actions": [
            { "paramId": 122, "value": 0 },
            { "paramId": 100, "value": 400 }
          ],
          "nextStep": "step2"
        },
        {
          "label": "3-Phase 3-Wire",
          "description": "Three phase sensing without neutral.",
          "actions": [
            { "paramId": 122, "value": 1 },
            { "paramId": 100, "value": 230 }
          ],
          "nextStep": "step2"
        }
      ]
    },
    {
      "id": "step2",
      "question": "What is the system frequency?",
      "description": "Select the nominal frequency of your power system.",
      "options": [
        {
          "label": "50 Hz",
          "description": "Standard frequency for Europe, Asia and Africa.",
          "actions": [
            { "paramId": 117, "value": 50 },
            { "paramId": 118, "value": 50 }
          ],
          "nextStep": null
        },
        {
          "label": "60 Hz",
          "description": "Standard frequency for Americas.",
          "actions": [
            { "paramId": 117, "value": 60 },
            { "paramId": 118, "value": 60 }
          ],
          "nextStep": null
        }
      ]
    }
  ]
}
```

| Alan | Açıklama |
|---|---|
| steps | Wizard adımlarının dizisidir. |
| steps → id | Adımın benzersiz kimliği. Dallanma için referans olarak kullanılır. |
| steps → question | Kullanıcıya sorulan soru. |
| steps → description | Sorunun altında görünen açıklama. |
| steps → options | Cevap seçenekleri. |
| options → label | Seçeneğin adı (örn. "3-Phase 4-Wire"). |
| options → description | Seçeneğin açıklaması. |
| options → actions | Bu seçenek seçildiğinde uygulanacak parametre yazımları. Her action bir paramId + value çiftidir; tek seçenek birden fazla parametreyi ayarlayabilir. |
| options → nextStep | Seçim sonrası gidilecek adımın id'si. `null` ise wizard biter. |

**Dallanma:** Farklı seçenekler farklı nextStep değerlerine yönlendirilebildiği için verilen cevaba göre farklı sorular ve akışlar kurgulanabilir.

**Yazma davranışı:** Seçimler wizard boyunca biriktirilir; tüm adımlar tamamlandığında parametre değerleri cihaza **en sonda topluca yazılır**. Kullanıcı wizard'ı yarıda bırakırsa cihaza hiçbir değişiklik yansımaz.

### 4.8. diagramDeviceName.json ve DeviceName.svg

Her cihaz için iki dosya bulunur: **diagramDeviceName.json** (etkileşim tanımları) ve **DeviceName.svg** (bağlantı şemasının görseli). SVG, Diagram sayfasında açılır; kullanıcı şema üzerindeki giriş/çıkışlara veya konnektörlere tıklayarak işlem yapabilir. Böylece kullanıcı, cihazın fiziksel bağlantı şemasına bakarken ilgili terminale tıklayıp o terminalin ayarına doğrudan ulaşabilir.

```json
{
  "device": "DAVR100",
  "hotspots": [
    {
      "pathId": "path4141",
      "label": "AI1 - Analog Input",
      "action": "message",
      "message": "0-10V analog giriş. Maksimum 10V uygulanabilir. Bu pine aşırı voltaj uygulamayın."
    },
    {
      "pathId": "path2",
      "label": "DI1 - Digital Input",
      "action": "setParameter",
      "paramId": 55
    },
    {
      "pathId": "path5000",
      "label": "Generator Bağlantı Ayarı",
      "action": "wizard",
      "steps": [ ]
    }
  ]
}
```

`hotspots` dizisi, SVG üzerindeki tıklanabilir bölgeleri tanımlar. SVG üzerinde hotspot olarak tanımlanmamış bölgeler tıklanabilir değildir; tıklandığında herhangi bir işlem gerçekleşmez.

| Alan | Açıklama |
|---|---|
| pathId | SVG içindeki ilgili path elementinin id'si. Tıklanabilir bölge bu id ile eşleştirilir. |
| label | Bölgenin adı/başlığı (örn. "AI1 - Analog Input"). |
| action | Tıklandığında yapılacak işlem tipi: `message`, `setParameter` veya `wizard`. |

| Action Tipi | Davranış |
|---|---|
| message | Bilgilendirme amaçlıdır; `message` alanındaki açıklama gösterilir (örn. aşırı voltaj uyarısı). |
| setParameter | `paramId` ile belirtilen parametrenin düzenleme penceresi açılır; kullanıcı değeri görüp düzenleyebilir. |
| wizard | Konnektöre özel bir soru-cevap sihirbazı başlatılır. `steps` yapısı configWizard ile birebir aynı şemadır (bkz. [Bölüm 4.7](#47-configwizardjson)). |

> **Önemli fark – yazma davranışı:** Diagram üzerinden başlatılan wizard'da parametre değerleri, configWizard'daki gibi sonda toplu yazılmaz; kullanıcı **Set tuşuna bastığı anda** ilgili parametreler cihaza yazılır. Aynı adım şemasını kullanmalarına rağmen yazma davranışları farklıdır, JSON hazırlarken bu fark dikkate alınmalıdır.

### 4.9. userMessages.json

Kullanıcılara mesaj/bildirim göndermek için kullanılır. Dosya sunucuda durur, indirilmez; kontrolü ENKO'dadır. Program açılışında bu dosya kontrol edilir ve koşulları sağlayan mesajlar kullanıcıya gösterilir. User Messages sayfasının veri kaynağıdır.

```json
{
  "id": 1,
  "device": "DAVR100",
  "minVersion": 1000,
  "maxVersion": 5000,
  "idContains": ["12345", "1225566"],
  "title": "Title",
  "message": "Mesaj bilgisi",
  "isPermanent": true,
  "command": "USER_MESSAGE",
  "lastDate": "2026-03-15"
}
```

| Alan | Açıklama |
|---|---|
| id | Mesaj kimliği. |
| device | Mesaj, bu isimdeki cihaz bağlıyken geçerlidir. |
| minVersion / maxVersion | Cihaz versiyonu bu aralıktaysa mesaj gösterilir. |
| idContains | Cihazın 64 karakterlik benzersiz deviceID'si ile "içinde geçen" mantığıyla eşleşir. Boş dizi ise ID filtresi uygulanmaz. |
| title | Mesaj başlığı. |
| message | Mesaj içeriği. HTML destekler; tıklanabilir link eklenebilir. |
| lastDate | Mesajın son yayınlanacağı tarih. Bu tarihten sonra kullanıcıya bu mesaj gösterilmez. |
| isPermanent | true ise tarihe bakılmaksızın mesaj sürekli gösterilir. |
| command | Mesaj tipi: USER_MESSAGE, FIRMWARE_UPDATE veya DESIGN_UPDATE. |
| fileUrl | FIRMWARE_UPDATE ve DESIGN_UPDATE komutlarında indirilecek dosyanın adresi. |

**idContains ile hedefleme:** deviceID'nin yapısı (hafta, yıl, stok kodu, BOM, gerber, seri no...) sayesinde hedefleme çok esnektir. Tam ID yazılırsa mesaj dünyadaki tek bir cihaza gönderilebilir; stok kodu yazılırsa o stok kodundaki tüm cihazlara; yıl+hafta yazılırsa o hafta üretilen cihazlara; BOM veya gerber bilgisiyle de benzer filtrelemeler yapılabilir.

| Command | Davranış |
|---|---|
| USER_MESSAGE | Yalnızca mesaj gösterir. |
| FIRMWARE_UPDATE | Mesaj içinde firmware update butonu çıkar; butona basıldığında `fileUrl` adresindeki dosya indirilir ve firmware güncellemesi yapılır. |
| DESIGN_UPDATE | `fileUrl` adresindeki design dosyası `design/` klasörüne indirilir; böylece kullanıcıya yeni bir tasarım tanımlanmış olur. |

Mesaj içeriğine link ekleme örneği:

```json
"message": "DAVR100 ürününe ait dokümanlara ulaşmak için <a href='#' onclick='openUrl(\"https://enkoelektronik.com/...\"); return false;' style='color: var(--textSecondary);'>buraya tıklayın</a>"
```

**Mesaj görünürlüğü ve okundu takibi:** Okundu takibi vardır. Koşulları sağlayan mesajlar her açılışta mesaj kutusunda (User Messages sayfasında) durmaya devam eder. Mesaj daha önce okunmadıysa kullanıcıya "1 message" şeklinde bildirim (notification) gösterilir; okunduysa bildirim çıkmaz ancak mesaj listede erişilebilir kalır. isPermanent olmayan mesajlar lastDate geçince artık gösterilmez.

### 4.10. deviceNotes.json

Cihazlara ait önemli notların, uyarıların ve SSS (sıkça sorulan sorular) tarzı bilgilerin tutulduğu dosyadır. Sunucuda durur, indirilmez; kontrolü ENKO'dadır. Device Notes sayfasının veri kaynağıdır. Sunucuda durduğu için, sahadaki bir cihazla ilgili yeni bir bilgi/uyarı eklemek istendiğinde dosyanın güncellenmesi yeterlidir; tüm kullanıcılar bir sonraki açılışta güncel notları görür.

```json
[
  {
    "device": "DAVR100",
    "minVersion": 1000,
    "maxVersion": 5000,
    "title": "Önemli Uyarı-Tr",
    "message": "Mesaj içeriği buraya yazılacak",
    "language": "Tr"
  },
  {
    "device": "DAVR100",
    "minVersion": 1000,
    "maxVersion": 5000,
    "title": "SSS Mesaj Başlığı",
    "message": "SSS Mesaj içeriği buraya yazılacak...",
    "language": "Fr"
  }
]
```

| Alan | Açıklama |
|---|---|
| device | Notun ait olduğu cihaz. O cihaz bağlıyken gösterilir. |
| minVersion / maxVersion | Cihaz versiyonu bu aralıktaysa not geçerlidir. |
| title | Not başlığı. |
| message | Not içeriği. |
| language | Notun dili (örn. "Tr", "Fr"). Aynı not farklı dillerde ayrı kayıtlar olarak tanımlanabilir. Device Notes sayfasındaki dil butonu ile kullanıcı yalnızca istediği dildeki notları filtreleyerek listeleyebilir. |

### 4.11. deviceDocuments.json

Bağlı cihaza ait dokümanların listesini getirir. Sunucuda durur; kontrolü ENKO'dadır. Device Document sayfasının veri kaynağıdır.

```json
{
  "device": "CCS-M",
  "minVersion": 1000,
  "maxVersion": 1500,
  "paramId": [1, 2, 3],
  "name": "Dokuman - 1",
  "language": "Eng",
  "document": "https://raw.githubusercontent.com/en-ko/PowerCloud/main/documents/AMF-L_ON_KULLANIM_KILAVUZU.pdf"
}
```

| Alan | Açıklama |
|---|---|
| device | Dokümanın ait olduğu cihaz. |
| minVersion / maxVersion | Cihaz versiyonu bu aralıktaysa doküman listelenir. |
| paramId | Parametre id dizisi. Bağlama duyarlı gösterim sağlar (aşağıya bakınız). |
| name | Dokümanın listede görünen adı. |
| language | Dokümanın dili. |
| document | Dokümanın indirme adresi (URL). |

**İndirme davranışı:** Doküman listede sürekli durur. **Download** tuşuyla indirilen dosya `documents/` klasörüne kaydedilir. Doküman daha önce indirilmişse Download'un yanında **Open** tuşu da görünür; kullanıcı dosyayı doğrudan açabilir.

**paramId ile bağlama duyarlı gösterim:** Dizide parametre id'leri tanımlıysa, kullanıcı ilgili cihazın parametre ayar sayfasını (parameter-setting) o parametrelerden biri için açtığında bu doküman o sayfada da görünür. Böylece kullanıcı bir parametreyi ayarlarken, o parametreyle ilgili dokümana Device Document sayfasına gitmeden ulaşabilir.

## 5. Loglama Mekanizmaları

Power Cloud MKII'de iki ayrı loglama mekanizması bulunur: kullanıcıya görünen **System Log** ve arka planda çalışan teknik **Debug Log**.

### 5.1. System Log

Kullanıcının yazılımda yaptığı tüm işlemleri loglar. Loglar anlık olarak çalışma dizinindeki `log/` klasörüne, o günün tarihiyle isimlendirilen dosyaya kaydedilir (günlük dosya mantığı):

```
system_log_2026-06-30.txt
```

Kayıtlar System Log sayfasından da görüntülenebilir.

**Parametre değişikliklerinin loglanması:** Bir parametre değiştirildiğinde "şu parametre, şu değerden şu değere değiştirildi" formatında log tutulur. Böylece parametrenin eski değeri de kayıt altına alınmış olur; "parametre neydi, ne yapıldı" sorusunun cevabı her zaman mevcuttur.

### 5.2. Debug Log

Kullanıcının hiçbir sayfada görmediği, yazılımın arka planda tuttuğu teknik logdur. Otomatik dosya kaydı yapmaz; log oluştuğunda hafızada tutulur. Farklı debug seviyelerinde kayıt tutar; catch(error) bilgilerini loglar ve kayıtlar hata kodları içerir. Bu kodlarla yazılımın nerede hataya düştüğü tespit edilebilir.

**Kayıt alma:** `Ctrl+Shift+L` kısayoluna basıldığında dosya kayıt penceresi açılır ve loglar CSV formatında kaydedilebilir.

**Destek senaryosu:** Kullanıcı bir hata yaşadığında Ctrl+Shift+L ile kaydettiği CSV dosyasını ENKO'ya gönderir; ekip, hata kodu ve stack bilgisiyle sorunu debug modunda yakalar.

Örnek kayıt:

```
"03.07.2026 08:40:27","error","0271","","{""error"":""ENOENT: no such file or directory, open 'D:\\...\\json\\configWizard.json'"",""stack"":""Error: ENOENT: no such file or directory, ..."
```

## 6. Firmware Update ve Otomatik Parametre Yedeği

Firmware güncellemesi Firmware Update sayfasından yapılır. Yazılım, device.json içinde tanımlı `bMAddress` adresini set ederek cihazı boot moduna sokar ve güncellemeyi gerçekleştirir. Firmware güncellemesi ayrıca userMessages.json üzerinden FIRMWARE_UPDATE komutu ile de tetiklenebilir (bkz. [Bölüm 4.9](#49-usermessagesjson)).

**Otomatik parametre yedeği:** Firmware update işlemi başlatıldığında yazılım, kullanıcı fark etmeden (arka planda, otomatik olarak) güncelleme öncesindeki parametre değerlerini yedekler. Yedek, çalışma dizini altındaki `temp/` klasörüne **.prl** dosyası olarak kaydedilir. Böylece firmware update öncesi parametre yedeği otomatik alınmış olur; kullanıcının yedek almayı unutması riski ortadan kalkar.

Yedekler birikir: her firmware update işleminde yeni bir .prl dosyası oluşur, eski yedekler silinmez. Bu sayede geçmişteki herhangi bir güncelleme öncesinin parametre setine dönülebilir.

**Geri yükleme (tam döngü):** .prl dosyası, Import Param sayfasının kullandığı dosya formatının aynısıdır. Güncelleme sonrası bir sorun yaşanırsa kullanıcı, `temp/` klasöründeki .prl dosyasını Import Param sayfasından açar, parametreleri görüntüler ve cihaza geri yazar.


---

*Bu doküman, Power Cloud MKII'nin özelliklerini tanımlar. Yeni özellikler eklendikçe doküman güncellenmeli ve Doküman Geçmişi tablosuna yeni satır eklenmelidir.*
