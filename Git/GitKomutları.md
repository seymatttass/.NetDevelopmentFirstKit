# Git Komutları

* Belirli bir klasörü repodan kaldır
```razor
git rm -r InvoiceDetails.API
git commit -m "Remove InvoiceDetails project from repo"
git push origin main  # Aktif branch neyse onu yaz
```

* Windows ve Linux için klasör silme
* Windows PowerShell:
```razor
Remove-Item -Recurse -Force .\InvoiceDetails.API\
Remove-Item -Recurse -Force .\ShippingDetails.API\
# Linux/MacOS terminal:
rm -rf ShippingDetails.API
```

* Remote branch ile merge et (local kodu koruyarak)
```razor
git fetch origin
git merge origin/master --strategy=ours
git commit -m "Merged remote but kept local code"
git push origin master
```

* Local branch’i sıfırla (Tüm değişiklikler silinir)
```razor
git reset --hard origin/master     # Remote'a birebir eşitle
git clean -fd                      # Untracked dosyaları da temizle
```

* Remote’dan en güncel kodları çek
```razor
git pull origin master
```
* Değişiklikleri commitle ve pushla
```razor
git add .
git commit -m "Erenbey branch'inde değişiklikleri tamamladım"
git push origin Erenbey
```

* Durum ve branch kontrol komutları
```razor
git status         # Değişiklikleri gösterir
git branch         # Branch listesini verir
git pull origin master   # Remote master'dan kod çeker
```
