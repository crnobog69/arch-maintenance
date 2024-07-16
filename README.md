# 🐧 Водич за одржавање Арч Линукса / Arch Linux Maintenance Guide

Добродошли у Водич за одржавање Арч Линукса! Овај README пружа свеобухватан преглед основних задатака одржавања како би ваш Арч Линукс систем радио без проблема. 🚀

Welcome to the Arch Linux Maintenance Guide! This README provides a comprehensive overview of essential maintenance tasks to keep your Arch Linux system running smoothly. 🚀

## 📋 Садржај / Table of Contents

- [Провере здравља система / System Health Checks](#-провере-здравља-система--system-health-checks)
- [Ажурирања / Updates](#-ажурирања--updates)
- [Управљање пакетима / Package Management](#-управљање-пакетима--package-management)
- [Чишћење / Cleaning](#-чишћење--cleaning)
- [Управљање дневницима / Log Management](#-управљање-дневницима--log-management)
- [Оптимизација листе огледала / Mirror List Optimization](#-оптимизација-листе-огледала--mirror-list-optimization)
- [Додатни ресурси / Additional Resources](#-додатни-ресурси--additional-resources)

## 🩺 Провере здравља система / System Health Checks

1. **Провера неуспелих systemd сервиса / Check for failed systemd services:**
   ```
   systemctl --failed
   ```

2. **Преглед дневника / Review logs:**
   ```
   sudo journalctl -p 3 -xb
   ```

## 🔄 Ажурирања / Updates

Одржавајте систем ажурним покретањем / Keep your system up-to-date by running:

```
sudo pacman -Syu
```

За AUR пакете (ако користите yay) / For AUR packages (if using yay):

```
yay -Syu
```

На EndeavourOS може се користити само (и за ажурирање система) / On EndeavourOS, you can simply use (for system updates as well):

```
yay
```

## 📦 Управљање пакетима / Package Management

1. **Чишћење pacman кеша (пакети који нису инсталирани али се налазе у pacman / некоришћени) / Clean pacman cache (packages not installed but present in pacman / unused):**
   ```
   sudo pacman -Sc
   ```

2. **Чишћење pacman и yay кеша (сви пакети *ОПАСНО / може дођи до проблема са системом*) / Clean pacman and yay cache (all packages *DANGEROUS / may cause system issues*):**
   ```
   sudo pacman -Scc
   yay -Scc
   ```

3. **Чишћење AUR кеша (пакети који нису инсталирани / некоришћени) / Clean AUR cache (packages not installed / unused):**
   ```
   yay -Sc
   ```

4. **Уклањање нежељених зависности (orphaned packages) / Remove unwanted dependencies (orphaned packages):**
   ```
   yay -Yc
   ```

5. **Провера сирочади пакета / Check for orphaned packages:**
   ```
   pacman -Qtdq
   ```

6. **Уклањање сирочади пакета (*BASH*) / Remove orphaned packages (*BASH*):**
   ```
   sudo pacman -Rns $(pacman -Qtdq)
   ```

## 🧹 Чишћење / Cleaning

1. **Чишћење корисничког кеша / Clean user cache:**
   ```
   rm -rf ~/.cache/*
   ```

2. **Провера величине .config директоријума / Check the size of .config directory:**
   ```
   du -sh ~/.config
   ```

## 📜 Управљање дневницима / Log Management

1. **Провера величине дневника / Check log size:**
   ```
   du -sh /var/log/journal
   ```

2. **Чишћење дневника (задржавање последње две недеље) / Clean logs (keep last two weeks):**
   ```
   sudo journalctl --vacuum-time=2weeks
   ```

или / or

```
   sudo journalctl --vacuum-time=1week
```

или / or

```
   sudo journalctl --vacuum-time=3days
```

или / or

```
   sudo journalctl --vacuum-time=1day
```

## 🌐 Оптимизација листе огледала / Mirror List Optimization

Ажурирање листе огледала помоћу reflector-а (у случају коришђења EndeavourOS-а он долази са GUI за reflector) / Update mirror list using reflector (in case of using EndeavourOS, it comes with a GUI for reflector):

```
sudo reflector -c Worldwide -a 6 --sort rate --save /etc/pacman.d/mirrorlist
```

или / or

```
sudo reflector -c [your_country] -a 6 --sort rate --save /etc/pacman.d/mirrorlist
```

Замените `[your_country]` именом ваше земље. Користите наводнике за земље са више речи, нпр. 'United States'.

Replace `[your_country]` with the name of your country. Use quotes for multi-word countries, e.g., 'United States'.

## 📚 Додатни ресурси / Additional Resources

- [Арч Линукс Вики: Одржавање система / Arch Linux Wiki: System maintenance](https://wiki.archlinux.org/title/System_maintenance)
- [Арч Линукс Вики: Pacman савети и трикови / Arch Linux Wiki: Pacman tips and tricks](https://wiki.archlinux.org/title/Pacman/Tips_and_tricks)

Не заборавите да прилагодите рутину одржавања према вашим специфичним потребама и конфигурацији система. Редовно одржавање ће помоћи да осигурате стабилан и ефикасан Арч Линукс систем!

Remember to adjust your maintenance routine according to your specific needs and system configuration. Regular maintenance will help ensure a stable and efficient Arch Linux system!
