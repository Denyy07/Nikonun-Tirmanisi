# Niko'nun Tırmanışı (Niko's Climb)

Niko'nun Tırmanışı, dikey bir platformda engellerden kaçarak zümrüt topladığınız, minimalist ve yüksek tempolu bir mobil web oyunudur.

## 🎮 Temel Amaç

Dikenli engellere çarpmadan mümkün olan en yüksek skora ulaşmak için karakteri (Niko) yukarı doğru tırmandırmak.

## 🕹 Nasıl Oynanır

- **Başlat:** Ana menüde "Başla" butonuna dokunarak/tıklayarak oyunu başlat.
- **Wall Jump (Zıplama):** Niko bir duvara yapışıkken ekrana dokun/tıkla → karşı duvara doğru zıplar.
- **Double Jump (Çift Zıplama):** Niko havadayken ekrana bir kez daha dokun/tıkla → **yönü anında tersine döner**, böylece önündeki bir dikenden kaçılabilir.
- **Yörünge Göstergesi:** Duvardayken ekranda görünen kesikli çizgi, bir sonraki zıplamada izlenecek yörüngeyi önceden gösterir.
- **Zümrüt** topla, skor kazan; **dikene** çarparsan ya da hiçbir duvara tutunamadan düşersen oyun biter.
- Oyun bitince "Tekrar Oyna" ile sıfırdan başlanabilir.
- Kontroller hem dokunmatik (`touchstart`) hem fare (`mousedown`) ile çalışır; masaüstü ve mobilde aynı şekilde oynanabilir.

## ⚙️ Öne Çıkan Mekanikler

- **Wall Jump:** Ekrana dokunarak duvardan duvara seri zıplamalar.
- **Double Jump:** Havada yön değiştirerek imkânsız gibi görünen engelleri aşma.
- **Dinamik Kamera:** Karakter yukarı tırmandıkça dünyayı takip eden akıcı kamera sistemi.
- **Yörünge Göstergesi:** Zıplama rotasını önceden gösteren görsel rehber.
- **Onboarding Menüsü:** Yeni oyuncular için "Nasıl Oynanır?" ekranı.

## 🛠 Teknik Mimari

- **Teknolojiler:** Vanilla JavaScript, HTML5 Canvas API, CSS3.
- **Sıfır Bağımlılık:** Proje harici hiçbir kütüphane veya resim dosyası içermez. Tüm oyun varlıkları (karakter, zümrüt, diken) SVG Data URL formatında doğrudan kaynak koduna gömülüdür; bu da projeyi tek dosyalık ve taşınabilir kılar.
- **Game Loop:** `requestAnimationFrame` tabanlı, delta-time ile kare hızından bağımsız hareket.
- **Responsive:** `devicePixelRatio` desteği, `#game-wrapper` ile masaüstünde ortalanmış/max-width 420px, mobilde tam ekran dikey görünüm; yatay taşma yok.

## 🐞 Bilinen Eksiklikler

- Seviye (level) kavramı yok; tek bir zorluk eğrisi var, oyun ilerledikçe zorluk artmıyor.
- Ses/müzik efekti bulunmuyor.
- Yerel/genel skor tablosu (leaderboard) veya en yüksek skor kaydı yok.
- Diken/zümrüt spawn algoritması tamamen rastgele; hesaplanmış bir zorluk dengesi (difficulty curve) yok.
- Çarpışma kutuları (hitbox) basit AABB (dikdörtgen) mantığıyla çalışıyor, SVG'lerin gerçek şekline göre değil.

## 🚀 Gelecek İyileştirme Planları

- Niko için karakter animasyonları ve akıcı geçiş efektleri.
- Farklı görsel temalara sahip yeni haritalar.
- Oyun ilerledikçe hızlanan tempo ve daha karmaşık tuzak türleri (zorluk eğrisi).
- Kişisel skor tablosu.

## 🎯 İlham Kaynakları ve Özgün Farklarımız

**İlham Kaynakları:**
- **Doodle Jump:** Dikey tırmanış dinamiği ve sürekli yükselen platform yapısı.
- **Flappy Bird:** Tek dokunuşla (tap-to-action) yüksek tempo ve refleks odaklı oyun döngüsü.

