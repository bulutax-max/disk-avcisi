# Disk Avcısı

Ubuntu/Linux üzerinde büyük klasörleri ve yakın zamanda değişen dosyaları raporlayan Python aracı. Terminal ve Streamlit arayüzü içerir.

## Durum

Kişisel yardımcı araç / prototip. Depo düzeni 1 Ekim 2026'da temizlendi. Terminal taraması ile arayüzde boş sonuç işleme kontrol edilir; gerçek disklerde hız, izinler ve farklı Ubuntu sürümleri ayrıca değerlendirilmelidir.

## Terminal kullanımı

Python 3.10+ gerekir. Terminal sürümü Python standart kütüphanesini kullanır; ek Python paketi gerektirmez. GNU `du` varsa klasör boyutlarını onunla hesaplar.

```bash
python3 disk_avcisi.py --help
python3 disk_avcisi.py --largest 10 --path ~/Downloads --human
python3 disk_avcisi.py --changed 7 --limit 100 --path ~/Downloads --output recent.txt
```

`--depth` klasör tarama derinliğini, `--largest` sonuç sayısını belirler. `--output` verilirse belirtilen rapor dosyası oluşturulur veya üzerine yazılır.

## Streamlit arayüzü

Komutları depo klasöründen çalıştırın:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python -m streamlit run src/gui_streamlit.py --server.address 127.0.0.1
```

Terminalde gösterilen yerel adresi açın. Klasörü ve filtreleri seçip **Tara** düğmesine basın. Sonuçları CSV olarak indirebilirsiniz. Her yeni tarama dosyaları yeniden okur.

Arayüz, seçilen klasörün doğrudan alt klasörlerini toplam içerik boyutuna göre sıralar. Son değişen dosyalar alt klasörlerle birlikte taranır. Araç taranan dosyaları silmez.

## Depo düzeni

- `disk_avcisi.py`: terminal aracı.
- `src/core/scan.py`: arayüzün tarama işlevleri.
- `src/gui_streamlit.py`: web arayüzü.
- `requirements.txt`: yalnızca arayüz bağımlılıkları.

Sanal ortam ve Python önbellekleri kaynak kod olarak takip edilmez. Git geçmişindeki eski kopyalar korunur. Terminal ve arayüzün tarama kapsamı tamamen aynı değildir; özellikle `--depth` seçeneği terminal sürümüne aittir.

## Kontrol

Boş klasör, alt klasör içeren örnek veri, son değişen dosya listesi ve CSV indirme akışını kontrol edin. Erişim izni olmayan dosyalar sonuçları eksik bırakabilir.

1 Ekim 2026: geçici örnek klasörde terminalin büyük klasör ve son değişen dosya raporları; arayüzün tablo hazırlama işlevinde boş sonuç, klasör boyutu ve yeni dosyadan sonra yeniden tarama doğrulandı. Streamlit kurulamadığı için tam tarayıcı arayüzü ve CSV düğmesi etkileşimi bu ortamda test edilmedi.
