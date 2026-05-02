# Vertex-Antrum
ANTRUM by Team Vertex | Kapadokya Hackathon - Mağaraların doğal soğutma potansiyeliyle sıfır karbon salınımlı depolama ve 3 eksenli gelir modeli sağlayan ekosistem.

# 🚀 ANTRUM: Zero-Carbon Cave Storage & Exchange

*Kapadokya Hackathon 2026 | "Cave2Cloud - Kapadokya'dan Global Pazara" Teması* *Takım: **Vertex***

---

## 📌 Proje Bağlantıları (Teslimat Zorunlulukları)
* 🎥 **Demo Videosu (Loom/YouTube):** [Video Linki Buraya] *(Max 3 dk)*
* 🌐 **Canlı Demo (Vercel/Render):** [Canlı Yayın Linki Buraya]
* 📂 **GitHub Repo:** [Repo Linki]

---

## 💡 Projenin Amacı: Ne, Neden, Nasıl?

**Ne Yapıyoruz? (What)**
ANTRUM, Kapadokya'nın doğal yeraltı depolarının (tüf kayalar) sağladığı sıfır enerjili soğutma potansiyelini, modern lojistik ağı ve global karbon kredi piyasası ile birleştiren dijital bir B2B platformdur.

**Neden Yapıyoruz? (Why)**
Geleneksel soğuk hava depoları, lojistik maliyetlerinin ve küresel karbon salınımının en büyük etkenlerinden biridir. Kapadokya'nın doğal mağaraları ise %0 enerji ile doğal iklimlendirme sunar. Amacımız, bu yerel "doğal depo" gücünü dijitalleştirerek (Cave2Cloud), küresel sürdürülebilirlik hedefleri (ESG) doğrultusunda dünya pazarına bir karbon offset (dengeleme) ve kiralama aracı olarak sunmaktır.

**Nasıl Çalışıyor? (How)**
Platform, üretici ve lojistik firmalarını mağara sahipleriyle buluşturur. Açık kaynaklı harita API'leri kullanılarak lojistik rotası çizilir, taşınan yük ve mesafe bazında karbon ayak izi hesaplanır. Geleneksel depolama yerine doğal mağara tercih edildiği için tasarruf edilen karbon miktarı belgelendirilir ve TCMB canlı döviz kurları üzerinden global şirketlere karbon kredisi olarak fiyatlandırılır.

---

## ⚙️ Zorunlu Hackathon Kurallarının Entegrasyonu (Bonus Kurgusu)

Projemiz, hackathon komitesi tarafından belirlenen 3 teknik zorunlu kuralı birbirinden bağımsız bırakmak yerine, **"Bonus - Kuralların Birleşimi"** stratejisine uygun olarak tek bir hesap zincirinde birleştirmiştir:

* **Kural 3 (Coğrafi Veri):** Platformda `Nominatim` ve `OpenRouteService` (Açık kaynak) API'leri kullanılmıştır. Kullanıcı, ürünün çıkış noktasını ve Kapadokya'daki hedef mağarayı seçtiğinde, API üzerinden dinamik ve gerçek zamanlı rota/mesafe (km) hesaplaması yapılır. Asla statik (hardcoded) veri kullanılmamıştır.
* **Kural 1 (Coğrafi Karbon İzi):** OpenRouteService'den çekilen dinamik mesafe verisi ve yük miktarı, Hackathon referans emisyon faktörleri kullanılarak çarpılır.  
    *Formül:* `Mesafe (km) x Yük (ton) x Emisyon Faktörü (Örn: Kara-TIR için 0.100 kg CO2/ton-km) = Toplam Karbon Ayak İzi.`  
    Bu değer, geleneksel bir depo kullansalardı harcayacakları enerjiyle kıyaslanarak "Kazanılan Karbon Kredisi"ne dönüştürülür.
* **Kural 2 (Canlı Döviz Kuru):** Kazanılan karbon kredisi ve mağara kiralama bedelleri, `TCMB EVDS API` kullanılarak çekilen anlık döviz kurları (USD/EUR) ile TL'ye veya global pazar için dövize çevrilir. Kurlar arayüzde çift para birimi (₺ ve $) olarak gösterilir ve platformdaki "Kiralama Onayı" iş kararını doğrudan tetikler.

> **Bonus Akışı:** Coğrafi API ile Mesafe ➔ CO2 Hesabı ➔ Karbon Maliyeti TCMB Kuru ile TL/Döviz Karşılığı.

---

## 🏗️ Sistem Mimarisi (Architectural Diagram)

```mermaid
graph TD
    A[Kullanıcı/Lojistik Firması] -->|Rota Seçimi| B(OpenRouteService & Nominatim API)
    B -->|Dinamik Mesafe| C{Karbon Hesaplama Motoru}
    C -->|TIR: 0.100 çarpanı| D[Kurtarılan Karbon Miktarı]
    D --> E(TCMB EVDS API - Canlı Kur)
    E -->|Fiyatlandırma| F[Arayüzde Çift Para Birimi Gösterimi]
    F -->|İş Kararı| G[Mağara Kiralama & Karbon Kredisi Satışı]