**Bizi Farklı Kılan Özgünlükler:**
- **Stratejik Hareket:** Klasik dikey oyunların aksine, Double Jump (havada yön değiştirme) mekaniği ile oyuncuya sadece refleks değil, engellerden kaçmak için taktiksel karar verme yetkisi tanıdık.
- **Yörünge Tahmini:** Oyuncuya kesikli çizgilerle zıplama rotasını görme imkânı sunarak, oyunu "şans faktöründen" çıkarıp "öngörülebilir strateji" oyununa dönüştürdük.
- **Dinamik Zorluk ve Risk-Ödül:** Duvar kayma hızı ve engellerin yerleşimi, oyuncuyu sürekli hareket etmeye zorlayan ve hata payını minimize eden bir denge üzerine kuruludur.

---

## 🧠 Yapay Zeka ile Geliştirme Süreci

Bu proje, birden fazla yapay zeka aracıyla **"Pair Programming" (İkili Programlama)** yapılarak, **Vibe Coding** yaklaşımıyla geliştirilmiştir.

**Kullanılan araçlar ve amaçları:**
- **Gemini** → Oyunun tamamının kod yazımı: SVG asset üretimi, Canvas API tabanlı oyun mantığı (wall-jump, double-jump, kamera, spawn sistemi), UI/UX tasarımı ve responsive (masaüstü + mobil) arayüz kurulumu.
- **Claude** → `README.md` dosyasının hazırlanması ve projeye ait metinsel içeriklerin (nasıl oynanır, bilinen eksiklikler, ilham kaynakları, AI kullanım dokümantasyonu vb.) düzenlenmesi/derlenmesi.

Süreç boyunca aşağıdaki konularda yapay zeka ile iteratif bir geri bildirim döngüsü kurulmuştur:
- 3 adet SVG asset üretimi (karakter, zümrüt, diken) — her biri **ayrı promptla**
- Canvas API tabanlı oyun döngüsü (game loop) kurulumu
- Wall-jump / double-jump fizik mekaniği
- Responsive, masaüstü + mobil uyumlu arayüz
- Onboarding ("Nasıl Oynanır?") menüsü

Aşağıda geliştirme sürecinde kullanılan **tam prompt/konuşma geçmişi**, kronolojik sırayla yer almaktadır.

### 1) SVG Asset Üretimi — Sistem Talimatı

```
Sen uzman bir UI/UX tasarımcısı ve Front-End geliştiricisin. Bir mobil web oyunu için
[Yeşil, parlayan basit bir zümrüt] tasarlamanı istiyorum.

Kurallar:
1. Sadece, kopyalayıp HTML dosyama yapıştırabileceğim tek parça, temiz bir <svg> kodu ver.
2. Tasarım 'Flat Design' (Düz tasarım) ve minimalist olsun. Karmaşık yollardan
   (complex paths) ve degradelerden (gradients) kaçın.
3. Etiket width="32" height="32" viewBox="0 0 32 32" içersin.
4. Arka planı kesinlikle olmasın (transparent).
5. Kodun dışına hiçbir açıklama metni yazma, sadece kodu ver.
```

### 2) Asset 1 — Karakter (Niko)

**Prompt:**
```
Create a minimalist 2D SVG vector graphic of a black-furred assassin cat
character's face. It should have a circular dark grey/black head, pointy ears,
and glowing bright green eyes. Keep the design extremely simple, flat, and
scalable. No background.
```
→ AI, yukarıdaki sistem talimatına uygun tek parça `<svg>` kodu döndürdü.

### 3) Asset 3 — Duvar Dikeni (Spike)

**Prompt:**
```
Create a simple 2D SVG graphic of a sharp red spike or thorn attached to a wall.
It should be geometric, pointing left or right, using dark red colors.
Flat design, no background.
```
→ AI, geometrik, koyu kırmızı tonlarda tek parça `<svg>` kodu döndürdü.


### 4) Asset Entegrasyonu — JS Data URL Dönüşümü

**Prompt:**
```
bu svgleri oyunuma eklemem için js url formatına çevir
```
**AI yanıtı (özet):** Üç SVG, URI-encode edilerek `data:image/svg+xml,...` formatında tek satırlık JS sabitlerine (`nikoUrl`, `emeraldUrl`, `spikeUrl`) dönüştürüldü; `new Image()` ile Canvas'a çizilebilir hale getirildi.

