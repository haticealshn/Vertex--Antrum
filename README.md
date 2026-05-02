# 🚀 ANTRUM: Zero-Carbon Cave Storage & Exchange Ecosystem

*Kapadokya Hackathon 2026 | "Cave2Cloud - Kapadokya'dan Global Pazara" Teması* *Takım: **Vertex***

---

## 📌 Proje Bağlantıları
* 🎥 **Demo Videosu (Loom):** [Video Linki Buraya] *(Max 3 dk)*
* 🌐 **Canlı Demo (Vercel):** [Canlı Yayın Linki Buraya]
* 📂 **GitHub Repo:** [Repo Linki] *(Not: Pazar sabahı 09:00 öncesi Public yapılacaktır)*

---

## 💡 1. Projenin Özü: Rakiplerin Hiç Düşünmediği Modül
Kapadokya'daki doğal mağaralar, yapay soğuk hava depolarının yaptığı işi **%0 enerji** harcayarak yapar. ANTRUM, bu devasa enerji tasarrufunu ölçer, ISO 14064 standartlarına göre belgelendirir, karbon kredisine dönüştürür ve küresel şirketlere satar. Bu sistemde mağara sahibi hiçbir şey üretmeden, sadece alanının doğal soğutma kapasitesini kiralayarak 3 eksenli (Kira + Lojistik + Karbon Kredisi) bir gelir elde eder.

## 🔬 2. Bilimsel Altyapı ve Karbon Tasarruf Modeli

**Geleneksel Depolar Neden Zararlı?**
Yapay soğuk hava depolarının karbon salınımı iki ana kaynaktan (dolaylı) gerçekleşir:
1. **Elektrik Tüketimi:** Standart bir soğuk depo yılda 200-400 kWh/m² enerji tüketir. Türkiye'nin şebeke yapısında bu ciddi bir karbon ayak izi demektir.
2. **Soğutucu Gaz Kaçakları:** Klimaların içindeki HFC (hidroflorokarbon) gazları kaçtığında, CO₂'den binlerce kat daha zararlıdır. Örneğin; R-410A gazının Küresel Isınma Potansiyeli (GWP) 2.088'dir. (1 kg kaçak = 2.088 kg CO₂ salınımı).

**Doğal Avantaj (Respiration Emission):**
Patates gibi organik ürünler depolanırken oksijen tüketir ve CO₂/nem salar. Yapay depolarda bu CO₂'yi temizlemek için klimalar ekstra enerji harcar. ANTRUM'un kullandığı mağaralarda ise bu emisyon doğal havalanma ve tüf kayanın nefes alan yapısıyla ekstra enerji gerektirmeden dağılır.

## 🧮 3. Hesaplama Metodolojisi (Karma Yapı)
Sistemimiz, problemi çözerken hem **Deterministik** hem de **Stokastik** modelleri birleştirir:

* **Deterministik Kısım (Kesin Formüller):** Enerji tasarrufu ISO 14064 formülleriyle hesaplanır. Türkiye elektrik emisyon faktörü (TEİAŞ 2023) **0.522 kg CO₂/kWh** olarak baz alınır.
  * *Formül:* `Tasarruf (kg CO₂e) = [Referans Depo kWh - Mağara kWh (0)] × 0.522`
  * *Örnek (100 m² alan için):* 300 kWh × 0.522 = 156.6 kg CO₂/m²/yıl. 100 m² bir mağara yılda yaklaşık 15.7 ton CO₂ tasarrufu sağlar.
* **Stokastik Kısım (Makine Öğrenmesi):** Mağaranın nem ve sıcaklık davranışı hava koşullarına göre değişir. Geçmiş sensör ve iklim verilerine dayalı makine öğrenmesi (regresyon) modeliyle `Open-Meteo API` üzerinden tahminleme yapılır. (Simülasyon baz değerleri: 11°C sıcaklık, %70-80 nem).

## 🌍 4. Küresel Pazar ve Sertifikasyon Modeli
Üretilen karbon tasarrufu, küresel havacılık sektörü başta olmak üzere dev şirketlere satılır. Havayolu idaresinin onayına gerek yoktur; ICAO'nun CORSIA programı kapsamında 193 ülkedeki tüm havayolları bu kredileri zorunlu olarak alır.

* **Verra (VCS):** Enerji verimliliğine odaklanır. 1 kredi = 1 ton CO₂e (Güncel: 10$/ton). Başlangıç aşaması hedeftir.
* **Gold Standard:** WWF desteklidir. Çevresel + sosyal fayda arar. Kapadokya yerel halkına katkı sağladığı için ileri aşamada (30$/ton) hedeflenmektedir.

---

## ⚙️ 5. Zorunlu Kuralların (Bonus) Entegrasyonu
Üç zorunlu kural, birbiriyle konuşan tek bir hesap zincirinde birleştirilmiştir:

1. **Kural 3 (Coğrafi Veri):** `Nominatim` ve `OpenRouteService` API'leri ile ürünün çıkış noktasından mağaraya olan lojistik rotası (km) dinamik olarak çizilir.
2. **Kural 1 (Coğrafi Karbon İzi):** Lojistik esnasında oluşan taşıma karbon izi (Mesafe × Yük × 0.100 TIR Faktörü) hesaplanır. Mağaranın sağladığı "Kurtarılan Karbon" (ISO 14064) miktarından, lojistikte harcanan karbon düşülerek NET Karbon Kredisi elde edilir.
3. **Kural 2 (Canlı Döviz):** Elde edilen Net Karbon Kredisi, `TCMB EVDS API` üzerinden anlık çekilen USD/EUR kurları ile TL'ye çevrilir. Fiyatlandırma arayüzde ₺ ve $ olarak gösterilir ve "Kiralama Sözleşmesi" kararını tetikler.

---

## 🏗️ 6. Sistem Mimarisi & Veri Akışı

```mermaid
graph TD
    A[Meteoroloji / Open-Meteo API] -->|Sıcaklık/Nem| B(Stokastik ML Modeli)
    B --> C{ANTRUM Karbon Motoru}
    D[Lojistik Mesafe / OpenRouteService] -->|Ulaşım Emisyonu| C
    E[ISO 14064 & TEİAŞ 0.522 Çarpanı] -->|Depolama Tasarrufu| C
    C -->|Net Karbon Kredisi| F[Verra / Gold Standard API]
    F --> G(TCMB EVDS API - Canlı Kur)
    G -->|Satış Kararı| H[Çift Para Birimli Dashboard]
