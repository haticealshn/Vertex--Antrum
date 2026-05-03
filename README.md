# 🚀 ANTRUM: Zero-Carbon Cave Storage & Exchange OS

*Kapadokya Hackathon 2026 | "Cave2Cloud - Kapadokya'dan Global Pazara" Teması* *Takım: **Vertex***

---

## 📌 Proje Bağlantıları
* 🎥 **Demo Videosu (Loom/YouTube):** [(https://youtu.be/DLSSLCoz8os)]
* Animasyon Videosu (Youtube): [(https://youtu.be/HDiMiwWtfOo)]
* 🌐 **Canlı Demo (Vercel):** [(https://vertex-antrum-8rvm.vercel.app/)]
* 📂 **GitHub Repo:** [Repo Linki]

---

## 💡 1. Projenin Özü: "Rakiplerin Hiç Düşünmediği Modül"
Kapadokya'daki doğal tüf depolar, yapay soğuk hava depolarının kompresörlerle yaptığı iklimlendirme işini **%0 enerji** harcayarak yapar. ANTRUM, bu devasa enerji tasarrufunu (kWh/m³) ISO 14064 standartlarına göre hesaplar, karbon kredisine dönüştürür ve küresel piyasalarda satar. 

## 💰 2. Tam Entegre 3 Eksenli Gelir Modeli
Sistem, depo sahipleri için sadece bir iklimlendirme platformu değil, kapsamlı bir "Finansal İşletim Sistemi"dir. Depo sahibi alanını sisteme kaydettiğinde tek bir ekrandan üç farklı kazanç elde eder:
1. **Fiziksel Kira Geliri:** Depolanan ürünün tonajı ve süresi (ay) üzerinden alınan standart depo kirası.
2. **Karbon Kredisi Getirisi:** Önlenen elektrik tüketimi ve sıfırlanan soğutucu gaz kaçaklarından elde edilen kredinin (Verra/Gold Standard) global havayollarına (CORSIA) satışı.
3. **Lojistik Komisyonu:** Platformun akıllı rota algoritmasıyla çekilen nakliye operasyonlarından alınan pay.

## ⚙️ 3. Hackathon Zorunlu Kurallarının (Bonus) Entegrasyonu
Komite tarafından belirlenen 3 teknik zorunlu kural, birbirini besleyen bir hesap zincirinde **"Bonus Puan"** kurgusuyla birleştirilmiştir:

1. **Kural 3 (Coğrafi Veri & Dinamik Rota):** Sabit (hardcoded) lokasyon verisi kullanılmamıştır. Kullanıcı çıkış şehrini ve hedef depoyu seçtiğinde, **Leaflet.js** ve **OSRM (OpenRouteService)** ile mesafe dinamik çizilir. Haritada tıklanan konumların adresleri **Nominatim API (Reverse Geocoding)** ile anlık tespit edilir.
2. **Kural 1 (Coğrafi Karbon İzi):** OSRM'den çekilen rota (km) ve yük tonajı ile lojistik nakliye emisyonu hesaplanır. Bu lojistik emisyon yükü, deponun sağladığı brüt karbon tasarrufundan düşülerek şeffaf ve kanıtlanabilir **"Net Karbon Kazancı"** elde edilir.
3. **Kural 2 (Canlı Döviz Kuru):** Kazanılan global karbon kredileri, **TCMB XML Servisi** (Fallback: ExchangeRate-API) üzerinden çekilen anlık USD/TRY kurlarıyla çarpılarak, kullanıcılara çift para birimli (₺ ve $) raporlanır.

## 🧮 4. Bilimsel Altyapı ve Sertifikalı Raporlama
Hesaplamalarımız endüstriyel gerçekliğe dayanır:
* **Hacim Bazlı Standart:** Karbon motorumuz m² değil, GCCA küresel soğuk zincir standartları olan **m³** bazlı çalışır.
* **Şeffaflık İlkesi:** Doğal depoların %0 enerji harcadığı iddia edilmez; aydınlatma ve fanlar için **5 kWh/m³** operasyonel yük brüt tasarruftan düşülür.
* **PDF Sertifikasyon Raporu:** Sistem, ISO 14064-2 standartlarına uygun teknik parametreleri ve ekonomik öngörüleri içeren, yazdırılabilir anlık PDF "Teknik Analiz Raporları" üretir.

## 📱 5. Kusursuz Kullanıcı Deneyimi (Mobil İlk Yaklaşım)
Sistemimiz; **"Aydınlık Doğa (Light Nature)"** teması ve **Glassmorphism** UI mimarisi ile tasarlanmıştır. Telefon ve tabletler için %100 uyumlu "Responsive Hamburger Menü", reaktif veri grafikleri ve gelişmiş kullanıcı panelleri (API Yönetimi, Bildirim Ayarları) içermektedir.

## 🌐 6. API Ekosistemi (Canlı Veri Akışı)
* **Open-Meteo Live API:** Nevşehir'in anlık dış sıcaklık ve nem verisiyle karbon simülasyonunu anlık günceller.
* **Open-Meteo Archive API:** Raporlar sekmesinde son 1-12 aylık *gerçek* hava koşulları çekilerek, geçmiş tasarruf raporu dinamik oluşturulur.
* **OSRM & Nominatim:** Canlı lojistik ve adres sorgulama.
* **TCMB / ExchangeRate-API:** Canlı kur çevirileri.

## 🏗️ 7. Sistem Mimarisi (Architectural Diagram)

```mermaid
graph TD
    A[Open-Meteo API / İklim] -->|Sıcaklık & Nem| B(ISO 14064 Karbon Motoru)
    C[OSRM API / Lojistik] -->|Nakliye Emisyonu| B
    B -->|Net Kredi| D[Verra / Gold Standard]
    D --> E(TCMB Canlı Kur API)
    E -->|Kira + Karbon Geliri| F[Responsive Glassmorphism UI]
    F -->|In-Memory State| G[(Depo & Kapasite Veritabanı)]