**Yapılan düzeltmeler (adayın kendi değerlendirmesi):** Üretilen 32×32 SVG'ler doğrudan mevcut `player.size = 32` / `entities[].width/height = 32` değerleriyle örtüştüğü için boyut değişikliği gerekmedi; renk paleti (`#2ecc71`, `#58d68d` yeşil tonları) oyunun genel HUD/buton renk şemasıyla tutarlı olduğu için olduğu gibi bırakıldı.

### 5) Oyun İskeleti (Game Loop) Kurulumu

**Prompt:**
```
Bir staj değerlendirmesi için tek bir HTML dosyasında çalışan, vanilla JS ve
HTML5 Canvas API kullanan bir mobil oyun yapacağım. Bana sadece
requestAnimationFrame kullanan, ekranı dikey (portrait) modda sabitleyen temiz
bir Game Loop (update ve draw fonksiyonları) iskeleti oluştur. Şimdilik içine
oyun mantığı ekleme, sadece responsive mobil yapıyı kur.
```
→ AI, `resize()` (DPR desteği), boş `update()`/`draw()` ve `requestAnimationFrame` tabanlı temel iskeleti üretti.

### 6) Wall-Jump Temel Mekaniği + Spawn Sistemi

**Prompt:**
```
Şimdi bu iskelete temel mekaniği ekleyelim. Karakter dikey iki duvar arasında
sıkışmış olsun. Ekrana dokunulduğunda karakter belli bir ivmeyle karşı duvara
doğru fırlasın. Karakter yukarı çıktıkça kamera (oyun dünyası) aşağı kaysın.
Ayrıca sağ ve sol duvarda rastgele dikenler ve orta alanda toplanabilir
zümrütler üreten bir 'spawn' fonksiyonu yaz.
```
→ AI; `player` fizik objesi (yerçekimi, zıplama kuvveti, duvar çarpışması), kamera takibi ve `spawnEntities()` fonksiyonunu ekledi. Bu adımda ölüm mekaniği yerine geçici olarak "skor sıfırlama" kullanılmıştı.

### 7) Başlangıç / Bitiş Ekranı

**Prompt:**
```
bize bir başlama bir bitiş ekranı lazım
```
→ AI, Canvas üzerine değil DOM overlay (`#ui-overlay`, `#hud`) katmanı önererek `gameState` (START/PLAYING/GAME_OVER) durum makinesi ve `resetGame()` / `gameOver()` fonksiyonlarını ekledi; diken çarpması artık gerçek "oyun bitti" durumuna bağlandı.

### 8) Masaüstü/Mobil Uyumlu Kapsayıcı (Wrapper)

**Prompt:**
```
Oyun şu an tarayıcıda tam ekran (100% width/height) çalışıyor ancak bu mobil
odaklı dikey bir oyun. Masaüstü tarayıcılarda açıldığında tüm ekrana yayılmasını
istemiyorum.

Lütfen CSS ve resize() fonksiyonunu şu şekilde güncelle:
- Oyun alanı (Canvas ve UI elementleri) ekranın tam ortasında sabitlensin.
- Oyun alanının maksimum genişliği (max-width) 420px olsun ve etrafında hafif
  bir gölge (box-shadow) bulunsun.
- Tarayıcı arka planı farklı koyu bir renk (#111), oyun alanının kendi arka
  planı (#1a1a1a) olsun.
- window.innerWidth yerine sadece bu ortalanmış oyun konteynerinin (örneğin bir
  #game-wrapper div'i) genişliğini ve yüksekliğini referans alarak oyunu çizdir.
```
→ AI, `#game-wrapper` (max-width: 420px, flexbox ile ortalama) ekledi; `resize()` fonksiyonu `window` yerine `wrapper.clientWidth/clientHeight` referans alacak şekilde güncellendi; input dinleyicileri de `window`'dan `wrapper`'a taşındı.

### 9) Yörünge Göstergesi + Double Jump

