# FinAnchor 3.0

## Bankacılıkta Sürdürülebilirlik Erken Uyarı Sistemi

---

## Bankacılıkta Sürdürülebilirlik

Sürdürülebilirlik üç ana bileşenden oluşur:

- Environmental (Çevresel)
- Social (Sosyal)
- Governance (Yönetişim)

Bankacılık sektöründe sürdürülebilirlik çoğu zaman;

- İklim krizi projeleri
- Yeşil enerji yatırımları
- Cinsiyet eşitliği programları
- ESG raporlamaları

gibi unsurlar üzerinden pazarlama diliyle sunulmaktadır.

Ancak bankacılıkta gerçek sürdürülebilirlik, uzun vadede sosyal ve yönetişimsel dayanıklılık ile mümkündür.

### ESG Ağırlıklandırma Gerçeği

S&P ESG ağırlıklandırmasına göre (bankalar ve finansal hizmetler):

- Social & Governance: %84
- Environmental: %16

MSCI ESG ağırlıklandırmasında çevresel faktörlerin payı %10’a kadar düşmektedir.

Bu durum, bankacılıkta sürdürülebilirliğin temel belirleyicisinin sosyal ve yönetişimsel yapı olduğunu göstermektedir.

---

## Projenin Vizyonu

FinAnchor, bankalar için tasarlanmış bir erken uyarı sistemidir.

Temel inancımız:

> Bankacılık sektöründe sürdürülebilirlik, sosyal ve yönetişimsel faktörler öncelenmeden sağlanamaz.

Amacımız çevresel faktörleri dışlamak değildir. Aksine çevresel faktörlerin sosyal yapıyı etkilediğinin farkındayız. Ancak önceliğimiz, yönetişim ve sosyal dayanıklılık üzerinden potansiyel krizleri erken tespit etmektir.

FinAnchor’ın hedefi:

- 2008 Krizi
- DotCom Balonu
- Credit Suisse Vakası

gibi sürdürülebilirlik kaynaklı finansal kırılmaları önceden algılayabilecek bir sistem geliştirmektir.

---

## Veri Toplama ve Metodoloji

Yaklaşık 100 bankadan veri toplanmıştır.

### Veri Kaynakları

- S&P ESG Skorları (Python Selenium ile)
- Yahoo Finance:
  - ROE (%)
  - ROA (%)
  - P/E
  - P/B
  - Toplam Getiri
  - Volatilite
  - Sharpe Ratio
- Fitch Ratings:
  - Long Term Issuer Default Rating
- Ülke bazlı:
  - Enflasyon oranları
  - Kredi derecelendirmeleri
- Sürdürülebilirlik raporlarından çıkartılan birçok veri

Tüm veriler normalize edilmiş ve PostgreSQL veritabanında saklanmıştır.

---

## Integrity Index

FinAnchor’ın temel yeniliği olan metrik:

Integrity Index = 0.4 × ESG Score (Normalize) + 0.3 × Sharpe Ratio (Normalize) +0.3 × Volatility (Ters Normalize)


### Amacı

Bir banka:

- Yüksek ESG skoruna sahip olabilir,
- Ancak yüksek volatiliteye sahip olabilir,
- Sharpe oranı negatif olabilir,
- Piyasa güveni zayıf olabilir.

Bu durumda ESG skoru tek başına sürdürülebilirliği temsil etmez.

Integrity Index:

- Greenwashing riskini
- Finansal kırılganlığı
- Piyasa güveni ile ESG uyumsuzluğunu

tespit etmeyi amaçlar.

---

## Gözlemler

JPMorgan, Goldman Sachs, Morgan Stanley gibi bazı büyük bankaların ESG skorlarının düşük olduğu görülmüştür.

Bunun nedeni:

- Eksik anket bildirimleri
- Public veriye dayalı puanlama
- Eksik veri için “0” atanması

Ancak bu bankalar:

- Yüksek kredi notları
- Büyük piyasa değerleri
- “Too Big To Fail” algısı

sebebiyle yatırımcı güvenini korumaktadır.

Tarih göstermiştir ki büyük ölçekli kurumlar kriz anında en kırılgan yapılar olabilir.

---

## Sistem Mimarisi

### Veritabanı

- PostgreSQL
- Normalize edilmiş finansal ve ESG veriler
- Dinamik veri çekme altyapısı

### Uygulama

- JavaScript ile geliştirilmiştir.
- 2 ana modülden oluşmaktadır.

---

