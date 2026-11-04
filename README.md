# 🔐 Şifre Kasası

**Türkçe · [English](README.en.md)**

Tarayıcıda çalışan, tek dosyalık, kurulum gerektirmeyen kişisel şifre kasası.
Şifreler **cihazında AES-256-GCM ile şifrelenir** ve sadece senin sakladığın şifreli bir `kasa.json` dosyasında durur. Sunucu yok, hesap yok, takip yok.

**Hemen dene:** https://wolkansezer.github.io/sifre-kasasi/

<table align="center">
  <tr>
    <th colspan="2">🇹🇷 Türkçe</th>
    <th colspan="2">🇬🇧 English</th>
  </tr>
  <tr>
    <td><img src="docs/kilit.png" width="200" alt="Kilit ekranı"></td>
    <td><img src="docs/kasa.png" width="200" alt="Kasa ekranı (örnek verilerle)"></td>
    <td><img src="docs/lock-en.png" width="200" alt="Lock screen"></td>
    <td><img src="docs/vault-en.png" width="200" alt="Vault screen (sample data)"></td>
  </tr>
</table>

<sub>Ekran görüntülerindeki kayıtlar örnektir.</sub>

## Neden?

Hazır şifre yöneticileri harika ama bazen tam kontrol istersin: verinin nerede durduğunu bilmek, kodun tamamını tek dosyada okuyabilmek ve kasayı istediğin buluta (Google Drive, iCloud, USB bellek) koyabilmek. Şifre Kasası bunun için yapıldı.

## Özellikler

- **Uçtan uca şifreleme**: AES-256-GCM, anahtar ana şifreden PBKDF2-SHA256 ile **600.000 turda** türetilir
- **Tamamen yerel**: Şifreleme ve çözme tarayıcının Web Crypto API'si ile cihazında yapılır; sayfa hiçbir yere bağlanamaz (CSP ile `connect-src 'none'`)
- **Tek dosya**: HTML, CSS ve JavaScript tek `index.html` içinde, dış kütüphane yok
- **Güçlü şifre üretici**: Uzunluk ve sembol seçimiyle, şifre gücü göstergesi
- **Tek tuşla kopyalama**: Pano 30 saniye sonra otomatik temizlenir
- **Otomatik kilit**: 5 dakika işlem yapılmazsa kasa kilitlenir
- **Arama**: Başlık, adres, kullanıcı adı ve notlarda
- **CSV içe aktarma**: Chrome, Edge, Bitwarden vb. dışa aktarımlarından
- **Ana şifre değiştirme**
- **Mobil uyumlu**: iPhone ve Android'de ana ekrana eklenebilir
- **Türkçe ve İngilizce arayüz** (🌐 butonuyla değiştirilir), koyu tema

## Kullanım

### Çevrimiçi
GitHub Pages adresini aç: **https://wolkansezer.github.io/sifre-kasasi/**

### Çevrimdışı
`index.html` dosyasını indir ve tarayıcıda aç. İnternet gerekmez.

### İlk kurulum
1. **Yeni kasa** sekmesinden ana şifreni belirle.
2. Kayıtlarını ekle ve **💾 Kaydet**'e bas, `kasa.json` iner.
3. Bu dosyayı Google Drive, iCloud Drive ya da istediğin yere koy.

### Sonraki kullanımlar
**Kasayı aç** → `kasa.json` dosyasını seç → ana şifreni gir. Değişiklikten sonra kaydedip eski dosyanın üzerine yaz.

### Telefon ve bilgisayar arasında eşitleme
Senkronizasyon dosya üzerinden yapılır: her iki cihazda da Drive'daki aynı `kasa.json` dosyasını aç ve kaydet. Bilgisayarda *Google Drive for Desktop* kullanırsan Drive klasörüne kaydetmek yeterlidir. Aynı anda iki cihazda düzenleme yapma; son kaydedilen dosya geçerli olur.

## Güvenlik

| | |
|---|---|
| Şifreleme | AES-256-GCM (her kaydetmede yeni 96 bit IV) |
| Anahtar türetme | PBKDF2-HMAC-SHA256, 600.000 tur, 128 bit rastgele tuz |
| Rastgelelik | `crypto.getRandomValues` |
| Ağ erişimi | Yok (Content-Security-Policy ile engelli) |
| Saklama | Sadece kullanıcının kendi `kasa.json` dosyası |

Kasa dosyasının biçimi:

```json
{ "app": "sifre-kasasi", "v": 1, "kdf": "PBKDF2-SHA256", "iter": 600000,
  "salt": "…", "iv": "…", "ct": "…" }
```

> ⚠️ **Ana şifreni unutursan kasayı açmanın hiçbir yolu yoktur.** Kâğıda yazıp güvenli bir yerde sakla ve kasa dosyanın yedeğini tut.

> ℹ️ Bu proje kişisel kullanım için geliştirilmiştir ve bağımsız bir güvenlik denetiminden geçmemiştir. Kritik kullanımlar için Bitwarden ya da KeePassXC gibi denetlenmiş çözümleri de değerlendir.

## Lisans

[MIT](LICENSE)
