# 🐧 Водич за одржавање Арч Линукса

Добродошли у Водич за одржавање Арч Линукса! Овај README пружа свеобухватан преглед основних задатака одржавања како би ваш Арч Линукс систем радио без проблема. 🚀

## 📋 Садржај

- [Провере здравља система](#-провере-здравља-система)
- [Ажурирања](#-ажурирања)
- [Управљање пакетима](#-управљање-пакетима)
- [Чишћење](#-чишћење)
- [Управљање дневницима](#-управљање-дневницима)
- [Оптимизација листе огледала](#-оптимизација-листе-огледала)
- [Додатни ресурси](#-додатни-ресурси)

## 🩺 Провере здравља система

1. **Провера неуспелих systemd сервиса:**
   ```
   systemctl --failed
   ```

2. **Преглед дневника:**
   ```
   sudo journalctl -p 3 -xb
   ```

## 🔄 Ажурирања

Одржавајте систем ажурним покретањем:

```
sudo pacman -Syu
```

За AUR пакете (ако користите yay):

```
yay -Syu
```

На EndeavourOS може се користити само (и за ажурирање система):

```
yay
```

## 📦 Управљање пакетима

1. **Чишћење pacman кеша (пакети који нису инсталирани али се налазе у pacman / некоришћени):**
   ```
   sudo pacman -Sc
   ```

2. **Чишћење pacman и yay кеша (сви пакети *ОПАСНО / може дођи до проблема са системом*):**
   ```
   sudo pacman -Scc
   yay -Scc
   ```

3. **Чишћење AUR кеша (пакети који нису инсталирани / некоришћени):**
   ```
   yay -Sc
   ```

4. **Уклањање нежељених зависности (*orphaned packages*):**
   ```
   yay -Yc
   ```

5. **Провера сирочади пакета:**
   ```
   pacman -Qtdq
   ```

6. **Уклањање сирочади пакета (*BASH*):**
   ```
   sudo pacman -Rns $(pacman -Qtdq)
   ```

## 🧹 Чишћење

1. **Чишћење корисничког кеша:**
   ```
   rm -rf ~/.cache/*
   ```

2. **Провера величине .config директоријума:**
   ```
   du -sh ~/.config
   ```

## 📜 Управљање дневницима

1. **Провера величине дневника:**
   ```
   du -sh //var/log/journal
   ```

2. **Чишћење дневника (задржавање последње две недеље):**
   ```
   sudo journalctl --vacuum-time=2weeks
   ```

или

```
   sudo journalctl --vacuum-time=1week
```

или

```
   sudo journalctl --vacuum-time=3days
```

или

```
   sudo journalctl --vacuum-time=1day
```

## 🌐 Оптимизација листе огледала

Ажурирање листе огледала помоћу reflector-а (у случају коришђења EndeavourOS-а он долази са GUI за reflector):

```
sudo reflector -c Worldwide -a 6 --sort rate --save /etc/pacman.d/mirrorlist
```

или за одређену државу

```
sudo reflector -c [ваша_земља] -a 6 --sort rate --save /etc/pacman.d/mirrorlist
```

Замените `[ваша_земља]` именом ваше земље. Користите наводнике за земље са више речи, нпр. 'Сједињене Државе' => 'United States'.

## 📚 Додатни ресурси

- [Арч Линукс Вики: Одржавање система](https://wiki.archlinux.org/title/System_maintenance)
- [Арч Линукс Вики: Pacman савети и трикови](https://wiki.archlinux.org/title/Pacman/Tips_and_tricks)

Не заборавите да прилагодите рутину одржавања према вашим специфичним потребама и конфигурацији система. Редовно одржавање ће помоћи да осигурате стабилан и ефикасан Арч Линукс систем!
