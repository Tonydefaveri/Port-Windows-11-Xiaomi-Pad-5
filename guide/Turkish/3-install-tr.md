<img align="right" src="https://raw.githubusercontent.com/erdilS/Port-Windows-11-Xiaomi-Pad-5/main/nabu.png" width="425" alt="Windows 11 Running On A Xiaomi Pad 5">


# Xiaomi Pad 5'te Windows Çalıştırma
> [!WARNING]
> **LÜTFEN YOUTUBE VEYA BAŞKA BİR PLATFORMDAKİ GÜNCEL OLMAYAN VİDEO REHBERLERİNİ KULLANMAYIN! BU VİDEOLAR ESKİDİR VE BUNLARI KULLANARAK CİHAZINIZI BRICK EDEBİLİRSİNİZ! EĞER BİR VİDEO REHBERİNE İHTİYACINIZ VARSA, [ArtoSeVeN](https://www.youtube.com/channel/UCYjwfxlYlJ7Nnzv01oszQvA) TARAFINDAN HAZIRLANAN BU [YENİ VİDEO REHBERİNİ](https://youtu.be/BbgTbTGbXYg) KULLANIN**


## Windows Kurulumu
> [!NOTE]
> Şimdi CMD veya powershell'i yönetici olarak açmanız ve ardından -yolunu klasörün gerçek yolu ile değiştirdiğiniz- `cd C:\gerçek\yol\platform-tools` komutunu kullanarak platform-tools klasörüne erişmeniz önerilir .
> Tüm kılavuz boyunca aynı pencereyi kullanın, pencereyi kapatmayın.

### Gerekli Dosyalar

- ```Beyin```
  
- [```UEFI imajı```](https://github.com/erdilS/Port-Windows-11-Xiaomi-Pad-5/releases/download/UEFI/uefi-v3.img)

- [```ARM Windows esd```](https://worproject.com/esd) (Şu seçenekleri seçin: Version: ```11``` | Build: ```22631.2861``` | Architecture: ```ARM64``` | Edition: ```CLIENT``` | Language:  ```istediğiniz dil```)
  
- [```Sürücüler (driverlar)```](https://github.com/map220v/MiPad5-Drivers/releases/latest)


### Windows'u kurmaya başlamak için recovery'e boot edin

```cmd
fastboot boot <recovery.img>
```

#### msc çalıştırın

> Sizden komutu bir kez daha çalıştırmanızı dair uyarı gelirse, bunu yapın

```cmd
adb shell msc
```

### Disklere harf atayın

  
#### Diskpart'ı (Windows disk yönetimini) başlatın

```cmd
diskpart
```


### Windows volümüne (volume) `X` harfini atayın

#### Tabletinizdeki Windows volümünü seçin
> Bunu bulmak için `list volume` komutunu kullanabilirsiniz, "WINNABU" isimli volümdür.

```diskpart
select volume <volume numarası>
```

#### X harfini atayın

```diskpart
assign letter x
```

### ESP volümüne `Y` harfini atayın

#### Tabletteki ESP bölümünü seçin
> Bunu bulmak için `list volume` komutunu kullanabilirsiniz, "ESPNABU" isimli volümdür.

```diskpart
select volume <volume numarası>
```

#### Y harfini atayın

```diskpart
assign letter y
```

### Diskpart arayüzünden çıkın.

```diskpart
exit
```



### Kurulum işlemi

<gerçek\yol\install.esd>` yerine install.esd dosyasının bulunduğu gerçek yolu yazın (install.wim olarak da adlandırılmış olabilir)

```cmd
dism /apply-image /ImageFile:<gerçek\yol\install.esd> /index:6 /ApplyDir:X:\
```

> Eğer `Error 87` hatası alırsanız, `dism /get-imageinfo /ImageFile:<gerçek\yol\install.esd>` komutu ile imajınızın indexini (dizinini) kontrol edin, ardından `index:6` yerine imajınızdaki Windows 11 Pro'nun gerçek index numarasını yazın



### Sürücü kurulumu

> Sürücüleri [buradan](https://github.com/map220v/MiPad5-Drivers/releases/latest) indirebilirsiniz 

> Eğer `"Automatic WINNABU detection failed! Enter Drive Letter manually"` diyorsa **`X`** yazın

```cmd
 Sürücülerin bulunduğu klasörü açın ve OfflineUpdater.cmd dosyasını çalıştırın
```



### EFI için Windows bootloader dosyalarını oluşturun

> Boot dosyalarını kopyalarken bir hata oluşursa, ESPNABU'nun hala Y harfine sahip olup olmadığını kontrol edin. Eğer Y harfine sahip değilse, başka bir harf (mesela K) ekleyin ve aşağıdaki komuttaki Y'yi sırasıyla söz konusu harfle değiştirin

```cmd
bcdboot X:\Windows /s Y: /f UEFI
```

## ESPNABU'nun harfini kaldırın
> Eğer bu işe yaramazsa, bunu görmezden gelin ve bir sonraki komuta geçin. Bu hayalet sürücü bilgisayarınızı bir sonraki yeniden başlatışınızda kaybolacaktır.
```cmd
mountvol y: /d
```

## Windows'a boot edin

### Rootlu boot imajının bir yedeğini alın

```cmd
adb shell "dd if=/dev/block/platform/soc/1d84000.ufshc/by-name/boot$(getprop ro.boot.slot_suffix) of=/tmp/rooted_boot.img" && adb pull /tmp/rooted_boot.img
```

### Bootloader'a boot edin

```cmd
adb reboot bootloader
```

### UEFI imajını indirin ve flashlayın
> [UEFI imajını](https://github.com/erdilS/Port-Windows-11-Xiaomi-Pad-5/releases/download/UEFI/uefi-v3.img) indirin 

```cmd
fastboot flash boot <imajın bulunduğu yol>
```

## Windows'a reboot edin
```cmd
fastboot reboot
```

> [!NOTE]
> İlk Windows açılışında, herhangi bir Wi-Fi ağı görmeyecektir. Yeniden başlayana dek güç düğmesine basılı tutarak tabletinizi yeniden başlatın. Yeniden başlatmadan sonra sorun çözülecektir. "Bağlanılamadı" şeklinde bir bildirim alırsanız, çalışana kadar yeniden dene düğmesine basın (genellikle 5 kez)

### Android'e geri boot edin
Windows kurulduktan sonra, Windows'ta yeniden başlat düğmesine basın (KAPATMA'ya basmayın), ardından yeniden başlatılırken fastboot'a geri dönmek için `sesi kısma` + `güç` tuşlarına basılı tutun
> Android'e dönmek için yedeklediğiniz boot imajını fastboot üzerinden geri yükleyin.

```cmd
fastboot flash boot rooted_boot.img
```

```cmd
fastboot reboot
```


### [Son Aşama: Dualboot (çift sistem) kurulumu](dualboot-tr.md)