**Prompt:**
```
oyuncu zıplarken zıplama açısını görmesi için bir açı metresi tarzı birşey ekle

oyunda bazen traplar ard arda olabiliyor bunu geçmek için heromuza bir double
jump özelliği ekle
```
→ AI, "açı metresi" isteğini dinamik bir **tahmini yörünge çizgisi** (`drawTrajectory`) olarak yorumladı ve havadayken ikinci dokunuşla ek bir zıplama hakkı veren `canDoubleJump` mantığını ekledi.

**Adayın sorguladığı/değiştirdiği kısım:** İlk üretilen double-jump kodunda karakter havada sadece dikey (Y ekseni) yönde hafif zıplıyor, yatay yönünü (`vx`) değiştirmiyordu — bu da dikenlerden kaçmayı işlevsiz kılıyordu. Bu, aşağıdaki prompt ile AI'a geri bildirildi:

```
Görsel entegrasyon ve yörünge çizgisi harika olmuş. Etrafta çıkan yeşil Double
Jump göstergesi de güzel, kalabilir. Ancak Double Jump mekaniğinde kritik bir
fizik hatası var.

Karakter havadayken tıkladığımda sadece Y ekseninde hafifçe zıplıyor ama yön
değiştirmiyor (vx sabit kalıyor). Oyuncunun dikenlerden kaçabilmesi için havada
tıklandığında player.vx değerinin tam tersine (negative/positive) dönmesi, yani
karakterin geldiği duvara doğru geri fırlaması gerekiyor. Lütfen handleInput
içindeki Double Jump mantığını, karakterin X eksenindeki hızını tersine
çevirecek şekilde güncelle.
```
→ AI, `handleInput()` içinde `player.vx = -player.vx;` satırını ekleyerek düzeltti. **Bu, şartnamenin "önerilen çözümler sorgulanmalı, gerektiğinde adayın kendi değerlendirmesiyle değiştirilmeli" maddesine karşılık gelen somut örnektir:** ilk AI çıktısı test edildi, oynanışı bozan bir fizik hatası tespit edildi ve AI'a spesifik olarak geri bildirildi.

### 10) Onboarding ("Nasıl Oynanır?") Menüsü

**Prompt:**
```
Gayet güzel şimdi oyuna yeni girenler ve açıklamayı okumayanlar için başlat
menüsünün yanına nasıl oynanır tarzında bir menü ekleyelim burada ekrana
tıklayınca nikonun zıpladığını, zıpladıktan sonra havada bir kere daha ekrana
tıklanıldığında ya da dokunulduğunda double jump yaptığını yazalım
```
→ AI; ana menüye ikincil bir "Nasıl Oynanır?" butonu, `#help-menu` panelini ve `main-menu` / `help-menu` arasında geçiş yapan `helpBtn` / `backBtn` olay dinleyicilerini ekledi. Mobil dokunma alanlarını büyütmek için butonlar yan yana değil **alt alta** (dikey buton grubu) yerleştirildi.

### Sorgulanan / Değiştirilen AI Önerileri (Özet)

| AI'ın ilk önerisi | Neden sorgulandı | Adayın değişikliği |
|---|---|---|
| Diken çarpınca skor sıfırlanıp oyuna devam edilmesi | Gerçek bir "kaybetme" hissi vermiyordu, şartnamedeki "kazanma-kaybetme" beklentisiyle örtüşmüyordu | Sonraki iterasyonda `gameOver()` durumuna bağlanarak gerçek bitiş ekranı kuruldu |
| Double jump'ta sadece dikey zıplama (`vx` sabit) | Test edilince art arda gelen dikenlerden kaçışı işlevsiz kıldığı görüldü | `player.vx = -player.vx;` ile yön tersine çevrilecek şekilde düzeltildi |
| `resetGame()` sonrası "Nasıl Oynanır?" butonunun gizli kalması *(kod incelemesi sırasında fark edilen bug)* | Oyun bir kez bitirildikten sonra bu buton bir daha hiç görünmüyordu | `resetGame()` içine `helpBtn.classList.remove('hidden')` eklenerek düzeltildi |

## 📁 Dosya Yapısı

```
oyun.html   → Tek dosyalık oyun (HTML + CSS + JS, harici bağımlılık yok)
README.md   → Bu dosya
```
