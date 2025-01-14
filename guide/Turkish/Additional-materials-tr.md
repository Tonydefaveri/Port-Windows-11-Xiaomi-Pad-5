<img align="right" src="https://raw.githubusercontent.com/erdilS/Port-Windows-11-Xiaomi-Pad-5/main/nabu.png" width="425" alt="Windows 11 Running On A Xiaomi Pad 5">

# Xiaomi Pad 5'te Windows için faydalı uygulamalar ve talimatlar

## Hide D drive (modem partition)
> [!NOTE]
> This is recommended because this drive should not be modified, while some applications may try to write to it

- Open a command prompt window and run ```diskpart```
- Run ```list volume``` to see all available volumes
- Select the disk that has letter D with ```select volume $```, replacing "$" with the volume number
- Remove the letter with ```remove letter d```
- Exit diskpart with ```exit```

#### Finished!


## USB Host modunu devre dışı bırakma
> [!Warning]
> Ek güç verilmemiş USB aygıtlar çalışmayı durduracaktır.

Run [USB Host Control](https://github.com/erdilS/Port-Windows-11-Xiaomi-Pad-5/releases/download/USBHost/USB.Host.Mode.Control.V4.0.vbs) to enable/disable USB host mode, confirm that you want to disable/enable USB host mode and then confirm the reboot


## Secureboot'u devre dışı bırakma
> Sürücüleri bilgisayar olmadan güncelleyebilmek için secureboot kapatılmalıdır.

[Secureboot'u devre dışı bırakma rehberi](/guide/Turkish/disable-secureboot-tr.md)

## ```Microsoft Office``` / ```Microsoft 365``` kurulumu

- Bu [ISO dosyasını](https://mega.nz/file/hjAiSL4T#G7kOKpsUFpyL2UW9RQmY2e96urcQW5xZKdc7ciaNOy8) tablete indirin
- iso dosyasına sağ tıklayın ve windows gezgininde (explorer) açmak için bağlayın (mount edin)
- Kurulum sihirbazını başlatmak için ```Office Tool Plus.exe``` dosyasını çift tıklayın
- Açılan pencerede `Evet (Yes)`i seçin
- Kurulumun bitmesini bekleyin

 ### Windows / Office aktivasyonunu yapma

Massgravel talimatlarını [buradan](https://github.com/massgravel/Microsoft-Activation-Scripts) takip edin

 ## El feneri (flashlight) nasıl kullanılır

- [Flashlight.7z](https://github.com/erdilS/Port-Windows-11-Xiaomi-Pad-5/releases/download/1.0/flashlight_fix.7z) arşiv dosyasını indirin ve herhangi bir klasöre çıkartın

> El fenerini açmak için flashlight.exe'yi çalıştın

> Kapatmak için ise herhangi bir tuşa basın
