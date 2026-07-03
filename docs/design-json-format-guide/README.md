# Design JSON Object Oluşturma Kılavuzu

Bu doküman, yazılımda kullanılan dinamik ekran tasarımı için kullanılan JSON dosyasında yer alan object türlerini ve özelliklerini detaylı şekilde açıklamaktadır.  
Her obje, ekran üzerinde farklı bir bileşeni temsil eder ve burada yer alan açıklamalar, JSON dosyanızı doğru ve etkili şekilde oluşturmanız için rehberlik eder.

| | |
|---|---|
| **Doküman Adı** | Power Cloud MKII – Object Oluşturma Klavuzu |
| **Doküman Versiyonu** | 1.0 |
| **Hazırlanma Tarihi** | 03.07.2026 |
| **Hazırlayan** | Özer Kavi |
| **Şirket** | ENKO Elektronik |

## Doküman Geçmişi

| Tarih | Versiyon | Değişikliği Yapan | Açıklama |
|---|---|---|---|
| 03.07.2026 | 1.0 | Özer Kavi | Doküman GitHub formatına düzenlendi (içindekiler ve doküman bilgileri eklendi). |

## İçindekiler

- [datacard Nesnesi](#datacard-nesnesi)
- [datacardgroup Nesnesi](#datacardgroup-nesnesi)
- [datalist Nesnesi](#datalist-nesnesi)
- [progressgauge Nesnesi](#progressgauge-nesnesi)
- [gradegauge Nesnesi](#gradegauge-nesnesi)
- [bargauge Nesnesi](#bargauge-nesnesi)
- [fillbargauge Nesnesi](#fillbargauge-nesnesi)
- [temperaturegauge Nesnesi](#temperaturegauge-nesnesi)
- [pressuregauge Nesnesi](#pressuregauge-nesnesi)
- [thermometer Nesnesi](#thermometer-nesnesi)
- [fueltank Nesnesi](#fueltank-nesnesi)
- [airtank Nesnesi](#airtank-nesnesi)
- [ledindicator Nesnesi](#ledindicator-nesnesi)
- [ledioindicator Nesnesi](#ledioindicator-nesnesi)
- [text Nesnesi](#text-nesnesi)
- [image Nesnesi](#image-nesnesi)
- [table Nesnesi](#table-nesnesi)
- [dataTable Nesnesi](#datatable-nesnesi)
- [chart Nesnesi](#chart-nesnesi)
- [button Nesnesi](#button-nesnesi)
  - [config Nesnesi (sayfa yapılandırması)](#️-örnek-config-nesnesi)
- [space Nesnesi](#space-nesnesi)
- [dataoperation Nesnesi](#dataoperation-nesnesi)

---

# `datacard` Nesnesi

Bu nesne, **veri kartlarını (data card)** tanımlamak için kullanılır. Ekranda gösterilecek bilgi kartlarının görünümü, metin biçimi, renkler ve koşullara göre davranışları bu nesne üzerinden belirlenir.

---

## 🔧 Özellikler

| Alan Adı            | Tür       | Açıklama |
|---------------------|-----------|----------|
| `object`            | string    | Nesne tipi, `"datacard"` olmalıdır. |
| `page`              | number    | Ekranda gösterileceği sayfa numarası. |
| `row`               | number    | Gösterilecek satır sayısı. |
| `side`              | string    | Ekranın hangi tarafında gösterileceği (`"left"`, `"right"`, `"center"`). |
| `width`             | string    | Kartın genişliği (örnek: `'200px'`). |
| `height`            | string    | Kartın yüksekliği (örnek: `'120px'`). |
| `paramId`           | dizi      | Gösterilecek parametre ID'leri (örn: `[29]`). |
| `nameFontSize`      | string    | Başlığın font boyutu (örn: `'18px'`). |
| `nameIsBold`        | boolean   | Başlık kalın mı? (`true` veya `false`). |
| `nameIsItalic`      | boolean   | Başlık italik mi? |
| `nameColor`         | string    | Başlık rengi (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `valueFontSize`     | string    | Değerin font boyutu (örn: `'14px'`). |
| `valueIsBold`       | boolean   | Değer kalın mı? |
| `valueIsItalic`     | boolean   | Değer italik mi? |
| `valueColor`        | string    | Değerin rengi (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `backgroundColor`   | string    | Arka plan rengi (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `information`       | string    | Kullanıcıya gösterilecek bilgi mesajı. |
| `infoIconColor`     | string    | Bilgi ikonunun rengi (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `conditions`        | array     | Koşullu formatlama için kullanılan koşullar dizisi. |

---

## 🧠 `conditions` (Koşullar)

Kartın görünümünü veya davranışını koşullara göre değiştirmek için kullanılır.

Her bir `condition` şu alanları içerir:

| Alan Adı             | Tür      | Açıklama |
|----------------------|----------|----------|
| `conditionParamId`   | number   | Koşulun uygulanacağı parametre ID'si. |
| `compareParamId`     | number   | Karşılaştırma yapılacak parametre ID'si (öncelik compareParamId karşılaştırmasıdır. compareParamId yok ise compareValue sabiti ile karşılaştırma yapar). |
| `compareValue`       | string   | Karşılaştırma yapılacak değer. |
| `operator`           | string   | Karşılaştırma operatörü. Desteklenen operatörler: `eq` (eşit), `neq` (eşit değil), `gt` (büyük), `lt` (küçük), `gte` (büyük veya eşit), `lte` (küçük veya eşit), `bitZero` (bit sıfır mı), `bitOne` (bit bir mi). |
| `fixedValue`         | string   | Koşul sağlanırsa gösterilecek sabit metin. |
| `isHidden`           | boolean  | Koşul sağlandığında kart gizlensin mi? |
| `isDisabled`         | boolean  | Koşul sağlandığında kart pasif olsun mu? |
| `backgroundColor`    | string   | Koşul sağlanırsa arka plan rengi ne olsun (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |

### 🔁 `andConditions` (Ek Koşullar)

Her bir `condition` içinde isteğe bağlı olarak `andConditions` tanımlanabilir.

| Alan Adı             | Tür      | Açıklama |
|----------------------|----------|----------|
| `conditionParamId`   | number   | Ek koşulun parametre ID'si. |
| `compareParamId`     | number   | Karşılaştırma yapılacak parametre ID'si (öncelik compareParamId karşılaştırmasıdır. compareParamId yok ise compareValue sabiti ile karşılaştırma yapar). |
| `compareValue`       | string   | Karşılaştırma değeri. |
| `operator`           | string   | Karşılaştırma operatörü. Desteklenen operatörler: `eq` (eşit), `neq` (eşit değil), `gt` (büyük), `lt` (küçük), `gte` (büyük veya eşit), `lte` (küçük veya eşit), `bitZero` (bit sıfır mı), `bitOne` (bit bir mi). |

---

## 🧪 Örnek `datacard` Nesnesi

```json
{
  "object": "datacard",
  "page": 1,
  "row": 3,
  "side": "center",
  "width": "200px",
  "height": "120px",
  "paramId": [29],
  "nameFontSize": "18px",
  "nameIsBold": true,
  "nameIsItalic": false,
  "nameColor": "red",
  "valueFontSize": "24px",
  "valueIsBold": true,
  "valueIsItalic": false,
  "valueColor": "blue",
  "backgroundColor": "green",
  "information": "Bu mesaj test amaçlıdır",
  "infoIconColor": "yellow",
  "conditions": [
    {
      "conditionParamId": 117,
      "compareParamId": 118,
      "compareValue": "48.60",
      "operator": "eq",
      "fixedValue": "Hata durumu!",
      "isHidden": false,
      "isDisabled": false,
      "backgroundColor": "red",
      "andConditions": [
        {
          "conditionParamId": 123,
          "compareValue": "0V – 10V",
          "operator": "neq"
        }
      ]
    }
  ]
}
```


# `datacardgroup` Nesnesi

Bu nesne, **bir grup veri kartını** (datacard) bir arada göstermek için kullanılır. Genellikle benzer veya ilişkili parametrelerin toplu olarak sunulması için tercih edilir.

---

## 🔧 Özellikler

| Alan Adı          | Tür          | Açıklama |
|-------------------|--------------|----------|
| `object`          | string       | Nesne tipi, `"datacardgroup"` olmalıdır. |
| `page`            | number       | Ekranda gösterileceği sayfa numarası. |
| `row`             | number       | Gösterilecek satır sayısı. |
| `side`            | string       | Ekranın hangi tarafında gösterileceği (`"left"`, `"right"`, `"center"`). |
| `width`           | string       | Kartın genişliği (örnek: `"200px"`). |
| `height`          | string       | Kartın yüksekliği (örnek: `"120px"`). |
| `name`            | string       | Grup adı / başlığı. |
| `paramId`         | array[number]| Gösterilecek parametrelerin ID listesi. |
| `showUnits`       | boolean      | Birimlerin gösterilip gösterilmeyeceği. |
| `minDigits`       | number       | Değerin en az kaç basamak gösterileceği. Eksik basamaklar soldan `0` ile doldurulur. Tanımlanmazsa uygulanmaz (örn: `2` → `5` değeri `05` olur). showUnits özelliğinin false olması durumunda geçerlidir. |
| `separator`       | string       | Grup içindeki öğeler arasına konacak ayırıcı karakter (örneğin `":"`). |
| `nameFontSize`    | string       | Grup adı yazı boyutu (örn: `"24px"`). |
| `nameIsBold`      | boolean      | Grup adı kalın mı? |
| `nameIsItalic`    | boolean      | Grup adı italik mi? |
| `nameColor`       | string       | Grup adı rengi (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `valueFontSize`   | string       | Değerlerin yazı boyutu (örn: `'14px'`). |
| `valueIsBold`     | boolean      | Değerler kalın mı? |
| `valueIsItalic`   | boolean      | Değerler italik mi? |
| `valueColor`      | string       | Değerlerin rengi (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `information`     | string       | Kullanıcıya gösterilecek açıklama mesajı. |
| `infoIconColor`   | string       | Bilgi ikonunun rengi (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |

---

## 🧪 Örnek `datacardgroup` Nesnesi

```json
{
  "object": "datacardgroup",
  "page": 1,
  "row": 8,
  "side": "center",
  "width": "300px",
  "height": "400px",
  "name": "Jeneratör Çalışma Saati",
  "paramId": [
    99,
    98,
    97,
    96,
    95,
    94
  ],
  "showUnits": true,
  "separator": ":",
  "minDigits" : 2,
  "nameFontSize": "24px",
  "nameIsBold": true,
  "nameIsItalic": true,
  "nameColor": "red",
  "valueFontSize": "14px",
  "valueIsBold": true,
  "valueIsItalic": true,
  "valueColor": "yellow",
  "information": "Açıklama",
  "infoIconColor": "yellow"
}
```


# `datalist` Nesnesi

Bu nesne, dinamik ekranda **veri listesi** oluşturmak için kullanılır. Liste, bir sayfada birden fazla öğe göstermek için tasarlanmıştır ve her öğenin yazı biçimi, renkleri ve koşullu durumları tanımlanabilir.

---

## 🔧 Özellikler

| Alan Adı          | Tür          | Açıklama |
|-------------------|--------------|----------|
| `object`          | string       | Nesne tipi, `"datalist"` olmalıdır. |
| `page`            | number       | Listelenen sayfa numarası. |
| `row`             | number       | Listede gösterilecek satır sayısı. |
| `side`            | string       | Ekranın hangi tarafında gösterileceği (`"left"`, `"right"`, `"center"`). |
| `width`           | string       | Listenin genişliği (örnek: `"300px"`). |
| `height`          | string       | Listenin yüksekliği (örnek: `"400px"`). |
| `title`           | string       | Listenin başlığı. |
| `titleFontSize`   | string       | Başlık yazı boyutu (örn: `'14px'`). |
| `titleIsBold`     | boolean      | Başlık kalın mı? |
| `titleIsItalic`   | boolean      | Başlık italik mi? |
| `titleColor`      | string       | Başlık rengi (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`).|
| `itemFontSize`    | string       | Liste öğelerinin yazı boyutu. |
| `showItemBorder`  | boolean      | Öğelerin çevresinde sınır çizgisi gösterilsin mi? |
| `itemList`        | array        | Liste içinde gösterilecek öğeler dizisi. |
| `conditions`      | array        | Koşullu formatlama için kullanılan koşullar dizisi. |
| `protectionSet`   | object       | Protection sayfası için ayarlar. İçinde `topToggleId`, `textInputIds`, `leftToggleId`, `rightToggleId` gibi parametre ID'leri bulunur. Bu tanımlama varsa protection sayfası açılır ve ekran bu ayarlara göre oluşturulur (Özellikler AVR projelerinde protection sayfaları için tasarlanmıştır).|


---


## 🧠 `conditions` (Koşullar)

Datalistin görünümünü veya davranışını koşullara göre değiştirmek için kullanılır.

Her bir `condition` şu alanları içerir:

| Alan Adı             | Tür      | Açıklama |
|----------------------|----------|----------|
| `conditionParamId`   | number   | Koşulun uygulanacağı parametre ID'si. |
| `compareParamId`     | number   | Karşılaştırma yapılacak parametre ID'si (öncelik compareParamId karşılaştırmasıdır. compareParamId yok ise compareValue sabiti ile karşılaştırma yapar). |
| `compareValue`       | string   | Karşılaştırma yapılacak değer. |
| `operator`           | string   | Karşılaştırma operatörü. Desteklenen operatörler: `eq` (eşit), `neq` (eşit değil), `gt` (büyük), `lt` (küçük), `gte` (büyük veya eşit), `lte` (küçük veya eşit), `bitZero` (bit sıfır mı), `bitOne` (bit bir mi). |
| `isHidden`           | boolean  | Koşul sağlandığında kart gizlensin mi? |
| `isDisabled`         | boolean  | Koşul sağlandığında kart pasif olsun mu? |
| `backgroundColor`    | string   | Koşul sağlanırsa arka plan rengi ne olsun (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |

### 🔁 `andConditions` (Ek Koşullar)

Her bir `condition` içinde isteğe bağlı olarak `andConditions` tanımlanabilir.

| Alan Adı             | Tür      | Açıklama |
|----------------------|----------|----------|
| `conditionParamId`   | number   | Koşulun uygulanacağı parametre ID'si. |
| `compareParamId`     | number   | Karşılaştırma yapılacak parametre ID'si (öncelik compareParamId karşılaştırmasıdır. compareParamId yok ise compareValue sabiti ile karşılaştırma yapar). |
| `compareValue`       | string   | Karşılaştırma değeri. |
| `operator`           | string   | Karşılaştırma operatörü. Desteklenen operatörler: `eq` (eşit), `neq` (eşit değil), `gt` (büyük), `lt` (küçük), `gte` (büyük veya eşit), `lte` (küçük veya eşit), `bitZero` (bit sıfır mı), `bitOne` (bit bir mi). |

---

## 🧩 `itemList` İçeriği

Her liste öğesi aşağıdaki alanlara sahiptir:

| Alan Adı        | Tür       | Açıklama |
|-----------------|-----------|----------|
| `paramId`            | number    | Parametre ID'si. |
| `nameIsBold`    | boolean   | Öğenin adı kalın mı? |
| `nameIsItalic`  | boolean   | Öğenin adı italik mi? |
| `nameColor`     | string    | Öğenin adı rengi (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `valueIsBold`   | boolean   | Öğenin değeri kalın mı? |
| `valueIsItalic` | boolean   | Öğenin değeri italik mi? |
| `valueColor`    | string    | Öğenin değeri rengi (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `information`   | string    | Öğeye ait bilgi mesajı. |
| `infoIconColor` | string    | Bilgi ikonunun rengi (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `isEditable`    | boolean   | Parametre datalist üzerinden set edilsin mi? |
| `conditions`    | array     | Koşullu formatlama için kullanılan koşullar dizisi. |

---

## 🧠 `conditions` Dizisi (Opsiyonel)

Koşullar, bir öğe değeri belirli bir şarta uyduğunda görüntüyü değiştirmek için kullanılır.

| Alan Adı          | Tür       | Açıklama |
|-----------------  |-----------|----------|
| `compareParamId`  | number    | Karşılaştırma yapılacak parametre ID'si (öncelik compareParamId karşılaştırmasıdır. compareParamId yok ise compareValue sabiti ile karşılaştırma yapar. Eğer her ikisi de var ise compareParamId değerini compareValue ile karşılaştırır). |
| `compareValue`    | string    | Karşılaştırılacak değer. |
| `operator`        | string    | Karşılaştırma operatörü. Desteklenen operatörler: `eq` (eşit), `neq` (eşit değil), `gt` (büyük), `lt` (küçük), `gte` (büyük veya eşit), `lte` (küçük veya eşit), `bitZero` (bit sıfır mı), `bitOne` (bit bir mi). |
| `displayText`     | string    | Koşul sağlandığında gösterilecek metin. |
| `textColor`       | string    | Koşul sağlandığında metin rengi (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `backgroundColor` | string    | Koşul sağlandığında arka plan (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `isHidden`        | boolean   | Koşul sağlandığında item gizlensin mi? |

---

## 🧩 `protectionSet` İçeriği

`protectionSet` nesnesi aşağıdaki alanlara sahiptir ve `datalist` içinde opsiyonel olarak tanımlanabilir. Bu yapı varsa protection sayfası açılır ve ekran bu ayarlara göre oluşturulur:

| Alan Adı         | Tür          | Açıklama |
|------------------|--------------|----------|
| `topToggleId`    | number       | Üst toggle kontrol parametre ID'si. |
| `textInputIds`   | array[number]| Metin girişi alanlarının parametre ID'leri dizisi. |
| `leftToggleId`   | number       | Sol toggle kontrol parametre ID'si. |
| `rightToggleId`  | number       | Sağ toggle kontrol parametre ID'si. |

---

## 🧪 Örnek `datalist` Nesnesi

```json
{
  "object": "datalist",
  "page": 1,
  "row": 1,
  "side": "center",
  "width": "300px",
  "height": "400px",
  "title": "Veri Listesi",
  "titleFontSize": "18px",
  "titleIsBold": true,
  "titleIsItalic": false,
  "titleColor": "var(--textPrimary)",
  "itemFontSize": "24px",
  "showItemBorder": false,
  "conditions": [
    {
      "conditionParamId": 134,
      "compareValue": "10",
      "operator": "eq",
      "isHidden": false,
      "isDisabled" : true,
      "backgroundColor" : "Green"
    }
  ],
  "itemList": [
    {
      "paramId": 29,
      "nameIsBold": true,
      "nameIsItalic": false,
      "nameColor": "#123456",
      "valueIsBold": true,
      "valueIsItalic": true,
      "valueColor": "red",
      "information": "Bu değer sistemin çalışma sıcaklığını gösterir",
      "infoIconColor": "yellow",
      "isEditable": true
    },
    {
      "paramId": 50,
      "nameIsBold": false,
      "nameIsItalic": true,
      "nameColor": "var(--textPrimary)",
      "valueIsBold": true,
      "valueIsItalic": false,
      "valueColor": "var(--textPrimary)",
      "information": "Bu değer sistemin çalışma sıcaklığını gösterir",
      "conditions": [
        {
          "compareValue": "51",
          "operator": "eq",
          "displayText": "HATA!",
          "textColor": "#ffffff",
          "backgroundColor": "#ff0000",
          "isHidden":false
        }
      ]
    },
    {
      "paramId": 51,
      "nameIsBold": false,
      "nameIsItalic": true,
      "nameColor": "var(--textPrimary)",
      "valueIsBold": true,
      "valueIsItalic": false,
      "valueColor": "var(--textPrimary)",
      "information": "Bu değer sistemin çalışma sıcaklığını gösterir",
      "conditions": [
        {
          "compareParamId": 52,
          "operator": "eq",
          "displayText": "HATA!",
          "textColor": "#ffffff",
          "backgroundColor": "#ff0000",
          "isHidden":false
        }
      ]
    }
  ],
  "protectionSet": {
        "topToggleId": 459,
        "textInputIds": [456,458],
        "leftToggleId": 462,
        "rightToggleId": 463
    }
}
```


# `progressgauge` Nesnesi

Bu nesne, bir parametrenin ilerleme göstergesini (progress gauge) ekranda göstermek için kullanılır. Genellikle ölçüm değerlerini görsel olarak ifade etmek için tercih edilir.

---

## 🔧 Özellikler

| Alan Adı                | Tür          | Açıklama |
|-------------------------|--------------|----------|
| `object`                | string       | Nesne tipi, `"progressgauge"` olmalıdır. |
| `page`                  | number       | Gösterileceği sayfa numarası. |
| `row`                   | number       | Satır numarası. |
| `side`                  | string       | Ekranın hangi tarafında gösterileceği (`"left"`, `"right"`, `"center"`). |
| `width`                 | string       | Göstergenin genişliği (örnek: `"200px"`). |
| `height`                | string       | Göstergenin yüksekliği (örnek: `"190px"`). |
| `paramId`               | array[number]| Gösterilecek parametre ID'si listesi (tek veya çok olabilir). |
| `nameFontSize`          | string       | Gösterge adı yazı boyutu. |
| `nameIsBold`            | boolean      | Gösterge adı kalın mı? |
| `nameIsItalic`          | boolean      | Gösterge adı italik mi? |
| `nameColor`             | string       | Gösterge adı rengi (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `valueTextSize`         | number       | Gösterge üzerindeki değer yazı boyutu. |
| `valueTextColor`        | string       | Gösterge üzerindeki değer (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `mainColor`             | string       | Gösterge ana rengi (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `secondaryColor`        | string       | Gösterge ikincil rengi (örn. doluluk dışında kalan renk). |
| `showProgress`          | boolean      | İlerleme durumunun gösterilip gösterilmeyeceği. |
| `splitNumber`           | number       | Gösterge üzerindeki bölme sayısı (ölçeklendirme). |
| `labelDecimalPlaces`    | number       | Göstergedeki etiketlerin ondalık basamak sayısı. |
| `valueDecimalPlaces`    | number       | Göstergedeki değerin ondalık basamak sayısı. |
| `information`           | string       | Kullanıcıya gösterilecek bilgi mesajı. |
| `infoIconColor`         | string       | Bilgi ikonunun rengi (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `criticalLow`           | number       | Kritik alt sınır değeri (örneğin sıcaklık alt limiti). |
| `criticalHigh`          | number       | Kritik üst sınır değeri. |
| `conditions`            | array        | Koşullu formatlama için kullanılan koşullar dizisi. |

---

## 🧠 `conditions` (Koşullar)

Kartın görünümünü veya davranışını koşullara göre değiştirmek için kullanılır.

Her bir `condition` şu alanları içerir:

| Alan Adı             | Tür      | Açıklama |
|----------------------|----------|----------|
| `conditionParamId`   | number   | Koşulun uygulanacağı parametre ID'si. |
| `compareParamId`     | number   | Karşılaştırma yapılacak parametre ID'si (öncelik compareParamId karşılaştırmasıdır. compareParamId yok ise compareValue sabiti ile karşılaştırma yapar). |
| `compareValue`       | string   | Karşılaştırma yapılacak değer. |
| `operator`           | string   | Karşılaştırma operatörü. Desteklenen operatörler: `eq` (eşit), `neq` (eşit değil), `gt` (büyük), `lt` (küçük), `gte` (büyük veya eşit), `lte` (küçük veya eşit), `bitZero` (bit sıfır mı), `bitOne` (bit bir mi). |
| `fixedValue`         | string   | Koşul sağlanırsa gösterilecek sabit metin. |
| `isHidden`           | boolean  | Koşul sağlandığında kart gizlensin mi? |
| `isDisabled`         | boolean  | Koşul sağlandığında kart pasif olsun mu? |
| `backgroundColor`    | string   | Koşul sağlanırsa arka plan rengi ne olsun (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |

### 🔁 `andConditions` (Ek Koşullar)

Her bir `condition` içinde isteğe bağlı olarak `andConditions` tanımlanabilir.

| Alan Adı             | Tür      | Açıklama |
|----------------------|----------|----------|
| `conditionParamId`   | number   | Ek koşulun parametre ID'si. |
| `compareParamId`     | number   | Karşılaştırma yapılacak parametre ID'si (öncelik compareParamId karşılaştırmasıdır. compareParamId yok ise compareValue sabiti ile karşılaştırma yapar). |
| `compareValue`       | string   | Karşılaştırma değeri. |
| `operator`           | string   | Karşılaştırma operatörü. Desteklenen operatörler: `eq` (eşit), `neq` (eşit değil), `gt` (büyük), `lt` (küçük), `gte` (büyük veya eşit), `lte` (küçük veya eşit), `bitZero` (bit sıfır mı), `bitOne` (bit bir mi). |

---

## 🧪 Örnek `progressgauge` Nesnesi

```json
{
  "object": "progressgauge",
  "page": 1,
  "row": 1,
  "side": "center",
  "width": "200px",
  "height": "190px",
  "paramId": [95],
  "nameFontSize": "18px",
  "nameIsBold": false,
  "nameIsItalic": true,
  "nameColor": "var(--textPrimary)",
  "valueTextSize": "24px",
  "valueTextColor": "yellow",
  "mainColor": "yellow",
  "secondaryColor": "red",
  "showProgress": true,
  "splitNumber": 4,
  "labelDecimalPlaces" : 2,
  "valueDecimalPlaces" : 2,
  "information": "Sıcaklık değeri için bilgi metni",
  "infoIconColor": "yellow",
  "criticalLow": 20,
  "criticalHigh": 80,
  "conditions": [
    {
      "conditionParamId": 117,
      "compareParamId": 118,
      "compareValue": "48.60",
      "operator": "eq",
      "fixedValue": "Hata durumu!",
      "isHidden": false,
      "isDisabled": false,
      "backgroundColor": "red",
      "andConditions": [
        {
          "conditionParamId": 123,
          "compareValue": "0V – 10V",
          "operator": "neq"
        }
      ]
    }
  ]
}
```


# `gradegauge` Nesnesi

Bu nesne, bir parametrenin dereceli göstergesini (grade gauge) ekranda göstermek için kullanılır. Farklı renk aralıkları ile değerlerin durumunu görsel olarak ifade eder.

---

## 🔧 Özellikler

| Alan Adı                | Tür           | Açıklama |
|-------------------------|---------------|----------|
| `object`                | string        | Nesne tipi, `"gradegauge"` olmalıdır. |
| `page`                  | number        | Gösterileceği sayfa numarası. |
| `row`                   | number        | Satır numarası. |
| `side`                  | string        | Ekranın hangi tarafında gösterileceği (`"left"`, `"right"`, `"center"`). |
| `width`                 | string        | Göstergenin genişliği (örn: `"200px"`). |
| `height`                | string        | Göstergenin yüksekliği (örn: `"190px"`). |
| `paramId`               | array[number] | Gösterilecek parametre ID'si listesi. |
| `nameFontSize`          | string        | Göstergenin adı yazı boyutu. |
| `nameIsBold`            | boolean       | Göstergenin adı kalın mı? |
| `nameIsItalic`          | boolean       | Göstergenin adı italik mi? |
| `nameColor`             | string        | Göstergenin adı rengi (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `valueTextColor`        | string        | Göstergedeki değer metni (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `valueTextSize`         | number        | Göstergedeki değer yazı boyutu. |
| `splitNumber`           | number        | Göstergedeki bölme sayısı (ölçeklendirme). |
| `labelDecimalPlaces`    | number       | Göstergedeki etiketlerin ondalık basamak sayısı. |
| `valueDecimalPlaces`    | number       | Göstergedeki değerin ondalık basamak sayısı. |
| `information`           | string        | Kullanıcıya gösterilecek bilgi mesajı. |
| `infoIconColor`         | string        | Bilgi ikonunun (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `criticalLow`           | number        | Kritik alt sınır değeri. |
| `criticalHigh`          | number        | Kritik üst sınır değeri. |
| `mainColor`             | string        | Göstergenin ana (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `colorRanges`           | array[array]  | Değer aralıklarına göre renk dizisi. Her eleman `[oran, renk]` formatında. Örneğin: `[0.3, "#67e0e3"]` |
| `conditions`            | array     | Koşullu formatlama için kullanılan koşullar dizisi. |

---

## 🧠 `conditions` (Koşullar)

Kartın görünümünü veya davranışını koşullara göre değiştirmek için kullanılır.

Her bir `condition` şu alanları içerir:

| Alan Adı             | Tür      | Açıklama |
|----------------------|----------|----------|
| `conditionParamId`   | number   | Koşulun uygulanacağı parametre ID'si. |
| `compareParamId`     | number   | Karşılaştırma yapılacak parametre ID'si (öncelik compareParamId karşılaştırmasıdır. compareParamId yok ise compareValue sabiti ile karşılaştırma yapar). |
| `compareValue`       | string   | Karşılaştırma yapılacak değer. |
| `operator`           | string   | Karşılaştırma operatörü. Desteklenen operatörler: `eq` (eşit), `neq` (eşit değil), `gt` (büyük), `lt` (küçük), `gte` (büyük veya eşit), `lte` (küçük veya eşit), `bitZero` (bit sıfır mı), `bitOne` (bit bir mi). |
| `fixedValue`         | string   | Koşul sağlanırsa gösterilecek sabit metin. |
| `isHidden`           | boolean  | Koşul sağlandığında kart gizlensin mi? |
| `isDisabled`         | boolean  | Koşul sağlandığında kart pasif olsun mu? |
| `backgroundColor`    | string   | Koşul sağlanırsa arka plan rengi ne olsun (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |

### 🔁 `andConditions` (Ek Koşullar)

Her bir `condition` içinde isteğe bağlı olarak `andConditions` tanımlanabilir.

| Alan Adı             | Tür      | Açıklama |
|----------------------|----------|----------|
| `conditionParamId`   | number   | Ek koşulun parametre ID'si. |
| `compareParamId`     | number   | Karşılaştırma yapılacak parametre ID'si (öncelik compareParamId karşılaştırmasıdır. compareParamId yok ise compareValue sabiti ile karşılaştırma yapar). |
| `compareValue`       | string   | Karşılaştırma değeri. |
| `operator`           | string   | Karşılaştırma operatörü. Desteklenen operatörler: `eq` (eşit), `neq` (eşit değil), `gt` (büyük), `lt` (küçük), `gte` (büyük veya eşit), `lte` (küçük veya eşit), `bitZero` (bit sıfır mı), `bitOne` (bit bir mi). |

---

## 🧪 Örnek `gradegauge` Nesnesi

```json
{
  "object": "gradegauge",
  "page": 1,
  "row": 1,
  "side": "center",
  "width": "200px",
  "height": "190px",
  "paramId": [95],
  "nameFontSize": "18px",
  "nameIsBold": false,
  "nameIsItalic": true,
  "nameColor": "var(--textPrimary)",
  "valueTextColor": "red",
  "valueTextSize": "24px",
  "splitNumber": 6,
  "labelDecimalPlaces" : 2,
  "valueDecimalPlaces" : 2,
  "information": "Sıcaklık değeri için bilgi metni",
  "infoIconColor": "yellow",
  "criticalLow": 20,
  "criticalHigh": 80,
  "mainColor": "yellow",
  "colorRanges": [
    [0.3, "#67e0e3"],
    [0.7, "#37a2da"],
    [1, "#fd666d"]
  ],
  "conditions": [
    {
      "conditionParamId": 117,
      "compareParamId": 118,
      "compareValue": "48.60",
      "operator": "eq",
      "fixedValue": "Hata durumu!",
      "isHidden": false,
      "isDisabled": false,
      "backgroundColor": "red",
      "andConditions": [
        {
          "conditionParamId": 123,
          "compareValue": "0V – 10V",
          "operator": "neq"
        }
      ]
    }
  ]
}
```

# `bargauge` Nesnesi

Bu nesne, değerleri segment bazlı bar/gauge olarak gösteren bir göstergedir. Dikey veya yatay olarak düzenlenebilir, kare veya daire şeklinde segmentlerle değer görselleştirmesi yapar. Min-max değer aralığına göre segmentler renk gradyanı ile dolar.

---

## 🔧 Özellikler

| Alan Adı              | Tür             | Açıklama |
|-----------------------|-----------------|----------|
| `object`              | string          | Nesne tipi, `"bargauge"` olmalıdır. |
| `page`                | number          | Gösterileceği sayfa numarası. |
| `row`                 | number          | Satır numarası. |
| `side`                | string          | Ekranın hangi tarafında gösterileceği (`"left"`, `"right"`, `"center"`). |
| `width`               | string          | Bileşenin genişliği (örn: `"100px"`). Belirtilmezse içeriğe göre otomatik ayarlanır. |
| `height`              | string          | Bileşenin yüksekliği (örn: `"400px"`). Belirtilmezse içeriğe göre otomatik ayarlanır. |
| `title`               | string          | Gösterge başlığı. Belirtilmezse parametre adı kullanılır. Boş string (`""`) verilirse başlık gösterilmez. |
| `titleFontSize`       | string          | Başlık yazı boyutu (örn: `"16px"`). Varsayılan: `"16px"`. |
| `titleIsBold`         | boolean         | Başlık kalın mı? Varsayılan: `true`. |
| `titleIsItalic`       | boolean         | Başlık italik mi? Varsayılan: `false`. |
| `titleColor`          | string          | Başlık rengi (renk ismi, hex kodu veya CSS değişkeni, örn: `"red"`, `"#ff0000"`, `"var(--textPrimary)"`). |
| `paramId`             | array[number]   | Gösterilecek parametre ID'leri dizisi. Her paramId için ayrı bir bargauge oluşturulur (örn: `[100]` veya `[100, 101]`). |
| `minValue`            | number          | Minimum değer. Belirtilmezse parametrenin minValue'su kullanılır. Varsayılan: `0`. |
| `maxValue`            | number          | Maksimum değer. Belirtilmezse parametrenin maxValue'su kullanılır. Varsayılan: `100`. |
| `segmentCount`        | number          | Toplam segment sayısı. Varsayılan: `10`. |
| `orientation`         | string          | Gösterge yönü: `"vertical"` (dikey) veya `"horizontal"` (yatay). Varsayılan: `"vertical"`. |
| `shape`               | string          | Segment şekli: `"square"` (kare) veya `"circle"` (daire). Varsayılan: `"square"`. |
| `segmentSize`         | string          | Her bir segmentin boyutu (örn: `"30px"`). Varsayılan: `"30px"`. |
| `segmentSpacing`      | string          | Segmentler arası boşluk (örn: `"5px"`). Varsayılan: `"5px"`. |
| `startColor`          | string          | Başlangıç rengi (minimum değer tarafı). Renk ismi, hex veya rgb formatı (örn: `"yellow"`, `"#ffeb3b"`, `"rgb(255,235,59)"`). Varsayılan: `"#ffeb3b"`. |
| `endColor`            | string          | Bitiş rengi (maksimum değer tarafı). Renk ismi, hex veya rgb formatı (örn: `"red"`, `"#f44336"`, `"rgb(244,67,54)"`). Varsayılan: `"#f44336"`. |
| `emptyColor`          | string          | Boş segmentlerin rengi. Varsayılan: `"#e0e0e0"`. |
| `showValue`           | boolean         | Değer gösterimi aktif mi? Varsayılan: `true`. |
| `valueFontSize`       | string          | Değer yazı boyutu (örn: `"14px"`). Varsayılan: `"14px"`. |
| `valueColor`          | string          | Değer yazı rengi. Varsayılan: `"var(--textPrimary)"`. |


---

## 🧪 Örnek `bargauge` Nesnesi

```json
{
  "object": "bargauge",
  "page": 1,
  "row": 1,
  "side": "center",
  "width": "100px",
  "height": "350px",
  "title": "Fuel Level",
  "titleFontSize": "16px",
  "titleIsBold": true,
  "titleColor": "var(--textPrimary)",
  "paramId": [105],
  "minValue": 0,
  "maxValue": 100,
  "segmentCount": 10,
  "orientation": "vertical",
  "shape": "square",
  "segmentSize": "20px",
  "segmentSpacing": "4px",
  "startColor": "#ffeb3b",
  "endColor": "#f44336",
  "emptyColor": "#396387",
  "showValue": true,
  "valueFontSize": "14px",
  "valueColor": "var(--textPrimary)"
}
```

# `fillbargauge` Nesnesi

Bu nesne, değerleri tek bir bar içinde gradient dolgu ile gösteren bir göstergedir. Dikey veya yatay olarak düzenlenebilir ve isteğe bağlı seviye çizgileri ile görselleştirme yapılabilir. Min-max değer aralığına göre bar renk gradyanı ile dolar.

---

## 🔧 Özellikler

| Alan Adı              | Tür             | Açıklama |
|-----------------------|-----------------|----------|
| `object`              | string          | Nesne tipi, `"fillbargauge"` olmalıdır. |
| `page`                | number          | Gösterileceği sayfa numarası. |
| `row`                 | number          | Satır numarası. |
| `side`                | string          | Ekranın hangi tarafında gösterileceği (`"left"`, `"right"`, `"center"`). |
| `width`               | string          | Bileşenin genişliği (örn: `"100px"`). Belirtilmezse içeriğe göre otomatik ayarlanır. |
| `height`              | string          | Bileşenin yüksekliği (örn: `"400px"`). Belirtilmezse içeriğe göre otomatik ayarlanır. |
| `title`               | string          | Gösterge başlığı. Belirtilmezse parametre adı kullanılır. Boş string (`""`) verilirse başlık gösterilmez. |
| `titleFontSize`       | string          | Başlık yazı boyutu (örn: `"16px"`). Varsayılan: `"16px"`. |
| `titleIsBold`         | boolean         | Başlık kalın mı? Varsayılan: `true`. |
| `titleIsItalic`       | boolean         | Başlık italik mi? Varsayılan: `false`. |
| `titleColor`          | string          | Başlık rengi (renk ismi, hex kodu veya CSS değişkeni, örn: `"red"`, `"#ff0000"`, `"var(--textPrimary)"`). |
| `paramId`             | array[number]   | Gösterilecek parametre ID'leri dizisi. Her paramId için ayrı bir fillbargauge oluşturulur (örn: `[100]` veya `[100, 101]`). |
| `minValue`            | number          | Minimum değer. Belirtilmezse parametrenin minValue'su kullanılır. Varsayılan: `0`. |
| `maxValue`            | number          | Maksimum değer. Belirtilmezse parametrenin maxValue'su kullanılır. Varsayılan: `100`. |
| `orientation`         | string          | Gösterge yönü: `"vertical"` (dikey) veya `"horizontal"` (yatay). Varsayılan: `"vertical"`. |
| `shape`               | string          | Bar şekli: `"square"` (köşeli) veya `"rounded"` (yuvarlatılmış köşeler). Varsayılan: `"square"`. |
| `barThickness`        | string          | Bar kalınlığı (örn: `"40px"`). Varsayılan: `"40px"`. |
| `borderRadius`        | string          | Köşe yuvarlaklığı (örn: `"8px"`, `"30px"`). Varsayılan: `"8px"`. |
| `startColor`          | string          | Başlangıç rengi (minimum değer tarafı). Renk ismi, hex veya rgb formatı (örn: `"yellow"`, `"#ffeb3b"`, `"rgb(255,235,59)"`). Varsayılan: `"#ffeb3b"`. |
| `endColor`            | string          | Bitiş rengi (maksimum değer tarafı). Renk ismi, hex veya rgb formatı (örn: `"green"`, `"#4caf50"`, `"rgb(76,175,80)"`). Varsayılan: `"#f44336"`. |
| `emptyColor`          | string          | Boş alanın rengi. Varsayılan: `"#396387"`. |
| `showValue`           | boolean         | Değer gösterimi aktif mi? Varsayılan: `true`. |
| `valueFontSize`       | string          | Değer yazı boyutu (örn: `"14px"`). Varsayılan: `"14px"`. |
| `valueColor`          | string          | Değer yazı rengi. Varsayılan: `"var(--textPrimary)"`. |
| `levelLines`          | number          | Seviye çizgisi sayısı. `0` veya belirtilmezse çizgi gösterilmez. Örn: `4` → 4 eşit aralıklı çizgi. Varsayılan: `0`. |
| `levelLineColor`      | string          | Seviye çizgilerinin rengi. Varsayılan: `"rgba(0, 0, 0, 0.3)"`. |
| `levelLineThickness`  | string          | Seviye çizgilerinin kalınlığı (örn: `"1px"`, `"2px"`). Varsayılan: `"1px"`. |

---

## 🧪 Örnek `fillbargauge` Nesneleri

```json
{
  "object": "fillbargauge",
  "page": 1,
  "row": 1,
  "side": "center",
  "width": "100px",
  "height": "400px",
  "title": "Fuel Level",
  "paramId": [109],
  "minValue": 0,
  "maxValue": 100,
  "orientation": "vertical",
  "shape": "square",
  "barThickness": "40px",
  "borderRadius": "30px",
  "startColor": "#ffeb3b",
  "endColor": "green",
  "emptyColor": "#396387",
  "showValue": true,
  "levelLines": 4,
  "levelLineColor": "#88A1B7",
  "levelLineThickness": "1px"
}
```

# `temperaturegauge` Nesnesi

Bu nesne, sıcaklık değerlerini görsel olarak göstermek için kullanılan özel bir gösterge türüdür. Kritik sıcaklık aralıkları renklerle belirtilir.

---

## 🔧 Özellikler

| Alan Adı                | Tür           | Açıklama |
|-------------------------|---------------|----------|
| `object`                | string        | Nesne tipi, `"temperaturegauge"` olmalıdır. |
| `page`                  | number        | Gösterileceği sayfa numarası. |
| `row`                   | number        | Satır numarası. |
| `side`                  | string        | Ekranın hangi tarafında gösterileceği (`"left"`, `"right"`, `"center"`). |
| `width`                 | string        | Göstergenin genişliği (örn: `"200px"`). |
| `height`                | string        | Göstergenin yüksekliği (örn: `"220px"`). |
| `paramId`               | array[number] | Gösterilecek parametre ID'si listesi. |
| `nameFontSize`          | string        | Göstergenin adı yazı boyutu. |
| `nameIsBold`            | boolean       | Göstergenin adı kalın mı? |
| `nameIsItalic`          | boolean       | Göstergenin adı italik mi? |
| `nameColor`             | string        | Göstergenin adı rengi (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `color`                 | array[string] | Sıcaklık aralıklarında kullanılacak renkler (örn: `["#c53d3d", "#891111"]`). |
| `criticalLow`           | number        | Kritik alt sıcaklık sınırı. |
| `criticalHigh`          | number        | Kritik üst sıcaklık sınırı. |
| `valueTextSize`         | string        | Gösterge üzerindeki değer yazı boyutu. |
| `valueTextColor`        | string        | Gösterge üzerindeki değer (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `information`           | string        | Kullanıcıya gösterilecek bilgi metni. |
| `infoIconColor`         | string        | Bilgi ikonunun (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `splitNumber`           | number        | Gösterge üzerindeki bölme sayısı (ölçeklendirme). |
| `labelDecimalPlaces`    | number       | Göstergedeki etiketlerin ondalık basamak sayısı. |
| `valueDecimalPlaces`    | number       | Göstergedeki değerin ondalık basamak sayısı. |

---

## 🧪 Örnek `temperaturegauge` Nesnesi

```json
{
  "object": "temperaturegauge",
  "page": 1,
  "row": 1,
  "side": "center",
  "width": "200px",
  "height": "190px",
  "paramId": [95],
  "nameFontSize": "18px",
  "nameIsBold": false,
  "nameIsItalic": true,
  "nameColor": "var(--textPrimary)",
  "color": ["#c53d3d", "#891111"],
  "criticalLow": 20,
  "criticalHigh": 80,
  "valueTextSize": "24px",
  "valueTextColor": "red",
  "information": "Sıcaklık değeri için bilgi metni",
  "infoIconColor": "yellow",
  "splitNumber": 6,
  "labelDecimalPlaces" : 2,
  "valueDecimalPlaces" : 2
}
```


# `pressuregauge` Nesnesi

Bu nesne, basınç değerlerini görsel olarak göstermek için kullanılan bir gösterge türüdür. Kritik sınırlar ve renklerle değerlerin durumu belirtilir.

---

## 🔧 Özellikler

| Alan Adı                | Tür           | Açıklama |
|-------------------------|---------------|----------|
| `object`                | string        | Nesne tipi, `"pressuregauge"` olmalıdır. |
| `page`                  | number        | Gösterileceği sayfa numarası. |
| `row`                   | number        | Satır numarası. |
| `side`                  | string        | Ekranın hangi tarafında gösterileceği (`"left"`, `"right"`, `"center"`). |
| `width`                 | string        | Göstergenin genişliği (örn: `"200px"`). |
| `height`                | string        | Göstergenin yüksekliği (örn: `"220px"`). |
| `paramId`               | array[number] | Gösterilecek parametre ID'si listesi. |
| `nameFontSize`          | string        | Göstergenin adı yazı boyutu. |
| `nameIsBold`            | boolean       | Göstergenin adı kalın mı? |
| `nameIsItalic`          | boolean       | Göstergenin adı italik mi? |
| `nameColor`             | string        | Göstergenin adı rengi (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `criticalLow`           | number        | Kritik alt sınır değeri. |
| `criticalHigh`          | number        | Kritik üst sınır değeri. |
| `valueTextSize`         | string        | Gösterge üzerindeki değer yazı boyutu. |
| `valueTextColor`        | string        | Gösterge üzerindeki değer (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `mainColor`             | string        | Göstergenin ana (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `secondaryColor`        | string        | Göstergenin ikincil (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `information`           | string        | Kullanıcıya gösterilecek bilgi metni. |
| `infoIconColor`         | string        | Bilgi ikonunun (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `splitNumber`           | number        | Gösterge üzerindeki bölme sayısı (ölçeklendirme). |
| `labelDecimalPlaces`    | number       | Göstergedeki etiketlerin ondalık basamak sayısı. |
| `valueDecimalPlaces`    | number       | Göstergedeki değerin ondalık basamak sayısı. |

---

## 🧪 Örnek `pressuregauge` Nesnesi

```json
{
  "object": "pressuregauge",
  "page": 1,
  "row": 1,
  "side": "center",
  "width": "200px",
  "height": "190px",
  "paramId": [95],
  "nameFontSize": "18px",
  "nameIsBold": false,
  "nameIsItalic": true,
  "nameColor": "var(--textPrimary)",
  "criticalLow": 20,
  "criticalHigh": 80,
  "valueTextSize": "24px",
  "valueTextColor": "white",
  "mainColor": "yellow",
  "secondaryColor": "red",
  "information": "Sıcaklık değeri için bilgi metni",
  "infoIconColor": "yellow",
  "splitNumber": 6,
  "labelDecimalPlaces" : 2,
  "valueDecimalPlaces" : 2
}
```


# `thermometer` Nesnesi

Bu nesne, sıcaklık değerlerini termometre şeklinde görsel olarak göstermek için kullanılır. Kritik seviyeler, renk geçişleri ve animasyonlar desteklenir.

---

## 🔧 Özellikler

| Alan Adı            | Tür           | Açıklama |
|---------------------|---------------|----------|
| `object`            | string        | Nesne tipi, `"thermometer"` olmalıdır. |
| `page`              | number        | Gösterileceği sayfa numarası. |
| `row`               | number        | Satır numarası. |
| `side`              | string        | Ekranın hangi tarafında gösterileceği (`"left"`, `"right"`, `"center"`). |
| `width`             | string        | Termometrenin genişliği (örn: `"160px"`). |
| `height`            | string        | Termometrenin yüksekliği (örn: `"260px"`). |
| `paramId`           | array[number] | Gösterilecek parametre ID'si listesi. |
| `nameFontSize`      | string        | Termometre adı yazı boyutu. |
| `nameIsBold`        | boolean       | Termometre adı kalın mı? |
| `nameIsItalic`      | boolean       | Termometre adı italik mi? |
| `nameColor`         | string        | Termometre adı rengi (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `information`       | string        | Kullanıcıya gösterilecek bilgi metni. |
| `infoIconColor`     | string        | Bilgi ikonunun (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `thermometerColor`  | string        | Termometrenin ana (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `fillStartColor`    | string        | Termometre dolumunun başlangıç (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `fillEndColor`      | string        | Termometre dolumunun bitiş (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `valueTextSize`     | string        | Değer metni yazı boyutu. |
| `rangeTextSize`     | string        | Aralık metni yazı boyutu. |
| `valueTextColor`    | string        | Değer metni (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `rangeTextColor`    | string        | Aralık metni (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `thermometerWidth`  | string        | Termometre gövde genişliği. |
| `bulbSize`          | string        | Termometrenin alt kısmındaki ampul boyutu. |
| `criticalLow`       | number        | Kritik alt sıcaklık değeri. |
| `criticalHigh`      | number        | Kritik üst sıcaklık değeri. |
| `showRanges`        | boolean       | Aralıkların gösterilip gösterilmeyeceği. |
| `highRange`         | number        | Yüksek sıcaklık aralığı sınırı. |
| `midRange`          | number        | Orta sıcaklık aralığı sınırı. |
| `lowRange`          | number        | Düşük sıcaklık aralığı sınırı. |
| `lowerRange`        | number        | En düşük sıcaklık aralığı sınırı. |

---

## 🧪 Örnek `thermometer` Nesnesi

```json
{
  "object": "thermometer",
  "page": 1,
  "row": 1,
  "side": "center",
  "height": "260px",
  "width": "160px",
  "paramId": [95],
  "nameFontSize": "18px",
  "nameIsBold": true,
  "nameIsItalic": true,
  "nameColor": "var(--textPrimary)",
  "information": "Sıcaklık değeri için bilgi metni",
  "infoIconColor": "var(--textPrimary)",
  "thermometerColor": "var(--textPrimary)",
  "fillStartColor": "#2196F3",
  "fillEndColor": "#891111",
  "valueTextSize": "24px",
  "rangeTextSize": "12px",
  "valueTextColor": "var(--textPrimary)",
  "rangeTextColor": "var(--textPrimary)",
  "thermometerWidth": "20px",
  "bulbSize": "30px",
  "criticalLow": 20,
  "criticalHigh": 80,
  "showRanges": true,
  "highRange": 90,
  "midRange": 70,
  "lowRange": 50,
  "lowerRange": 30
}
```


# `fueltank` Nesnesi

Bu nesne, yakıt deposu seviyesini görsel olarak göstermek için kullanılır. Kritik seviyeler ve renklerle yakıt durumunu ifade eder.

---

## 🔧 Özellikler

| Alan Adı          | Tür           | Açıklama |
|-------------------|---------------|----------|
| `object`          | string        | Nesne tipi, `"fueltank"` olmalıdır. |
| `page`            | number        | Gösterileceği sayfa numarası. |
| `row`             | number        | Satır numarası. |
| `side`            | string        | Ekranın hangi tarafında gösterileceği (`"left"`, `"right"`, `"center"`). |
| `width`           | string        | Göstergenin genişliği (örn: `"180px"`). |
| `height`          | string        | Göstergenin yüksekliği (örn: `"180px"`). |
| `paramId`         | array[number] | Gösterilecek parametre ID'si listesi. |
| `nameFontSize`    | string        | Ad yazı boyutu. |
| `nameIsBold`      | boolean       | Ad kalın mı? |
| `nameIsItalic`    | boolean       | Ad italik mi? |
| `nameColor`       | string        | Ad rengi (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `valueTextSize`   | string        | Değer yazı boyutu. |
| `valueTextColor`  | string        | Değer (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `information`     | string        | Kullanıcıya gösterilecek bilgi metni. |
| `infoIconColor`   | string        | Bilgi ikonunun (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `criticalLow`     | number        | Kritik alt seviye. |
| `criticalHigh`    | number        | Kritik üst seviye. |
| `tankColor`       | string        | Depo ana (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `level4Color`     | string        | Seviye 4 rengi (yüksek seviye). |
| `level3Color`     | string        | Seviye 3 (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `level2Color`     | string        | Seviye 2 (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `level1Color`     | string        | Seviye 1 rengi (düşük seviye). |

---

## 🧪 Örnek `fueltank` Nesnesi

```json
{
  "object": "fueltank",
  "page": 1,
  "row": 1,
  "side": "center",
  "height": "260px",
  "width": "160px",
  "paramId": [95],
  "nameFontSize": "18px",
  "nameIsBold": false,
  "nameIsItalic": true,
  "nameColor": "var(--textPrimary)",
  "valueTextSize": "24px",
  "valueTextColor": "red",
  "information": "Sıcaklık değeri için bilgi metni",
  "infoIconColor": "yellow",
  "criticalLow": 60,
  "criticalHigh": 80,
  "tankColor": "red",
  "level4Color": "green",
  "level3Color": "blue",
  "level2Color": "orange",
  "level1Color": "yellow"
}
```


# `airtank` Nesnesi

Bu nesne, hava tankı seviyesini görsel olarak göstermek için kullanılır. Kritik seviyeler ve renklerle hava basıncı durumu ifade edilir.  
Ayrıca tankın doluluk durumuna göre **opacity** (saydamlık) değerleri ayarlanarak görsel yoğunluk değiştirilebilir.


---

## 🔧 Özellikler

| Alan Adı          | Tür           | Açıklama |
|-------------------|---------------|----------|
| `object`          | string        | Nesne tipi, `"airtank"` olmalıdır. |
| `page`            | number        | Gösterileceği sayfa numarası. |
| `row`             | number        | Satır numarası. |
| `side`            | string        | Ekranın hangi tarafında gösterileceği (`"left"`, `"right"`, `"center"`). |
| `width`           | string        | Göstergenin genişliği (örn: `"180px"`). |
| `height`          | string        | Göstergenin yüksekliği (örn: `"180px"`). |
| `paramId`         | array[number] | Gösterilecek parametre ID'si listesi. |
| `nameFontSize`    | string        | Ad yazı boyutu. |
| `nameIsBold`      | boolean       | Ad kalın mı? |
| `nameIsItalic`    | boolean       | Ad italik mi? |
| `nameColor`       | string        | Ad rengi (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `valueTextSize`   | string        | Değer yazı boyutu. |
| `valueTextColor`  | string        | Değer (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `information`     | string        | Kullanıcıya gösterilecek bilgi metni. |
| `infoIconColor`   | string        | Bilgi ikonunun (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `criticalLow`     | number        | Kritik alt seviye. |
| `criticalHigh`    | number        | Kritik üst seviye. |
| `tankColor`       | string        | Tankın ana (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `mainColor`       | string        | Gösterge ana (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |

---

## 🧪 Örnek `airtank` Nesnesi

```json
{
  "object": "airtank",
  "page": 1,
  "row": 1,
  "side": "center",
  "height": "180px",
  "width": "180px",
  "paramId": [95],
  "nameFontSize": "18px",
  "nameIsBold": false,
  "nameIsItalic": true,
  "nameColor": "var(--textPrimary)",
  "valueTextSize": "24px",
  "valueTextColor": "blue",
  "information": "Sıcaklık değeri için bilgi metni",
  "infoIconColor": "yellow",
  "criticalLow": 20,
  "criticalHigh": 80,
  "tankColor": "red",
  "mainColor": "yellow"
}
```


# `ledindicator` Nesnesi

Bu nesne, LED göstergeler grubunu temsil eder. Her bir LED farklı koşullara bağlı olarak farklı renk ve durumlarda yanabilir veya yanıp sönebilir.

---

## 🔧 Özellikler

| Alan Adı              | Tür             | Açıklama |
|-----------------------|-----------------|----------|
| `object`              | string          | Nesne tipi, `"ledindicator"` olmalıdır. |
| `page`                | number          | Gösterileceği sayfa numarası. |
| `row`                 | number          | Satır numarası. |
| `side`                | string          | Ekranın hangi tarafında gösterileceği (`"left"`, `"right"`, `"center"`). |
| `width`               | string          | Bileşenin genişliği (örn: `"300px"`). |
| `height`              | string          | Bileşenin yüksekliği (örn: `"400px"`). |
| `title`               | string          | Gösterge grubunun başlığı. |
| `titleFontSize`       | string          | Başlık yazı boyutu. |
| `titleIsBold`         | boolean         | Başlık kalın mı? |
| `titleIsItalic`       | boolean         | Başlık italik mi? |
| `titleColor`          | string          | Başlık (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `itemFontSize`        | string          | LED öğelerinin yazı boyutu. |
| `showItemBorder`      | boolean         | LED öğelerinin etrafında çerçeve gösterilsin mi? |
| `hideIfNoConditions`  | boolean         | Koşul yoksa tüm grup gizlensin mi? |
| `itemList`            | array[object]   | LED öğelerinin listesi. |

### `itemList` içindeki her öğe için özellikler:

| Alan Adı          | Tür             | Açıklama |
|-------------------|-----------------|----------|
| `name`            | string          | LED öğesinin adı. |
| `nameParamId`     | number          | Item isminin hangi parametre değerinden alınacağı. Ayrıca üzerine tıklama ile ilgili parametre set sayfasının açılması. |
| `nameIsBold`      | boolean         | Ad kalın mı? |
| `nameIsItalic`    | boolean         | Ad italik mi? |
| `nameColor`       | string          | Ad (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `information`     | string          | Kullanıcıya gösterilecek bilgi metni. |
| `infoIconColor`   | string          | Bilgi ikonunun (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `conditions`      | array[object]   | LED'in durumu için koşullar listesi. |

### `conditions` içindeki her koşul için özellikler:

| Alan Adı          | Tür             | Açıklama |
|-------------------|-----------------|----------|
| `conditionParamId`| number          | Koşulun bağlı olduğu parametre ID'si. |
| `compareParamId`     | number   | Karşılaştırma yapılacak parametre ID'si (öncelik compareParamId karşılaştırmasıdır. compareParamId yok ise compareValue sabiti ile karşılaştırma yapar). |
| `compareValue`    | string/number   | Karşılaştırılacak değer. |
| `operator`        | string          | Karşılaştırma operatörü. Desteklenen operatörler: `eq` (eşit), `neq` (eşit değil), `gt` (büyük), `lt` (küçük), `gte` (büyük veya eşit), `lte` (küçük veya eşit), `bitZero` (bit sıfır mı), `bitOne` (bit bir mi). |
| `color`           | string          | LED rengi (aktif olduğunda). |
| `isOn`            | boolean         | LED'in yanıp yanmadığını belirtir (true = açık). |
| `isBlinking`      | boolean         | LED yanıp sönüyor mu? |
| `andConditions`   | array[object]   | Ek koşullar (ve mantığı ile). |

---

### 🔁 `andConditions` (Ek Koşullar)

Her bir `condition` içinde isteğe bağlı olarak `andConditions` tanımlanabilir.

| Alan Adı             | Tür      | Açıklama |
|----------------------|----------|----------|
| `conditionParamId`   | number   | Ek koşulun parametre ID'si .|
| `compareParamId`     | number   | Karşılaştırma yapılacak parametre ID'si (öncelik compareParamId karşılaştırmasıdır. compareParamId yok ise compareValue sabiti ile karşılaştırma yapar). |
| `compareValue`       | string   | Karşılaştırma değeri. |
| `operator`           | string   | Karşılaştırma operatörü. Desteklenen operatörler: `eq` (eşit), `neq` (eşit değil), `gt` (büyük), `lt` (küçük), `gte` (büyük veya eşit), `lte` (küçük veya eşit), `bitZero` (bit sıfır mı), `bitOne` (bit bir mi). |

---

## 🧪 Örnek `ledindicator` Nesnesi

```json
{
  "object": "ledindicator",
  "page": 1,
  "row": 3,
  "side": "center",
  "width": "300px",
  "height": "400px",
  "title": "Motor Durum LEDleri",
  "titleFontSize": "18px",
  "titleIsBold": true,
  "titleIsItalic": false,
  "titleColor": "yellow",
  "itemFontSize": "14px",
  "showItemBorder": true,
  "hideIfNoConditions": false,
  "itemList": [
    {
      "name": "Motor Durum-1",
      "nameParamId" : 169,
      "nameIsBold": true,
      "nameIsItalic": false,
      "nameColor": "#444444",
      "information": "Motor çalışma durumu göstergesi",
      "infoIconColor": "yellow",
      "conditions": [
        {
          "conditionParamId": 43,
          "compareValue": "1",
          "operator": "eq",
          "color": "blue",
          "isOn": true,
          "isBlinking": false,
          "andConditions": [
            {
              "conditionParamId": 95,
              "compareValue": "58",
              "operator": "neq"
            }
          ]
        },
        {
          "conditionParamId": 42,
          "compareValue": "2",
          "operator": "eq",
          "color": "#4CAF50",
          "isOn": true,
          "isBlinking": false
        }
      ]
    },
    {
      "name": "Motor Durum-2",
      "nameIsBold": false,
      "nameIsItalic": false,
      "nameColor": "#444444",
      "information": "Motor uyarı göstergesi",
      "conditions": [
        {
          "conditionParamId": 95,
          "compareValue": 90,
          "operator": "gte",
          "color": "#FFC107",
          "isOn": true,
          "isBlinking": true
        }
      ]
    }
  ]
}
```

# `ledioindicator` Nesnesi

Bu nesne, LED göstergeler grubunu temsil eder. LED'ler yan yana dizilir ve her LED farklı koşullara bağlı olarak farklı renk ve durumlarda yanabilir veya yanıp sönebilir. LED isimleri görünmez, sadece fare üzerine geldiğinde tooltip olarak gösterilir.

---

## 🔧 Özellikler

| Alan Adı              | Tür             | Açıklama |
|-----------------------|-----------------|----------|
| `object`              | string          | Nesne tipi, `"ledioindicator"` olmalıdır. |
| `page`                | number          | Gösterileceği sayfa numarası. |
| `row`                 | number          | Satır numarası. |
| `side`                | string          | Ekranın hangi tarafında gösterileceği (`"left"`, `"right"`, `"center"`). |
| `width`               | string          | Bileşenin genişliği (örn: `"300px"`). Belirtilmezse içeriğe göre otomatik ayarlanır. |
| `height`              | string          | Bileşenin yüksekliği (örn: `"100px"`). Belirtilmezse içeriğe göre otomatik ayarlanır. |
| `title`               | string          | Gösterge grubunun başlığı. |
| `titleFontSize`       | string          | Başlık yazı boyutu (örn: `"16px"`). |
| `titleIsBold`         | boolean         | Başlık kalın mı? |
| `titleIsItalic`       | boolean         | Başlık italik mi? |
| `titleColor`          | string          | Başlık rengi (renk ismi, hex kodu veya CSS değişkeni, örn: `"red"`, `"#ff0000"`, `"var(--textPrimary)"`). |
| `ledSize`             | string          | LED boyutu (örn: `"20px"`). |
| `ledSpacing`          | string          | LED'ler arası boşluk (örn: `"10px"`). |
| `ledsPerRow`          | number          | Her satırda gösterilecek maksimum LED sayısı. |
| `tooltipFontSize`     | string          | Tooltip yazı boyutu (örn: `"12px"`). |
| `hideIfNoConditions`  | boolean         | Koşul yoksa LED gizlensin mi? |
| `itemList`            | array[object]   | LED öğelerinin listesi. |

### `itemList` içindeki her öğe için özellikler:

| Alan Adı          | Tür             | Açıklama |
|-------------------|-----------------|----------|
| `name`            | string          | LED öğesinin adı (tooltip olarak gösterilir). |
| `conditions`      | array[object]   | LED'in durumu için koşullar listesi. |

### `conditions` içindeki her koşul için özellikler:

| Alan Adı          | Tür             | Açıklama |
|-------------------|-----------------|----------|
| `conditionParamId`         | number          | Koşulun bağlı olduğu parametre ID'si. |
| `compareParamId`  | number          | Karşılaştırma yapılacak parametre ID'si (öncelik compareParamId karşılaştırmasıdır. compareParamId yok ise compareValue sabiti ile karşılaştırma yapar). |
| `compareValue`    | string/number   | Karşılaştırılacak değer. |
| `operator`        | string          | Karşılaştırma operatörü. Desteklenen operatörler: `eq` (eşit), `neq` (eşit değil), `gt` (büyük), `lt` (küçük), `gte` (büyük veya eşit), `lte` (küçük veya eşit), `bitZero` (bit sıfır mı), `bitOne` (bit bir mi). |
| `color`           | string          | LED rengi (aktif olduğunda). |
| `isOn`            | boolean         | LED'in yanıp yanmadığını belirtir (true = açık). |
| `isBlinking`      | boolean         | LED yanıp sönüyor mu? |
| `andConditions`   | array[object]   | Ek koşullar (ve mantığı ile). |

---

### 🔁 `andConditions` (Ek Koşullar)

Her bir `condition` içinde isteğe bağlı olarak `andConditions` tanımlanabilir.

| Alan Adı             | Tür      | Açıklama |
|----------------------|----------|----------|
| `conditionParamId`            | number   | Ek koşulun parametre ID'si. |
| `compareParamId`     | number   | Karşılaştırma yapılacak parametre ID'si (öncelik compareParamId karşılaştırmasıdır. compareParamId yok ise compareValue sabiti ile karşılaştırma yapar). |
| `compareValue`       | string   | Karşılaştırma değeri. |
| `operator`           | string   | Karşılaştırma operatörü. Desteklenen operatörler: `eq` (eşit), `neq` (eşit değil), `gt` (büyük), `lt` (küçük), `gte` (büyük veya eşit), `lte` (küçük veya eşit), `bitZero` (bit sıfır mı), `bitOne` (bit bir mi). |

---

## 🧪 Örnek `ledioindicator` Nesnesi
```json
{
  "object": "ledioindicator",
  "page": 1,
  "row": 2,
  "side": "center",
  "width": "400px",
  "height": "150px",
  "title": "Digital Inputs",
  "titleFontSize": "16px",
  "titleIsBold": true,
  "titleIsItalic": false,
  "titleColor": "var(--textPrimary)",
  "ledSize": "25px",
  "ledSpacing": "15px",
  "ledsPerRow": 8,
  "tooltipFontSize": "12px",
  "hideIfNoConditions": false,
  "itemList": [
    {
      "name": "DI 1",
      "conditions": [
        {
          "conditionParamId": 100,
          "compareValue": "1",
          "operator": "eq",
          "color": "#00ff00",
          "isOn": true,
          "isBlinking": false
        }
      ]
    },
    {
      "name": "DI 2",
      "conditions": [
        {
          "conditionParamId": 101,
          "compareValue": "1",
          "operator": "eq",
          "color": "#ff0000",
          "isOn": true,
          "isBlinking": true,
          "andConditions": [
            {
              "conditionParamId": 102,
              "compareValue": "0",
              "operator": "eq"
            }
          ]
        }
      ]
    },
    {
      "name": "DI 3",
      "conditions": [
        {
          "conditionParamId": 103,
          "compareValue": "1",
          "operator": "eq",
          "color": "#0000ff",
          "isOn": true,
          "isBlinking": false
        }
      ]
    },
    {
      "name": "DO 1",
      "conditions": [
        {
          "conditionParamId": 200,
          "compareValue": "1",
          "operator": "eq",
          "color": "#ffff00",
          "isOn": true,
          "isBlinking": false
        }
      ]
    }
  ]
}
```

# `text` Nesnesi

Bu nesne, statik veya koşullu metinlerin gösterimi için kullanılır. Metin görünümü ve koşullara bağlı değişimleri destekler.

---

## 🔧 Özellikler

| Alan Adı          | Tür             | Açıklama |
|-------------------|-----------------|----------|
| `object`          | string          | Nesne tipi, `"text"` olmalıdır. |
| `page`            | number          | Gösterileceği sayfa numarası. |
| `row`             | number          | Satır numarası. |
| `side`            | string          | Ekranın hangi tarafında gösterileceği (`"left"`, `"right"`, `"center"`). |
| `width`           | string          | Metin alanının genişliği (örn: `"100px"`). |
| `height`          | string          | Metin alanının yüksekliği (örn: `"100px"`). |
| `name`            | string          | Başlık veya metin adı. |
| `nameFontSize`    | string          | Başlık yazı boyutu. |
| `nameIsBold`      | boolean         | Başlık kalın mı? |
| `nameIsItalic`    | boolean         | Başlık italik mi? |
| `nameColor`       | string          | Başlık (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `text`            | string          | Gösterilecek varsayılan metin. |
| `valueColor`      | string          | Metin (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `valueFontSize`   | string          | Metin yazı boyutu. |
| `valueIsBold`     | boolean         | Metin kalın mı? |
| `valueIsItalic`   | boolean         | Metin italik mi? |
| `backgroundColor` | string          | Arka plan rengi (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `isBlinking`      | boolean         | Metin yanıp sönüyor mu? |
| `conditions`      | array[object]   | Metin içeriği ve stilini koşullara göre değiştiren liste. |

### `conditions` içindeki her koşul için özellikler:

| Alan Adı          | Tür             | Açıklama |
|-------------------|-----------------|----------|
| `conditionParamId`| number          | Koşulun bağlı olduğu parametre ID'si. |
| `compareValue`    | string/number   | Karşılaştırılacak değer. |
| `operator`         | string          | Karşılaştırma operatörü. Desteklenen operatörler: `eq` (eşit), `neq` (eşit değil), `gt` (büyük), `lt` (küçük), `gte` (büyük veya eşit), `lte` (küçük veya eşit), `bitZero` (bit sıfır mı), `bitOne` (bit bir mi). |
| `text`            | string          | Koşul sağlandığında gösterilecek metin. |
| `valueColor`      | string          | Koşul sağlandığında metin (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `valueFontSize`   | string          | Koşul sağlandığında metin boyutu. |
| `backgroundColor` | string          | Koşul sağlandığında arka plan (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `isBlinking`      | boolean         | Koşul sağlandığında metin yanıp sönüyor mu? |
| `andConditions`   | array[object]   | Ek koşullar (ve mantığı ile). |

---

### 🔁 `andConditions` (Ek Koşullar)

Her bir `condition` içinde isteğe bağlı olarak `andConditions` tanımlanabilir.

| Alan Adı             | Tür      | Açıklama |
|----------------------|----------|----------|
| `conditionParamId`   | number   | Ek koşulun parametre ID'si. |
| `compareParamId`     | number   | Karşılaştırma yapılacak parametre ID'si (öncelik compareParamId karşılaştırmasıdır. compareParamId yok ise compareValue sabiti ile karşılaştırma yapar). |
| `compareValue`       | string   | Karşılaştırma değeri. |
| `operator`           | string   | Karşılaştırma operatörü. Desteklenen operatörler: `eq` (eşit), `neq` (eşit değil), `gt` (büyük), `lt` (küçük), `gte` (büyük veya eşit), `lte` (küçük veya eşit), `bitZero` (bit sıfır mı), `bitOne` (bit bir mi). |

---

## 🧪 Örnek `text` Nesnesi

```json
{
  "object": "text",
  "page": 1,
  "row": 1,
  "side": "center",
  "width": "100px",
  "height": "100px",
  "name": "Başlık",
  "nameFontSize": "34px",
  "nameIsBold": true,
  "nameIsItalic": true,
  "nameColor": "yellow",
  "text": "Koşul-1",
  "valueColor": "red",
  "valueFontSize": "34px",
  "valueIsBold": true,
  "backgroundColor": "green",
  "valueIsItalic": true,
  "isBlinking": false,
  "conditions": [
    {
      "conditionParamId": 95,
      "compareValue": "58",
      "operator": "eq",
      "text": "Koşul-2",
      "valueColor": "yellow",
      "valueFontSize": "12px",
      "backgroundColor": "yellow",
      "isBlinking": true,
      "andConditions": [
        {
          "conditionParamId": 29,
          "compareValue": "3.133",
          "operator": "eq"
        },
        {
          "conditionParamId": 43,
          "compareValue": "1",
          "operator": "gte"
        }
      ]
    }
  ]
}
```


# `image` Nesnesi

Bu nesne, sayfada görsel (resim) göstermek için kullanılır. Koşullara bağlı olarak farklı resimler ve efektler uygulanabilir.  
Gösterilecek resimler, programın bulunduğu dizindeki `image` klasöründe yer almalıdır.

---

## 🔧 Özellikler

| Alan Adı           | Tür             | Açıklama |
|--------------------|-----------------|----------|
| `object`           | string          | Nesne tipi, `"image"` olmalıdır. |
| `page`             | number          | Gösterileceği sayfa numarası. |
| `row`              | number          | Satır numarası. |
| `side`             | string          | Ekranın hangi tarafında gösterileceği (`"left"`, `"right"`, `"center"`). |
| `width`            | string          | Resim alanının genişliği (örn: `"100px"`). |
| `height`           | string          | Resim alanının yüksekliği (örn: `"100px"`). |
| `name`             | string          | Görselin başlığı veya adı. |
| `nameFontSize`     | string          | Başlık yazı boyutu. |
| `nameIsBold`       | boolean         | Başlık kalın mı? |
| `nameIsItalic`     | boolean         | Başlık italik mi? |
| `nameColor`        | string          | Başlık (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `imageHeight`      | string          | Gösterilecek resmin yüksekliği. |
| `imageWidth`       | string          | Gösterilecek resmin genişliği. |
| `image`            | string          | Varsayılan gösterilecek resim dosyası adı(image klasöründe olmalı). |
| `conditions`       | array[object]   | Koşullara bağlı resim ve efekt tanımları. |

### `conditions` içindeki her koşul için özellikler:

| Alan Adı           | Tür             | Açıklama |
|--------------------|-----------------|----------|
| `conditionParamId` | number          | Koşulun bağlı olduğu parametre ID'si. |
| `compareParamId`   | number          | Karşılaştırma yapılacak parametre ID'si (öncelik compareParamId karşılaştırmasıdır. compareParamId yok ise compareValue sabiti ile karşılaştırma yapar). |
| `compareValue`     | string/number   | Karşılaştırılacak değer. |
| `operator`         | string          | Karşılaştırma operatörü. Desteklenen operatörler: `eq` (eşit), `neq` (eşit değil), `gt` (büyük), `lt` (küçük), `gte` (büyük veya eşit), `lte` (küçük veya eşit), `bitZero` (bit sıfır mı), `bitOne` (bit bir mi). |
| `image`            | string          | Koşul sağlandığında gösterilecek resim dosyası(image klasöründe olmalı). |
| `effect`           | string          | Uygulanacak efekt türü. Desteklenen efektler: `rotate`, `fade`, `zoom`, `colorChange`, `blur`, `slide`, `pulse`, `flip`. |
| `effectDuration`   | string          | Efekt süresi. (örn: `"0.5s"`, `"1000ms"`). |

---

### 🔁 `andConditions` (Ek Koşullar)

Her bir `condition` içinde isteğe bağlı olarak `andConditions` tanımlanabilir.

| Alan Adı             | Tür      | Açıklama |
|----------------------|----------|----------|
| `conditionParamId`   | number   | Ek koşulun parametre ID'si. |
| `compareParamId`     | number   | Karşılaştırma yapılacak parametre ID'si (öncelik compareParamId karşılaştırmasıdır. compareParamId yok ise compareValue sabiti ile karşılaştırma yapar). |
| `compareValue`       | string   | Karşılaştırma değeri. |
| `operator`           | string   | Karşılaştırma operatörü. Desteklenen operatörler: `eq` (eşit), `neq` (eşit değil), `gt` (büyük), `lt` (küçük), `gte` (büyük veya eşit), `lte` (küçük veya eşit), `bitZero` (bit sıfır mı), `bitOne` (bit bir mi). |

---

## 🧪 Örnek `image` Nesnesi

```json
{
  "object": "image",
  "page": 1,
  "row": 1,
  "side": "center",
  "width": "350px",
  "height": "350px",
  "name": "Başlık",
  "nameFontSize": "34px",
  "nameIsBold": true,
  "nameIsItalic": true,
  "nameColor": "yellow",
  "imageHeight": "120px",
  "imageWidth": "100px",
  "image": "gsmCommunicationGreen.png",
  "conditions": [
    {
      "conditionParamId": 95,
      "compareValue": "58",
      "operator": "eq",
      "image": "gsmCommunicationGreen.png",
      "andConditions": [
        {
          "conditionParamId": 29,
          "compareValue": "3.133",
          "operator": "eq"
        },
        {
          "conditionParamId": 43,
          "compareValue": "1",
          "operator": "gte"
        }
      ]
    },
    {
      "conditionParamId": 95,
      "compareValue": "588",
      "operator": "eq",
      "image": "gsmCommunicationGreen.png"
    },
    {
      "conditionParamId": 43,
      "compareParamId": 44,
      "operator": "neq",
      "image": "gsmCommunicationGreen.png"
    },
    {
      "conditionParamId": 43,
      "compareValue": "1",
      "operator": "bitZero",
      "image": "gsmCommunicationRed.png",
      "effect": "rotate",
      "effectDuration": "0.5s"
    }
  ]
}
```




# `table` Nesnesi

Bu nesne, birden fazla parametreyi tablo formatında listelemek ve gruplamak için kullanılır. Kullanıcıya okunabilir, filtrelenebilir ve gruplanabilir şekilde veri sunmak amacıyla tercih edilir.

---

## 🔧 Özellikler

| Alan Adı        | Tür           | Açıklama                             |
|-----------------|---------------|--------------------------------------|
| `object`        | string        | Nesne tipi, "table" olmalıdır.       |
| `page`          | number        | Gösterileceği sayfa numarası.        |
| `row`           | number        | Satır numarası.                      |
| `side`          | string        | Ekranın hangi tarafında gösterileceği (`"left"`, `"right"`, `"center"`). |
| `width`         | string        | Table alanının genişliği (örn: `"100px"`). |
| `height`        | string        | Table alanının yüksekliği (örn: `"100px"`). |
| `itemFontSize`  | string        | Tablonun öğelerinin yazı boyutu. |
| `filter`        | boolean       | Kullanıcının tabloda filtreleme yapıp yapamayacağı. |
| `order`         | string        | Tablonun sıralama kriterini belirler. "name", "id" veya "group" değerleri alabilir. "group" seçimi durumunda ikinci öncelik "id" kabu edilir.  |
| `showBorder`    | boolean       | Tablonun border çizgisinin gösterilip gösterilmeyeceği. |
| `paramId`       | array[number] | Tablo içinde gösterilecek parametre ID’lerinin listesi. |
| `paramGroups`   | array[string] | Tablo içinde gösterilecek parametre grupları. |
| `conditions`    | array[object] | Koşullara bağlı table gösterimi tanımları. |

### `conditions` içindeki her koşul için özellikler:

| Alan Adı             | Tür      | Açıklama |
|----------------------|----------|----------|
| `conditionParamId`   | number   | Koşulun uygulanacağı parametre ID'si. |
| `compareParamId`     | number   | Karşılaştırma yapılacak parametre ID'si (öncelik compareParamId karşılaştırmasıdır. compareParamId yok ise compareValue sabiti ile karşılaştırma yapar). |
| `compareValue`       | string   | Karşılaştırma yapılacak değer. |
| `operator`           | string   | Karşılaştırma operatörü. Desteklenen operatörler: `eq` (eşit), `neq` (eşit değil), `gt` (büyük), `lt` (küçük), `gte` (büyük veya eşit), `lte` (küçük veya eşit), `bitZero` (bit sıfır mı), `bitOne` (bit bir mi). |
| `isHidden`           | boolean  | Koşul sağlandığında kart gizlensin mi? |
| `isDisabled`         | boolean  | Koşul sağlandığında kart pasif olsun mu? |
| `backgroundColor`    | string   | Koşul sağlanırsa arka plan rengi ne olsun (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |

### 🔁 `andConditions` (Ek Koşullar)

Her bir `condition` içinde isteğe bağlı olarak `andConditions` tanımlanabilir.

| Alan Adı             | Tür      | Açıklama |
|----------------------|----------|----------|
| `conditionParamId`   | number   | Ek koşulun parametre ID'si. |
| `compareParamId`     | number   | Karşılaştırma yapılacak parametre ID'si (öncelik compareParamId karşılaştırmasıdır. compareParamId yok ise compareValue sabiti ile karşılaştırma yapar). |
| `compareValue`       | string   | Karşılaştırma değeri. |
| `operator`           | string   | Karşılaştırma operatörü. Desteklenen operatörler: `eq` (eşit), `neq` (eşit değil), `gt` (büyük), `lt` (küçük), `gte` (büyük veya eşit), `lte` (küçük veya eşit), `bitZero` (bit sıfır mı), `bitOne` (bit bir mi). |

---

## 🧪 Örnek `table` Nesnesi

```json
{
  "object": "table",
  "page": 1,
  "row": 1,
  "side": "center",
  "filter": true,
  "order": "group",
  "conditions": [
      {
        "conditionParamId": 9942,
        "compareValue": "2",
        "operator": "neq",
        "isHidden": true
      }
    ],
  "paramId": [      
    101, 102, 103, 135, 139, 140, 141, 142,
    123, 124, 137, 138, 270, 271, 277, 278
  ],
  "paramGroups": ["Grup1", "Grup2"]
}
```

# `dataTable` Nesnesi

Bu nesne, özelleştirilebilir sütun ve satır yapısıyla veri göstermek için kullanılır. Hem statik metin hem de dinamik parametre değerleri içerebilir. Satırlara koşullu renklendirme uygulanabilir.

---

## 🔧 Özellikler

| Alan Adı        | Tür           | Açıklama                             |
|-----------------|---------------|--------------------------------------|
| `object`        | string        | Nesne tipi, `"dataTable"` olmalıdır. |
| `page`          | number        | Gösterileceği sayfa numarası.        |
| `row`           | number        | Satır numarası.                      |
| `side`          | string        | Ekranın hangi tarafında gösterileceği (`"left"`, `"right"`, `"center"`). |
| `width`         | string        | Tablo alanının genişliği (örn: `"800px"`). |
| `height`        | string        | Tablo alanının yüksekliği (örn: `"400px"`). |
| `itemFontSize`  | string        | Tablonun öğelerinin yazı boyutu (örn: `"14px"`). |
| `filter`        | boolean       | Kullanıcının tabloda arama yapıp yapamayacağı. |
| `showBorder`    | boolean       | Tablo satırlarının alt çizgisinin gösterilip gösterilmeyeceği. |
| `columns`       | array[object] | Tablo sütunlarının tanımları. |
| `rows`          | array[object] | Tablo satırlarının tanımları. |
| `conditions`    | array[object] | Koşullara bağlı tablo gösterimi tanımları. |

---

## 📋 `columns` Dizisi

Her sütun için görünüm ve hizalama ayarları tanımlanır.

| Alan Adı  | Tür    | Açıklama |
|-----------|--------|----------|
| `title`   | string | Sütun başlığı. |
| `width`   | string | Sütun genişliği (örn: `"40%"`, `"200px"`). |
| `align`   | string | Hizalama: `"left"`, `"center"` veya `"right"`. |

---

## 📋 `rows` Dizisi

Her satır, hücre listesi ve isteğe bağlı satır koşulları içerir.

| Alan Adı        | Tür           | Açıklama |
|-----------------|---------------|----------|
| `cells`         | array[object] | Satırdaki hücrelerin listesi. |
| `rowConditions` | array[object] | Satıra uygulanacak koşullu renklendirme tanımları (opsiyonel). |

### `cells` içindeki her hücre için özellikler:

| Alan Adı  | Tür    | Açıklama |
|-----------|--------|----------|
| `type`    | string | Hücre tipi: `"static"` (sabit metin) veya `"param"` (parametre değeri). |
| `value`   | string | `type` `"static"` ise gösterilecek sabit metin. |
| `paramId` | number | `type` `"param"` ise gösterilecek parametre ID'si. |

### `rowConditions` içindeki her koşul için özellikler:

| Alan Adı             | Tür    | Açıklama |
|----------------------|--------|----------|
| `conditionParamId`   | number | Koşulun bağlı olduğu parametre ID'si. |
| `compareValue`       | string | Karşılaştırılacak değer. |
| `operator`           | string | Karşılaştırma operatörü. Desteklenen operatörler: `eq` (eşit), `neq` (eşit değil), `gt` (büyük), `lt` (küçük), `gte` (büyük veya eşit), `lte` (küçük veya eşit), `bitZero` (bit sıfır mı), `bitOne` (bit bir mi). |
| `backgroundColor`    | string | Koşul sağlanırsa satır arka plan rengi (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff4444`, `var(--textPrimary)`). |

---

## 🧠 `conditions` Dizisi

Koşullar, tablonun görünümünü veya davranışını dinamik olarak değiştirmek için kullanılır.

| Alan Adı             | Tür      | Açıklama |
|----------------------|----------|----------|
| `conditionParamId`   | number   | Koşulun uygulanacağı parametre ID'si. |
| `compareParamId`     | number   | Karşılaştırma yapılacak parametre ID'si (öncelik compareParamId karşılaştırmasıdır. compareParamId yok ise compareValue sabiti ile karşılaştırma yapar). |
| `compareValue`       | string   | Karşılaştırma yapılacak değer. |
| `operator`           | string   | Karşılaştırma operatörü. Desteklenen operatörler: `eq` (eşit), `neq` (eşit değil), `gt` (büyük), `lt` (küçük), `gte` (büyük veya eşit), `lte` (küçük veya eşit), `bitZero` (bit sıfır mı), `bitOne` (bit bir mi). |
| `isHidden`           | boolean  | Koşul sağlandığında tablo gizlensin mi? |
| `isDisabled`         | boolean  | Koşul sağlandığında tablo pasif olsun mu? |
| `backgroundColor`    | string   | Koşul sağlanırsa arka plan rengi (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |

### 🔁 `andConditions` (Ek Koşullar)

Her bir `condition` içinde isteğe bağlı olarak `andConditions` tanımlanabilir.

| Alan Adı             | Tür      | Açıklama |
|----------------------|----------|----------|
| `conditionParamId`   | number   | Ek koşulun parametre ID'si. |
| `compareParamId`     | number   | Karşılaştırma yapılacak parametre ID'si (öncelik compareParamId karşılaştırmasıdır. compareParamId yok ise compareValue sabiti ile karşılaştırma yapar). |
| `compareValue`       | string   | Karşılaştırma değeri. |
| `operator`           | string   | Karşılaştırma operatörü. Desteklenen operatörler: `eq` (eşit), `neq` (eşit değil), `gt` (büyük), `lt` (küçük), `gte` (büyük veya eşit), `lte` (küçük veya eşit), `bitZero` (bit sıfır mı), `bitOne` (bit bir mi). |

---

## 🧪 Örnek `dataTable` Nesnesi

```json
{
  "object": "dataTable",
  "page": 5,
  "row": 1,
  "side": "center",
  "filter": true,
  "width": "800px",
  "height": "400px",
  "itemFontSize": "14px",
  "showBorder": true,
  "columns": [
    { "title": "Parameter", "width": "40%", "align": "left" },
    { "title": "Value 1",   "width": "30%", "align": "center" },
    { "title": "Value 2",   "width": "30%", "align": "center" }
  ],
  "rows": [
    {
      "cells": [
        { "type": "static", "value": "Voltage" },
        { "type": "param",  "paramId": 100 },
        { "type": "param",  "paramId": 101 }
      ]
    },
    {
      "rowConditions": [
        {
          "conditionParamId": 102,
          "compareValue": "Enabled",
          "operator": "eq",
          "backgroundColor": "#ff4444"
        }
      ],
      "cells": [
        { "type": "static", "value": "Current" },
        { "type": "param",  "paramId": 102 },
        { "type": "param",  "paramId": 103 }
      ]
    }
  ],
  "conditions": [
    {
      "conditionParamId": 104,
      "compareValue": "8",
      "operator": "eq",
      "isDisabled": true
    }
  ]
}
```

# `chart` Nesnesi

Bu nesne, parametre değerlerini zaman bazlı veya kategorik olarak grafik formatında göstermek için kullanılır. Birden fazla seri destekler ve line, bar veya scatter grafik tiplerinde çalışır.

---

## 🔧 Özellikler

| Alan Adı       | Tür           | Açıklama                             |
|----------------|---------------|--------------------------------------|
| `object`       | string        | Nesne tipi, `"chart"` olmalıdır.     |
| `page`         | number        | Gösterileceği sayfa numarası.        |
| `row`          | number        | Satır numarası.                      |
| `side`         | string        | Ekranın hangi tarafında gösterileceği (`"left"`, `"right"`, `"center"`). |
| `width`        | string        | Grafik alanının genişliği (örn: `"500px"`). |
| `height`       | string        | Grafik alanının yüksekliği (örn: `"300px"`). |
| `title`        | string        | Grafiğin başlığı (opsiyonel). |
| `chartType`    | string        | Grafik tipi: `"line"`, `"bar"` veya `"scatter"`. |
| `timeWindow`   | number        | Grafik zaman penceresi saniye cinsinden (örn: `60`). Sadece `line` tipi için geçerlidir. |
| `showTooltip`  | boolean       | Fare üzerine gelindiğinde değer gösterilsin mi? |
| `series`       | array[object] | Grafikte gösterilecek seri tanımları. |

---

## 📊 `series` Dizisi

Her seri bir parametreye bağlıdır ve görünüm özellikleri ayrı ayrı tanımlanabilir.

| Alan Adı    | Tür    | Açıklama |
|-------------|--------|----------|
| `paramId`   | number | Serinin bağlı olduğu parametre ID'si. |
| `name`      | string | Seri adı (tooltip ve legend'da gösterilir). |
| `lineColor` | string | Seri rengi (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#2196F3`, `var(--textPrimary)`). |
| `lineWidth` | number | Çizgi kalınlığı (örn: `1`, `2`). Sadece `line` tipi için geçerlidir. |
| `min`       | number | Y ekseni minimum değeri (opsiyonel). |
| `max`       | number | Y ekseni maksimum değeri (opsiyonel). |

---

## 🧪 Örnek `chart` Nesnesi

```json
{
  "object": "chart",
  "page": 3,
  "row": 1,
  "side": "center",
  "width": "500px",
  "height": "300px",
  "title": "Voltage & Current",
  "chartType": "line",
  "timeWindow": 60,
  "showTooltip": true,
  "series": [
    {
      "paramId": 100,
      "name": "Voltage",
      "lineColor": "#2196F3",
      "lineWidth": 2,
      "min": 0,
      "max": 500
    },
    {
      "paramId": 101,
      "name": "Current",
      "lineColor": "#FF5722",
      "lineWidth": 1
    }
  ]
}
```

# `button` Nesnesi
Bu nesne, ekranda bir buton göstermek ve kullanıcı etkileşimiyle belirli bir eylemi (örneğin bir parametreye değer atamak) tetiklemek için kullanılır.

---

## 🔧 Özellikler

| Alan Adı            | Tür           | Açıklama                             |
|---------------------|---------------|--------------------------------------|
| `object`            | string        | Nesne tipi, "button" olmalıdır.      |
| `page`              | number        | Gösterileceği sayfa numarası.        |
| `row`               | number        | Satır numarası.                      |
| `side`              | string        | Ekranın hangi tarafında gösterileceği (`"left"`, `"right"`, `"center"`). |
| `width`             | string        | Buton alanının genişliği (örn: `"100px"`). |
| `height`            | string        | Buton alanının yüksekliği (örn: `"100px"`). |
| `name`              | string        | Buton ismi. |
| `nameFontSize`      | string        | Buton ismi font boyutu (örn: `"18px"`). |
| `nameIsBold`        | boolean       | Buton ismi kalın mı? (`true` veya `false`). |
| `nameIsItalic`      | boolean       | Buton ismi italik mi? |
| `nameColor`         | string        | Buton ismi rengi (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `backgroundColor`   | string        | Buton zemin rengi (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |
| `borderRadius`      | string        | Buton radius değeri (örn: `"18px"`). |
| `title`             | string        | Mouse ile buton üzerine gelindiğinde yazacak mesaj. |
| `image`             | string        | Buton üzerinde gösterilecek görselin dosya adı (image klasöründe olmalı). |
| `imageHeight`       | string        | Buton üzerinde gösterilecek resmin yüksekliği (örn: `"100px"`). |
| `imageWidth`        | string        | Buton üzerinde gösterilecek resmin genişliği (örn: `"100px"`). |
| `actionType`        | string        | Butona tıklanınca yapılacak işlem türü. `"setValue"`, `"setBit"` veya `"switchGroup"` değerini alabilir. `switchGroup` değeri `actionGroup` olarak tanımlı sayfayı açar. |
| `actionParamId`     | number        | İşlem yapılacak parametre ID'si. |
| `actionValue`       | number        | Parametreye atanacak değer. (`setBit` kullanıldığında bu parametre `0` ise ilgili biti `0`, `1` ise `1` yapar.) |
| `actionGroup`       | string        | `actionType` parametresi `switchGroup` olarak seçili ise bu parametrede yazan sayfayı açar. Sayfa bilgileri `config` nesnesinin `pageGroups` özelliğinde tanımlıdır. |
| `bitPosition`       | number        | İşlem yapılacak bit numarası. |
| `conditions`        | array[object] | Koşullara bağlı buton gösterimi tanımları. |

---

## 🧠 `conditions` Dizisi

Koşullar, butonun görünümünü veya davranışını dinamik olarak değiştirmek için kullanılır.

| Alan Adı             | Tür      | Açıklama |
|----------------------|----------|----------|
| `conditionParamId`   | number   | Koşulun uygulanacağı parametre ID'si. |
| `compareParamId`     | number   | Karşılaştırma yapılacak parametre ID'si (öncelik `compareParamId` karşılaştırmasıdır. `compareParamId` yok ise `compareValue` sabiti ile karşılaştırma yapar). |
| `compareValue`       | string   | Karşılaştırma yapılacak değer. |
| `operator`           | string   | Karşılaştırma operatörü. Desteklenen operatörler: `eq` (eşit), `neq` (eşit değil), `gt` (büyük), `lt` (küçük), `gte` (büyük veya eşit), `lte` (küçük veya eşit), `bitZero` (bit sıfır mı), `bitOne` (bit bir mi). |
| `isHidden`           | boolean  | Koşul sağlandığında buton gizlensin mi? |
| `isDisabled`         | boolean  | Koşul sağlandığında buton pasif olsun mu? |
| `backgroundColor`    | string   | Koşul sağlanırsa arka plan rengi (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). |

### 🔁 `andConditions` (Ek Koşullar)

Her bir `condition` içinde isteğe bağlı olarak `andConditions` tanımlanabilir.

| Alan Adı             | Tür      | Açıklama |
|----------------------|----------|----------|
| `conditionParamId`   | number   | Ek koşulun parametre ID'si. |
| `compareParamId`     | number   | Karşılaştırma yapılacak parametre ID'si (öncelik `compareParamId` karşılaştırmasıdır. `compareParamId` yok ise `compareValue` sabiti ile karşılaştırma yapar). |
| `compareValue`       | string   | Karşılaştırma değeri. |
| `operator`           | string   | Karşılaştırma operatörü. Desteklenen operatörler: `eq` (eşit), `neq` (eşit değil), `gt` (büyük), `lt` (küçük), `gte` (büyük veya eşit), `lte` (küçük veya eşit), `bitZero` (bit sıfır mı), `bitOne` (bit bir mi). |

---

## 🧪 Örnek `button` Nesnesi

```json
{
  "object": "button",
  "page": 1,
  "row": 10,
  "side": "center",
  "name": "Start",
  "nameFontSize": "16px",
  "nameIsBold": true,
  "nameIsItalic": false,
  "nameColor": "white",
  "backgroundColor": "#FFFFFF",
  "borderRadius": "10px",
  "title": "Start",
  "image": "start.png",
  "imageHeight": "80px",
  "imageWidth": "80px",
  "height": "100px",
  "width": "100px",
  "actionType": "setValue",
  "actionParamId": 201,
  "actionValue": 1, 
  "bitPosition": 3,
  "actionGroup": "detaylar",
  "conditions": [
    {
      "conditionParamId": 100,
      "compareValue": "1",
      "operator": "eq",
      "isDisabled": true,
      "backgroundColor": "red"
    }
  ]
}
```

---

## ⚙️ Örnek `config` Nesnesi

Her tasarım dosyasının başında bulunan `config` nesnesi, buton objesi için `switchGroup` seçilmesi durumunda aşağıdaki gibi tanımlanabilir.

| Alan Adı     | Tür           | Açıklama |
|--------------|---------------|----------|
| `object`     | string        | Nesne tipi, `"config"` olmalıdır. |
| `pageCount`  | number        | Toplam sayfa sayısı. |
| `pageTitle`  | array[string] | Her sayfanın başlığı. |
| `pageGroups` | object        | Sayfa grupları. Her grup, o grupta görünecek sayfa numaralarının listesini içerir. `switchGroup` butonu bu gruplar arasında geçiş yapar. |

```json
{
  "object": "config",
  "pageCount": 4,
  "pageTitle": [
    "Monitoring",
    "Set Point",
    "Configuration",
    "Protections"
  ],
  "pageGroups": {
    "default": [1, 2],
    "detaylar": [3, 4]
  }
}
```

# `space` Nesnesi

Bu nesne, sayfa düzeninde boşluk oluşturmak için kullanılır. Genellikle diğer bileşenler arasında görsel ayrım sağlar.

---

## 🔧 Özellikler

| Alan Adı           | Tür     | Açıklama                                    |
|--------------------|---------|---------------------------------------------|
| `object`           | string  | Nesne tipi, `"space"` olmalıdır.            |
| `page`             | number  | Gösterileceği sayfa numarası.               |
| `row`              | number  | Satır numarası.                             |
| `side`             | string  | Ekranın hangi tarafında gösterileceği (`"left"`, `"right"`, `"center"`). |
| `width`            | string  | Boşluk alanının genişliği (örn: `"100px"`).  |
| `height`           | string  | Boşluk alanının yüksekliği (örn: `"100px"`). |
| `backgroundColor`  | string  | Arka plan rengi ne olsun (renk ismi, hex kodu veya CSS değişkeni, örn: `red`, `#ff0000`, `var(--textPrimary)`). Tanımlanmaz ise zemin rengi olur |
| `showShadow`       | boolean | Gölge olsun mu? (`true` veya `false`). |

---

## 🧪 Örnek `space` Nesnesi

```json
{
  "object": "space",
  "page": 1,
  "row": 1,
  "side": "center",
  "width": "100px",
  "height": "180px",
  "backgroundColor" : "red",
  "showShadow" : true
}
```


# `dataoperation` Nesnesi

`dataoperation` nesnesi, bir veya daha fazla adımda matematiksel işlemler uygulayarak, hedef bir parametre (`targetParamId`) için hesaplama yapmanızı sağlar. İşlem adımları sırayla uygulanır ve çıkan sonuç, belirtilen hedef parametreye atanır.

---

## 🔧 Özellikler

| Alan Adı        | Tür       | Açıklama                                                               |
|------------------|-----------|-----------------------------------------------------------------------|
| object           | string    | Nesne tipi, `"dataoperation"` olmalıdır.                              |
| targetParamId    | number    | Hesaplama sonucunun atanacağı hedef parametrenin ID'si.               |
| decimalPlaces    | number    | Sonucun virgülden sonra kaç basamakla gösterileceği. Varsayılan: `0`. |
| operation        | object    | Hesaplama adımlarını içeren `steps` dizisini barındırır.              |

---

### 🧮 operation.steps Özellikleri

`steps` dizisi, sırasıyla uygulanacak işlemleri tanımlar.

| Alan Adı    | Tür       | Açıklama                                                                               |
|-------------|-----------|----------------------------------------------------------------------------------------|
| type        | string    | `"param"` (başka bir parametreden veri alır) veya `"constant"` (sabit değer kullanır). |
| id          | number    | `type` değeri `"param"` ise, kullanılan parametrenin ID'si.                            |
| value       | number    | `type` değeri `"constant"` ise, kullanılacak sabit sayı değeri.                        |
| operator    | string    | Uygulanacak matematiksel işlem. Desteklenen operatörler: `+`, `-`, `*`, `/`, `>>`, `<<`|

> 🔁 İşlemler sırayla uygulanır. İlk değer, `targetParamId` ile belirtilen parametrenin mevcut değeri olarak alınır.

---

## 💡 Operatör Açıklamaları

| Operatör | Anlamı                |
|----------|-----------------------|
| `+`      | Toplama               |
| `-`      | Çıkarma               |
| `*`      | Çarpma                |
| `/`      | Bölme                 |
| `>>`     | Bit kaydırma sağa     |
| `<<`     | Bit kaydırma sola     |

---

## 🧪 Örnek `dataoperation` Nesnesi

```json
{
  "object": "dataoperation",
  "targetParamId": 10,
  "decimalPlaces": 0,
  "operation": {
    "steps": [
      {
        "type": "param",
        "id": 15,
        "operator": "+"
      },
      {
        "type": "constant",
        "value": 100,
        "operator": "-"
      },
      {
        "type": "param",
        "id": 20,
        "operator": "*"
      },
      {
        "type": "constant",
        "value": 2,
        "operator": ">>"
      }
    ]
  }
}
```

Bu örnekte, `paramId: 10` olan hedef parametrenin başlangıç değeri alınır. Ardından şu işlemler sırasıyla uygulanır:

1. `paramId: 15` ile **toplanır**.
2. `100` sabiti ile **çıkarılır**.
3. `paramId: 20` ile **çarpılır**.
4. `2` bit kaydırılarak **sağa alınır**.

Sonuç, `decimalPlaces: 0` olduğu için **virgülden sonra basamak olmadan** formatlanır.
