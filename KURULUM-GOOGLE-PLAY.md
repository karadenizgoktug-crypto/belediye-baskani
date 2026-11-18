# Belediye Başkanı → Google Play: Adım Adım Rehber

Bu klasör, oyunun **Android uygulama projesidir** (Capacitor 8, Android 16 / API 36 hedefli).
Bilgisayarına Android Studio kurmana gerek yok: uygulama, **GitHub'ın ücretsiz sunucularında** otomatik derlenir.

Toplam süre: ~30 dakika kurulum + Google'ın kimlik onayı + 14 günlük kapalı test.

---

## 0. Önce Google Play hesabının doğrulamalarını bitir

Play Console ana sayfasındaki 4 adım: kimlik belgesi, satıcı statüsü, Android cihaz (Play Console uygulamasına giriş), telefon.
Bunlar bitmeden "Uygulama oluştur" düğmesi açılmaz. Aşağıdaki 1–4. adımları bu sırada yapabilirsin.

---

## 1. GitHub hesabı ve depo

1. https://github.com/signup adresinden ücretsiz hesap aç (varsa giriş yap).
2. Sağ üstte **+ → New repository**.
   - Repository name: `belediye-baskani`
   - **Public** seç (ücretsiz GitHub Pages ile gizlilik politikası sayfasını yayınlamak için gerekli).
   - "Create repository".

## 2. Dosyaları yükle

1. Yeni depoda **"uploading an existing file"** bağlantısına tıkla.
2. Bu klasörün (`belediye-baskani-app`) **içindeki her şeyi** sürükleyip bırak:
   `android`, `docs`, `www`, `.github`, `package.json`, `package-lock.json`, `capacitor.config.json`, `.gitignore`, bu rehber.
3. Aşağıdan **Commit changes**.

> ⚠️ Mac'te `.github` ve `.gitignore` gibi noktayla başlayan klasörler gizli olduğu için sürüklenmeyebilir (Finder'da göstermek için **Cmd + Shift + .**).
> Yüklendikten sonra depoda `.github/workflows/android.yml` görünmüyorsa: **Add file → Create new file**, ad olarak
> `.github/workflows/android.yml` yaz ve bu klasördeki aynı dosyanın içeriğini yapıştırıp kaydet.

## 3. İmza anahtarını GitHub'a gizli değer olarak ekle

Ayrı gönderdiğim **IMZA-ANAHTARI** klasöründe 3 dosya var. Depoda:
**Settings → Secrets and variables → Actions → New repository secret**

| Name | Secret (değer) |
|---|---|
| `KEYSTORE_BASE64` | `upload-keystore.base64.txt` dosyasının **tüm içeriği** (tek satır, uzun metin) |
| `KEYSTORE_PASSWORD` | `sifre.txt` içindeki `KEYSTORE_PASSWORD=` sonrasındaki şifre |

> 🔐 `upload-keystore.jks` ve şifreyi **kaybetme ve kimseyle paylaşma**. Bilgisayarında + bir yedekte (ör. şifreli bulut/USB) sakla.
> Güncellemeleri hep bu anahtarla imzalayacağız. (Kaybedersen Play Console'dan "yükleme anahtarı sıfırlama" istenebilir ama zahmetlidir.)
> Bu dosyaları **depoya yükleme**; sadece yukarıdaki gizli değerler olarak ekle.

## 4. Uygulamayı derle (.aab)

1. Depoda **Actions** sekmesi → (sorarsa "I understand… enable") → soldan **"Android uygulamasını derle"** → **Run workflow → Run workflow**.
2. 5–10 dakika bekle; yeşil ✓ olunca çalışmaya tıkla.
3. Sayfanın altındaki **Artifacts** bölümünden `belediye-baskani-android-N` dosyasını indir ve zip'i aç:
   - `app-release.aab` → **Google Play'e yüklenecek dosya**
   - `app-release.apk` → Android telefonuna doğrudan kurup deneyebileceğin sürüm (telefonda "bilinmeyen kaynaklara izin ver" gerekir)

> Kırmızı ✗ olursa hata sayfasının ekran görüntüsünü bana gönder, düzeltelim.
> Her yeni yüklemede (oyunu güncellediğimizde) sürüm numarası kendiliğinden artar.

## 5. Gizlilik politikası sayfasını yayınla

1. Depoda **Settings → Pages**.
2. Source: **Deploy from a branch**, Branch: **main**, klasör: **/docs** → Save.
3. 1–2 dakika sonra adresler:
   - Gizlilik politikası: `https://KULLANICI-ADIN.github.io/belediye-baskani/gizlilik.html`
   - Oyunun web sürümü: `https://KULLANICI-ADIN.github.io/belediye-baskani/` (test kullanıcılarına da gönderebilirsin; ana ekrana eklenebilir)

## 6. Play Console'da uygulamayı oluştur (doğrulamalar bittikten sonra)

1. **Uygulama oluştur**: Ad `Belediye Başkanı: Şehir Oyunu`, varsayılan dil **Türkçe**, **Oyun**, **Ücretsiz**, beyanları işaretle.
2. **Mağaza girişi**: `store/MAGAZA-METINLERI.md` içindeki metinler + `store/final` klasöründeki görseller.
3. **Uygulama içeriği** formları: aynı dosyadaki cevap tablosu.

## 7. Kapalı test (kişisel hesaplar için zorunlu: 12 kişi, 14 gün)

1. **Test → Kapalı test → Parça oluştur** (ör. "Arkadaşlar").
2. **Test kullanıcıları**: e-posta listesi oluştur, **en az 12** Gmail adresi ekle (fazlası iyi olur: 15–20).
3. **Yeni sürüm oluştur** → `app-release.aab` dosyasını yükle → sürüm notu: `İlk sürüm` → incelemeye gönder.
   (İlk yüklemede Google "Play Uygulama İmzalama"yı açar; **kabul et**, uygulamanın asıl imza anahtarını Google saklar.)
4. Onaylanınca çıkan **katılım bağlantısını** test kullanıcılarına gönder: bağlantıdan katılıp Play Store'dan uygulamayı indirsinler ve
   **14 gün boyunca katılımda kalsınlar** (ara sıra oynasınlar).
5. 14 gün dolunca Play Console'da **"Üretime erişim için başvur"** düğmesi açılır; birkaç soruyu yanıtla → onay → **Üretim** sürümü yayınla. 🎉

---

## Klasör yapısı

```
www/                 → Oyun (Android uygulamasının içindeki dosyalar)
docs/                → GitHub Pages: gizlilik politikası + oyunun web sürümü
android/             → Android projesi (simgeler, açılış ekranı, imza ayarları)
.github/workflows/   → Otomatik derleme tarifi
capacitor.config.json
```

Oyunu güncellemek istediğimizde: yeni `www/index.html` (ve `docs/index.html`) dosyasını depoya yükle → Actions yeni `.aab` üretir → Play Console'da yeni sürüm olarak yükle.
