# 🐧 Arch Linux Maintenance Guide / Водич за одржавање Арч Линукса

Welcome to the Arch Linux Maintenance Guide! This README provides a comprehensive overview of essential maintenance tasks to keep your Arch Linux system running smoothly. 🚀

Добродошли у Водич за одржавање Арч Линукса! Овај README пружа свеобухватан преглед основних задатака одржавања како би ваш Арч Линукс систем радио без проблема. 🚀

## 📋 Table of Contents / Садржај

- [System Health Checks / Провере здравља система](#-system-health-checks--провере-здравља-система)
- [Updates / Ажурирања](#-updates--ажурирања)
- [Package Management / Управљање пакетима](#-package-management--управљање-пакетима)
- [Cleaning / Чишћење](#-cleaning--чишћење)
- [Log Management / Управљање дневницима](#-log-management--управљање-дневницима)
- [Mirror List Optimization / Оптимизација листе огледала](#-mirror-list-optimization--оптимизација-листе-огледала)
- [Additional Resources / Додатни ресурси](#-additional-resources--додатни-ресурси)

## 🩺 System Health Checks / Провере здравља система

1. **Check for failed systemd services / Провера неуспелих systemd сервиса:**
   ```
   systemctl --failed
   ```

2. **Review logs / Преглед дневника:**
   ```
   sudo journalctl -p 3 -xb
   ```

## 🔄 Updates / Ажурирања

Keep your system up-to-date by running / Одржавајте систем ажурним покретањем:

```
sudo pacman -Syu
```

For AUR packages (if using yay) / За AUR пакете (ако користите yay):

```
yay -Syu
```

On EndeavourOS, you can simply use (for system updates as well) / На EndeavourOS може се користити само (и за ажурирање система):

```
yay
```

## 📦 Package Management / Управљање пакетима

1. **Clean pacman cache (packages not installed but present in pacman / unused) / Чишћење pacman кеша (пакети који нису инсталирани али се налазе у pacman / некоришћени):**
   ```
   sudo pacman -Sc
   ```

2. **Clean pacman and yay cache (all packages *DANGEROUS / may cause system issues*) / Чишћење pacman и yay кеша (сви пакети *ОПАСНО / може дођи до проблема са системом*):**
   ```
   sudo pacman -Scc
   yay -Scc
   ```

3. **Clean AUR cache (packages not installed / unused) / Чишћење AUR кеша (пакети који нису инсталирани / некоришћени):**
   ```
   yay -Sc
   ```

4. **Remove unwanted dependencies (orphaned packages) / Уклањање нежељених зависности (orphaned packages):**
   ```
   yay -Yc
   ```

5. **Check for orphaned packages / Провера сирочади пакета:**
   ```
   pacman -Qtdq
   ```

6. **Remove orphaned packages (*BASH*) / Уклањање сирочади пакета (*BASH*):**
   ```
   sudo pacman -Rns $(pacman -Qtdq)
   ```

## 🧹 Cleaning / Чишћење

1. **Clean user cache / Чишћење корисничког кеша:**
   ```
   rm -rf ~/.cache/*
   ```

2. **Check the size of .config directory / Провера величине .config директоријума:**
   ```
   du -sh ~/.config
   ```

## 📜 Log Management / Управљање дневницима

1. **Check log size / Провера величине дневника:**
   ```
   du -sh /var/log/journal
   ```

2. **Clean logs (keep last two weeks) / Чишћење дневника (задржавање последње две недеље):**
   ```
   sudo journalctl --vacuum-time=2weeks
   ```

or / или

```
   sudo journalctl --vacuum-time=1week
```

or / или

```
   sudo journalctl --vacuum-time=3days
```

or / или

```
   sudo journalctl --vacuum-time=1day
```

## 🌐 Mirror List Optimization / Оптимизација листе огледала

Update mirror list using reflector (in case of using EndeavourOS, it comes with a GUI for reflector) / Ажурирање листе огледала помоћу reflector-а (у случају коришђења EndeavourOS-а он долази са GUI за reflector):

```
sudo reflector -c Worldwide -a 6 --sort rate --save /etc/pacman.d/mirrorlist
```

```
sudo reflector -c [your_country] -a 6 --sort rate --save /etc/pacman.d/mirrorlist
```

Replace `[your_country]` with the name of your country. Use quotes for multi-word countries, e.g., 'United States'.

Замените `[your_country]` именом ваше земље. Користите наводнике за земље са више речи, нпр. 'United States'.

## 📚 Additional Resources / Додатни ресурси

- [Arch Linux Wiki: System maintenance / Арч Линукс Вики: Одржавање система](https://wiki.archlinux.org/title/System_maintenance)
- [Arch Linux Wiki: Pacman tips and tricks / Арч Линукс Вики: Pacman савети и трикови](https://wiki.archlinux.org/title/Pacman/Tips_and_tricks)

Remember to adjust your maintenance routine according to your specific needs and system configuration. Regular maintenance will help ensure a stable and efficient Arch Linux system!

Не заборавите да прилагодите рутину одржавања према вашим специфичним потребама и конфигурацији система. Редовно одржавање ће помоћи да осигурате стабилан и ефикасан Арч Линукс систем!
