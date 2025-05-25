# 🤖 Yapay Zeka Desteği – Shadow Sprint

Oyunun temel akışını ve yapısını kendim oluşturdum. Ancak aşağıdaki konularda özellikle hesaplama, animasyon ve platform fiziği gibi teknik detaylar için yapay zekadan destek aldım. Aşağıda bana ait sorular ve aldığım cevaplar yer alıyor.

---

## 🎯 Prompt 1: Oyuncunun tek zıplamayla ulaşabileceği maksimum yüksekliği nasıl hesaplarım?

**Soru:** Sabit değerle değil, zıplama hızı ve yerçekimi değerine göre karakterin çıkabileceği yüksekliği otomatik hesaplamak istiyorum.

**Cevap:** `h = v² / (2g)` formülünü kullanabilirsin. `ziplamaHizi` ve `yerCekimi` değerlerini bilerek, bu formülle karakterin her bir zıplamada çıkabileceği yüksekliği dinamik olarak belirleyebilirsin.

---

## 🎯 Prompt 2: Coin’ler aynı anda hareket ediyor, daha doğal görünmeleri için ne yapabilirim?

**Soru:** Coin'ler animasyonlu ama hepsi aynı anda sallanıyor. Her biri farklı zamanda dalgalansın istiyorum.

**Cevap:** Her coin’e `phase` (faz) ekleyebilirsin. `Math.sin(zaman + phase)` ile farklı zamanlarda hareket eden animasyonlar elde edersin. Böylece tüm coin'ler aynı anda yukarı-aşağı zıplamaz, daha doğal bir görüntü oluşur.

---

## 🎯 Prompt 3: Coin’lerde ışıldama efekti nasıl yapılır?

**Soru:** Coin'ler sadece sarı çiziliyor. Göz alıcı parlaklık efekti nasıl eklenebilir?

**Cevap:** `ctx.globalAlpha` ile coin üzerine ikinci bir iç daire çizebilirsin. Bu iç dairenin opaklığını `Math.sin()` ile zaman içinde değiştirerek parlayan bir etki yaratabilirsin.

---

## 🎯 Prompt 4: Dikey asansör platformlar bir noktaya geldiğinde durmalı, bunu nasıl yaparım?

**Soru:** Asansörler aşağı yukarı hareket ediyor ama doğru mesafede durmalarını ayarlayamıyorum. Matematiksel olarak nasıl sınırlarım?

**Cevap:** `offset` değeri, `range` kadar ileri veya geri hareket ettiğinde `offset = range`, `speed = 0` ve `dir = 0` olarak sıfırlayabilirsin. Bu sayede platform sınırına ulaştığında otomatik olarak durur.

---

## 🎯 Prompt 5: Platform bloklarının arası düzenli olmalı ama hesaplaması zor, nasıl yapabilirim?

**Soru:** Her platform segmenti için platformlar, yukarı ve aşağı asansörler eşit aralıklı ve hizalı olsun istiyorum. Bunu manuel değil, dinamik nasıl yaparım?

**Cevap:** `segmentUzunluk` gibi bir sabit oluşturup platform ve asansör konumlarını bu sabite göre hesaplayabilirsin. Her `i` döngüsünde `i * segmentUzunluk` ile tüm parçaları düzenli ve çakışmasız şekilde oluşturabilirsin.

---

## 🎯 Prompt 6: Karakterin zeminle çarpışmasını adım adım hesaplamak istiyorum. Nasıl yaparım?

**Soru:** Yüksek hızla düşerken karakter zeminin içine geçiyor. Bu sorunu azaltmak için ne yapabilirim?

**Cevap:** Düşüşü küçük adımlara bölebilirsin. Her adımda çarpışma olup olmadığını test ederek, zemini kaçırma riskini azaltırsın. Bunu yapmak için düşme miktarını örneğin 4 adıma bölüp her adımda çarpışmayı kontrol edebilirsin.

---

## 🎯 Prompt 7: Oyuncu bir platformda durduğunda yukarı çıkan platformla birlikte hareket etmeli mi?

**Soru:** Oyuncu hareketli bir platforma bindiğinde yukarı çıkması gerekiyor ama sabit kalıyor. Bunu nasıl bağlarım?

**Cevap:** Oyuncunun o anda üzerinde olduğu platformu bir değişkende (`asansorde`) tutarak, platformun hızına göre oyuncunun `y` değerini artırman gerekir. Bu sayede karakter platformla birlikte yukarı veya aşağı hareket eder.

---

## 🎯 Prompt 8: Ekranda onlarca yağmur damlası var, performans nasıl düşmeden gösterilir?

**Soru:** Yağmur parçacıkları her karede çiziliyor, ama çok fazlaysa yavaşlama oluyor. Ne yapmalıyım?

**Cevap:** Her damlaya sabit bir `hız` verip `y` konumunu ona göre güncelleyebilirsin. Canvas üzerinde çizilen çizgiler çok kısa olduğu için performansa aşırı etki etmez ama sayıyı 100–150 arasında tutmak idealdir. Ayrıca `requestAnimationFrame` zaten çizimleri optimize eder.

---

## 🎯 Prompt 9: Coin'ler karakterle çarpışınca toplanıyor ama ses bazen gecikiyor. Neden olabilir?

**Soru:** Coin sesi bazen çarpışma anında çalmıyor ya da gecikmeli geliyor. Bunun sebebi nedir?

**Cevap:** Aynı sesi tekrar çalmak için önce `ses.currentTime = 0` yapman gerekir. Aksi halde ses tamamlanmadan yeniden başlamaz. Her çalmadan önce sesi sıfırlarsan anlık ses efekti düzgün çalışır.

---

## 🎯 Prompt 10: Yüksek çözünürlüklü ekranlarda canvas tam dolmuyor, nasıl ayarlarım?

**Soru:** 1920x1080 gibi ekranlarda canvas boşluk bırakıyor veya küçülüyor. Tarayıcıya göre boyutu nasıl ayarlarım?

**Cevap:** `canvas.width = window.innerWidth` ve `canvas.height = window.innerHeight` komutlarıyla canvas'ı ekran boyutuna göre dinamik olarak ayarlayabilirsin. Ayrıca `window.addEventListener("resize", resizeCanvas)` kullanarak ekran boyutu değiştiğinde otomatik uyarlarsın.
