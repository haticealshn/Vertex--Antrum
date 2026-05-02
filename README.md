# 🚀 ANTRUM: Zero-Carbon Cave Storage & Exchange OS

*Kapadokya Hackathon 2026 | "Cave2Cloud - Kapadokya'dan Global Pazara" Teması* *Takım: **Vertex***

---

## 📌 Proje Bağlantıları
* 🎥 **Demo Videosu (Loom/YouTube):** [Video Linki Buraya] *(Max 3 dk)*
* 🌐 **Canlı Demo (Vercel/Render):** [Canlı Yayın Linki Buraya]
* 📂 **GitHub Repo:** [Repo Linki]

---

## 💡 1. Projenin Özü: "Rakiplerin Hiç Düşünmediği Modül"
Kapadokya'daki doğal mağaralar (tüf kayalar), yapay soğuk hava depolarının yaptığı iklimlendirme işini **%0 enerji** harcayarak yapar. ANTRUM, bu devasa enerji tasarrufunu (kWh/m³) ölçer, ISO 14064 standartlarına göre belgelendirir, karbon kredisine dönüştürür ve küresel şirketlere satar. Bu sistemde mağara sahibi, alanının doğal soğutma kapasitesini kiralayarak 3 eksenli (Kira + Lojistik + Karbon Kredisi) bir gelir modeli elde eder.

## 🛠️ 2. Sistem Yetenekleri (MVP Durumu)
Uygulamamız tam fonksiyonel bir **Single Page Application (SPA)** olarak kurgulanmıştır:
* **Tam Reaktif CRUD İşlemleri:** Sisteme yeni mağara eklenebilir, mevcut mağaralar düzenlenebilir veya silinebilir. Yapılan her değişiklik Dashboard KPI'larını (Toplam Hacim, Portföy Değeri, Toplam Karbon) anında günceller.
* **İnteraktif Veri Görselleştirme:** Karbon hesaplayıcıdaki slider'lar (hacim ve sıcaklık) kullanıcı etkileşimine göre dinamik olarak renk ve boyut değiştirir.
* **Glassmorphism UI:** Sürdürülebilirlik vizyonunu yansıtmak amacıyla "Aydınlık Doğa (Light Nature)" teması kullanılmıştır.

## ⚙️ 3. Hackathon Zorunlu Kurallarının (Bonus) Entegrasyonu
Hackathon komitesi tarafından belirlenen 3 teknik zorunlu kural, birbiriyle konuşan tek bir hesap zincirinde **"Bonus Puan"** kurgusuyla birleştirilmiştir:

1. **Kural 3 (Coğrafi Veri & Dinamik Rota):** Lojistik ve Dashboard sekmelerinde sabit veri kullanılmamıştır. Kullanıcı bir çıkış şehri ve sistemdeki aktif mağaralardan birini hedef olarak seçtiğinde, mesafe **Leaflet.js** ve **OSRM (OpenRouteService)** ile dinamik hesaplanır. Haritada tıklanan konumların adresleri **Nominatim API (Reverse Geocoding)** ile anlık tespit edilir.
2. **Kural 1 (Coğrafi Karbon İzi):** OSRM'den gelen rota mesafesi (km) ve yük tonajı baz alınarak nakliye emisyonu hesaplanır. Bu değer, mağaranın sağladığı brüt karbon tasarrufundan düşülerek **"Net Karbon Kazancı"** elde edilir.
3. **Kural 2 (Canlı Döviz Kuru):** Elde edilen Net Karbon Kredisi, **TCMB XML Servisi** (Fallback: ExchangeRate-API) üzerinden anlık çekilen USD/TRY kuru ile çarpılarak mağara sahibine anlık TL karşılığı olarak sunulur.

## 🧮 4. Bilimsel Altyapı ve Karbon Motoru (ISO 14064)
Karbon motorumuz m² yerine, GCCA/IIR küresel soğuk zincir standartları olan **m³ (hacim)** bazlı çalışır. 
* *Formül:* `[Referans Depo kWh - Mağara Operasyonel Yükü (5 kWh)] × Sıcaklık Katsayısı × Hacim × 0.522 (TEİAŞ Emisyon Faktörü)`
* Şeffaflık ilkesi gereği mağaranın %0 enerji harcadığı iddia edilmez; aydınlatma, fan ve sensörler için **5 kWh/m³** operasyonel yük brüt tasarruftan düşülür.

## 🌐 5. API Ekosistemi ve Veri Akışı
Sistem tamamen canlı verilerle beslenen bir organizmadır:
* **Open-Meteo Live API:** Nevşehir'in anlık dış sıcaklık ve nem verisini çekerek karbon tasarruf simülasyonunu günceller.
* **Open-Meteo Archive API:** Raporlar sekmesinde son 1, 3 veya 6 aylık geçmiş gerçek hava verilerini çekerek geçmiş karbon tasarruf istatistiklerini oluşturur (Chart.js ile çizdirilir) ve CSV olarak dışa aktarır.
* **OSRM & Nominatim:** Dinamik rota çizimi, mesafe hesaplama ve harita üstü konum sorgulama.
* **TCMB / ExchangeRate-API:** Canlı kur çevirileri.

## 🏗️ 6. Sistem Mimarisi (Architectural Diagram)

```mermaid
graph TD
    A[Meteoroloji / Open-Meteo API] -->|Anlık / Geçmiş İklim| B(ISO 14064 Karbon Motoru)
    C[Lojistik Mesafe / OSRM API] -->|Nakliye Emisyonu| B
    B -->|Net Karbon Kredisi| D[Verra / Gold Standard]
    D --> E(Canlı Döviz API)
    E -->|Fiyatlandırma| F[Glassmorphism Dashboard]
    F -->|In-Memory CRUD State| G[Mağara Ağları Veritabanı]
