# hyprland-arch
# За основу взял Arch linux + KDE Plasma
****
## Установка hyprland и доп. утила к нему:
**Заранее написанный скрипт типом:**
```
bash <(curl -s https://raw.githubusercontent.com/mylinuxforwork/hyprland-starter/main/setup.sh)
```
****
## Если что-то не установилось и скрипт сам не может доставить пакеты:
****
**Pacman:**
```
sudo pacman -S hyprland waybar hyprpaper alacritty dolphin rofi-wayland thunar hyprlock qt5-wayland brightnessctl figlet
```
**AUR:**
```
yay -S hyprshot
```
**Flatpak:**
```
flatpak install flathub org.pulseaudio.pavucontrol app.zen_browser.zen
```
****
## Самый главный бинд который надо знать:
#### `Win+Enter` - терминал, остальные бинды лежат по пути:
```
~/.config/hypr/conf/binds.conf 
```
****
## Добавить русскую раскладку:
**Зайти в файл input.conf**
```
sudo nano ~/.config/hyrp/conf/input.conf
```
#### **В строку kb_layout добавить:**
- `us, ru`
#### **В строку kb_options добавить:**
- `grp:win_space_toggle` - для смены на win+ пробел
- `grp:alt_shift_toggle` - для смены на alt+shift
****
## Настроить частоту и разрешение мониторов:
**Узнать названия мониторов:**
```
hyprctl monitors
```
**Взять название монитора и частоты его работы:**
- `Monitor {MonitorName}`
#### Зайти в файл monitor.conf
```
sudo nano ~/.config/hyrp/conf/monitor.conf
 ```
 **Файл примерно будет выглядеть вот так:**
```
# See https://wiki.hyprland.org/Configuring/Monitors/
monitor=eDP-1,2560x1600@120,auto,1.25
```
**Что нужно указывать из hyprctl monitors:**
```
monitor={monitor_name},{resolution}@{refresh_rate},auto,{scaling}
```
**Если мониторов больше чем один:**
```
monitor={monitor_name},{resolution}@{refresh_rate},auto,{scaling}
monitor={monitor_name},{resolution}@{refresh_rate},auto,{scaling}
```
**Например у меня файл выглядит так:**
```
monitor=eDP-1,2560x1600@120,auto,1.25
monitor=HDMI-A-1,1920x1080@120,auto,1
```
****
## Если нужен bluetooth:
```
sudo systemctl start bluetooth && sudo systemctl enable bluetooth
```
```
sudo pacman -S blueman
```
**Открыть настройки bluetooth:**
```
blueman-manager
```
****
## Когда понадобилось настроить звук:
**Если кнопка звука на панели сверху не работает:**
- **Открываем файл по пути:**
```
sudo nano ~/.config/waybar/modules.json
```
- **Листаем файл до строки // Pulseaudio, дальше ищем строку on-click и меняем**
```
pavucontrol
```
**На**
```
org.pulseaudio.pavucontrol
```
- **И после всех манипуляций перезапустить waybar:**
```
killall waybar
waybar & disown
```
****
## Скриншоты:
Со скриншотами произошла проблема: в стоке никакие проги для скриншотов не работают, работает только hyprshot, но на него надо дописать бинды в binds.conf
- **Установить hyprshot:**
```
yay -S hyprshot
```
- **Зайти в файл:**
```
sudo nano ~/.config/hyrp/conf/binds.conf
```
- **В конец секции Actions добавить 2 бинда:**
```
bind = $mainMod SHIFT, S, exec, hyprshot -m output -m {MonitorName} --clipboard-only
bind = $mainMod CTRL SHIFT, S, exec, hyprshot -m window -m active --clipboard-only
```
#### Win+Shift+S  - весь экран
#### Win+Ctrl+Shift+S - активное окно
****
## SWAP файл:
https://losst.pro/fajl-podkachki-linux