# 1️⃣ Ranking Modülü

- Bankalar Integrity Index’e göre sıralanır.
- Sütun grafiği ile görselleştirilir.
- Karşılaştırmalı sürdürülebilirlik analizi yapılır.

---

# 2️⃣ DNA Analyzer Modülü

Bu modül, belirlenen eşik değerlerine göre otomatik stratejik öneriler üretir.

### Örnek Kurallar

#### Eğer Enflasyon > %25 ise

**ALM & Enflasyon Kalkanı**  
Sabit getirili varlıklar azaltılmalı, TÜFE’ye endeksli tahviller artırılmalıdır.

---

#### Eğer Sustainability Score < 0.65 ise  
(Sustainability Score = (ESG + Integrity Index) / 2)

**Dijital Kaldıraç Stratejisi**  
Operasyonel maliyetleri düşürmek için işlemler %90+ dijital kanallara taşınmalıdır.

---

#### Eğer Sharpe Ratio < 0.35 ise

**Dinamik Ücret Politikası**

---

#### Eğer Integrity Index < 0.55 ise

**Sermaye Koruma (Oto-finansman)**

---

#### Eğer Volatility Security < 0.40 ise

**Döviz / Altın Bazlı Hedging**

---

#### Eğer ROE > %10 ve ESG < 0.40 ise

**Etik Kaldıraç ve Yeşil Tampon**

---

#### Eğer Status = “Sovereign Equal” ve Integrity > 0.7 ise

**Makroekonomik Tavanı Kırma Stratejisi**

---

#### Eğer P/B < 1 ve Integrity düşük ise

**Bilanço Arındırma & Şeffaflık Atılımı**

---

#### Eğer Integrity > 0.7 ve Sharpe > 0.5 ise

**Sürdürülebilir Risk Liderliği**

---

#### Eğer Integrity < 0.5 ve Sharpe < 0.3 ise

**Risk Yönetim Sistemi Revizyonu**

---

## Sosyal Etki Katmanı

8 banka için sürdürülebilirlik raporlarından ek veriler elde edilmiştir.

Segmentasyon:

- Yüksek ESG / Büyük Piyasa Değeri → BBVA
- Yüksek ESG / Küçük Piyasa Değeri → Taishin, Banco do Brasil
- Düşük ESG / Büyük Piyasa Değeri → JPMorgan, Goldman Sachs, Morgan Stanley, Bank of America
- Düşük ESG / Küçük Piyasa Değeri → Intercorp Financial Services

Ek metrikler:

- Green Finance Volume
- Green Progress Ratio
- KOBİ Destek Oranı (sSme)
- Kadın Girişimci Destek Oranı (sWomen)
- Finansal Kapsayıcılık (sInclusion)
- Social Impact Score

### Ek Aksiyon Kuralları

- Green progress > 80 ve ESG < 0.2 → Greenwashing Riski
- sSme < 0.5 → Mikro-KOBİ Finansman Atağı
- sWomen < 0.5 → Kadın Girişimci Kredi Fonu
- sInclusion < 0.5 → Dijital Kapsayıcılık Hamlesi
- social_impact_score < 0.5 → Toplumsal Yatırım Stratejisi

---

## Görsel Bileşenler

- Radar Grafiği (Enflasyona karşı reel erozyon analizi)
- Industrial Audit Note (Genel yorum bölümü)
- Rozetler:
  - Ülke
  - Banka kredi notu
  - Piyasa değeri
  - Ülke ile kredi notu karşılaştırması
  - Çevresel yatırım doğruluk rozeti
  - Sosyal kapsayıcılık rozeti

---

## Problem Tanımı

Bankacılıkta sürdürülebilirlik riski öngörülemezdir.

2008, DotCom ve Credit Suisse örnekleri, finansal sistemdeki yapısal kör noktaları göstermektedir.

---

## Amaç

Sürdürülebilirliği yalnızca anlatı temelli bir kavram olmaktan çıkararak, sosyal ve yönetişimsel öncelikli bir erken uyarı mekanizması geliştirmek.

---

## Çözüm

FinAnchor şu an erken aşama bir prototiptir.

Gelecekte:

- Yapay zeka entegrasyonu
- Anomali tespiti
- Kriz tahminleme modelleri
- Kurumsal API entegrasyonu

ile geliştirilebilir.

Amaç:

Yaklaşan riskleri erken tespit etmek ve ilgili kuruma stratejik aksiyon önerileri sunmak.

---

