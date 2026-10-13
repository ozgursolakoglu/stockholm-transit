# Stockholm Transit – Live Digital Shadow

Stockholm metrosu (Tunnelbana) ve banliyö treni (Pendeltåg) için gerçek zamanlı verilerle çalışan bir pano. Yapay zekâ ve dijital ikiz derslerinde kullanılmak üzere hazırlanmıştır. Arayüz İngilizcedir.

**Özellikler**

- Metro (hat 10, 11, 13, 14, 17, 18, 19) ve banliyö treni (hat 40, 41, 43, 44) haritası, katmanlar ayrı ayrı açılıp kapatılabilir
- Trenlerin tahmini anlık konumu; 2 dakikadan fazla gecikenler kırmızı çerçeveli
- Arama kutusundan SL ağındaki herhangi bir istasyon veya durak (otobüs, tramvay, vapur dahil) seçilebilir
- Seçilen durak için göstergeler: next departure, departures in the next 30 min, average delay, on-time rate, trains due in 10 min, cancellations, kalkış tablosu, 10 dakikalık aralıklarla kalkış grafiği ve service alerts
- Schematic / Geographic görünümleri arasında geçiş
- Bağlantı yoksa otomatik simülasyon modu

Veri kaynağı: [SL Transport API](https://www.trafiklab.se/api/other-apis/sl/transport/) (API anahtarı gerektirmez). Verilerin kullanımı için SL/Trafiklab lisans koşullarına bakın.

## Nasıl çalışır?

Sayfa tamamen statiktir; sunucu kodu yoktur. `netlify.toml` dosyası, sayfanın `/v1/...` adresine yaptığı istekleri Netlify üzerinden SL'ye aktarır. Böylece tarayıcı aynı alan adıyla konuşur ve CORS sorunu oluşmaz.

## GitHub'dan Netlify'a yayınlama

1. Bu dosyaları bir GitHub reposuna yükleyin (`index.html`, `netlify.toml`, `README.md`, `.gitignore`).
2. [app.netlify.com](https://app.netlify.com) adresinde GitHub hesabınızla oturum açın.
3. **Add new site > Import an existing project > GitHub** adımlarını izleyin ve repoyu seçin.
4. Ayarları boş bırakın (Build command: boş, Publish directory: `.`). Ayarlar `netlify.toml` dosyasından okunur.
5. **Deploy**'a basın. Sayfa `https://SITE-ADI.netlify.app` adresinde yayına girer.

Bundan sonra GitHub'a yaptığınız her değişiklik Netlify'da otomatik olarak yeniden yayınlanır. Site adını **Site configuration > Change site name** bölümünden değiştirebilirsiniz.

## Sınırlamalar

- Trenlerin konumu GPS değildir; istasyonlardaki "sonraki tren" tahminlerinden hesaplanır.
- Banliyö treni hatlarının durak listeleri sadeleştirilmiştir. SL'de değişiklik olursa `index.html` içindeki `LINES` bölümünden düzenlenebilir.
- Bazı istasyon adları SL kayıtlarıyla eşleşmezse sağ üstteki mesajda listelenir.
- Sistem trenleri yalnızca izler, yönetmez: bu bir dijital ikiz değil, **dijital gölgedir**.
