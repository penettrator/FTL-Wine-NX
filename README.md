# FTL: Faster Than Light (Advanced Edition) на Nintendo Switch через Wine-NX

Здесь только файлы, которые нужны, чтобы PC-версия FTL (GOG, 1.6.13) запускалась
на Switch через Wine-NX. Самой игры здесь нет — нужна своя копия.

[English below](#english)

## Что нужно

- Установленный Wine-NX (проверено на Test Build 4).
- FTL: Advanced Edition, GOG-версия, установленная на ПК.

## Установка

1. Скопируйте папку с установленной игрой (где лежит `FTLGame.exe`) на карту как
   `switch/wine/drive_c/ftl/`.
2. Скопируйте папку `switch` из этой папки в корень карты **с заменой** файлов.
3. Откройте лаунчер Wine-NX. Игра появится в библиотеке (`C:\ftl\FTLGame.exe`).
   Если нет: **+** → «Add game» → этот путь.
4. Запустите игру. Лаунчер предложит 32-битный ярлык («32-bit forwarder
   needed» → «Install now»), либо: **X** → Settings → «Make a 32-bit forwarder».
   Без него игра висит на чёрном экране.
5. Первый запуск долгий: чёрный экран и долгая загрузка — это нормально, подождите.

## Управление

FTL не поддерживает геймпад, поэтому кнопки Switch работают как мышь и клавиатура.
Сенсорный экран тоже работает: нажимает туда, куда коснулись.

| Кнопка    | Действие                                          |
|-----------|---------------------------------------------------|
| оба стика | курсор мыши                                       |
| A         | левая кнопка мыши: выбор, огонь, приказы экипажу  |
| B         | правая кнопка мыши: отмена, снять выделение       |
| X         | пробел: пауза / продолжить                        |
| Y         | Enter: подтвердить                                |
| +         | Esc: меню                                         |
| −         | V: автоогонь                                      |
| L / R     | 1 / 2: оружие 1 / 2                               |
| ZL / ZR   | 3 / 4: оружие 3 / 4                               |
| ↑         | J: карта и прыжок                                 |
| ↓         | U: корабль и улучшения                            |
| ←         | F1: первый член экипажа                           |
| →         | Q: весь экипаж                                    |

Раскладку можно поменять в файле `switch/wine/drive_c/ftl/FTLGame.keys.txt` или в
лаунчере (настройки игры → Edit controls). Другие клавиши — экранная клавиатура
Wine-NX (минус + нажатие правого стика).

> [!IMPORTANT]
> Выходите из игры через её меню (Esc → выход): FTL сохраняет прогресс и настройки
> только при выходе. Если закрыть её кнопкой HOME, несохранённое пропадёт.

## Что за файлы

Всё лежит в `switch/wine/drive_c/ftl/`, рядом с `FTLGame.exe`:

| Файл | Назначение |
|------|------------|
| `FTLGame.wine-nx.txt` | Название в лаунчере и запуск через 32-битный ярлык (`address-space=32-bit`). В обычном режиме игра висит на чёрном экране. |
| `FTLGame.keys.txt` | Раскладка кнопок (см. [«Управление»](#управление)). |
| `galaxy_wrapper.dll` | Замена обёртки GOG Galaxy. Оригинальная ищет клиент GOG Galaxy, которого на Switch нет. Эта отвечает игре «магазин не подключён», достижения ничего не делают. |
| `bass.dll`, `bassmix.dll` | Звуковая библиотека игры, распакованная заранее. Оригиналы сжаты упаковщиком petite, и под Wine-NX их распаковка ломается: игра закрывается при запуске. Версии те же (BASS 2.4.8, BASSmix 2.4.6). В `bass.dll` изменён 1 байт (смещение 0x205E5, 74 → EB): служебный поток, который запускает звуки, под Wine-NX завершался после первого звука, и на уровне звука не было. |
| `xinput1_4.dll`, `xinput1_3.dll` | Заглушки, на любой запрос отвечают «контроллер не подключён». FTL опрашивает XInput, а пока игра это делает, Wine-NX не превращает кнопки в мышь и клавиши — работал бы только сенсор. |

И отдельно:

`switch/wine/drive_c/users/steamuser/AppData/Roaming/FasterThanLight/settings.ini` —
настройки игры: русский язык и стандартные клавиши. Без него игра при первом
запуске спрашивает язык. Если нужен другой язык — не копируйте этот файл.

> [!TIP]
> Сохраните оригинальные `galaxy_wrapper.dll`, `bass.dll` и `bassmix.dll`, если
> захотите вернуть игру как было.

---

## English

Only the files that let the PC version of FTL: Advanced Edition (GOG, 1.6.13) run on
Switch through Wine-NX. The game itself is not included.

**Needs:** Wine-NX already installed (tested on Test Build 4) and the GOG version of
the game installed on a PC.

### Install

1. Copy the installed game folder (with `FTLGame.exe`) to `switch/wine/drive_c/ftl/`.
2. Copy this folder's `switch` folder to the card root, **replacing** files.
3. Start the game from the Wine-NX launcher (`C:\ftl\FTLGame.exe`) and install the
   32-bit forwarder when asked (or **X** → Settings → "Make a 32-bit forwarder").
4. Starting takes long: a black screen and long loading are normal.

### Controls

FTL has no gamepad support; the buttons act as mouse and keyboard, the
touchscreen clicks where touched.

| Button            | Action                       |
|-------------------|------------------------------|
| both sticks       | cursor                       |
| A / B             | left / right mouse button    |
| X                 | Space (pause)                |
| Y                 | Enter                        |
| +                 | Esc                          |
| −                 | V (autofire)                 |
| L / R / ZL / ZR   | weapons 1–4                  |
| D-pad ↑           | J (map, jump)                |
| D-pad ↓           | U (ship)                     |
| D-pad ←           | F1 (crew 1)                  |
| D-pad →           | Q (all crew)                 |

Change them in `FTLGame.keys.txt` or the launcher's Edit controls.

> [!IMPORTANT]
> Quit through the game's menu: FTL saves progress and settings only on exit.

### Files

In `switch/wine/drive_c/ftl/` next to `FTLGame.exe`:

- `FTLGame.wine-nx.txt` — launcher title and the 32-bit forwarder.
- `FTLGame.keys.txt` — the button layout above.
- `galaxy_wrapper.dll` — replaces the GOG Galaxy wrapper, which looks for a Galaxy
  client the Switch does not have.
- `bass.dll`, `bassmix.dll` — the game's own sound library versions, unpacked in
  advance; the originals are petite-packed and their unpacking breaks under Wine-NX.
  One byte of `bass.dll` is patched (offset 0x205E5, 74 → EB): the thread that starts
  every sound quit after the first one under Wine-NX, leaving levels silent.
- `xinput1_4.dll`, `xinput1_3.dll` — stubs that report "no controller"; while FTL
  polls XInput, Wine-NX would not turn the buttons into mouse and keys.
- `users/steamuser/AppData/Roaming/FasterThanLight/settings.ini` — Russian language
  and the default keys; skip it to pick the language yourself.

Keep the original `galaxy_wrapper.dll`, `bass.dll` and `bassmix.dll` to undo.
