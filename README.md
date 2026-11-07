# Slime — Godot-порт (из Slime.ccode7, CodeCube)

Аркада: слайм ездит за пальцем, сверху падают мусор (минус HP), кристаллы (+монеты), сердца (+HP). 3 режима, 9 скинов, настройки, промокод, локальный топ-7 + онлайн-таблица через Firebase.

## Как запустить
1. Godot 4.2+ (ставится с godotengine.org), Render — подойдёт GL Compatibility.
2. Project → Import → выбрать папку `SlimeGodot` (файл `project.godot`) → Open.
3. Нажать F5 (Run). Вертикальное окно 720×1280, управление — мышь/палец.

## Как собрать APK
1. Поставить Android Build Template + экспортные шаблоны (Project → Install Android Build Template, Editor → Manage Export Templates).
2. Project → Export → Android → добавить пресет, ориентация Portrait уже задана в `project.godot`.
3. Package name можно взять из оригинала: `com.popa.app52`.

## Управление
- Веди пальцем/мышью по экрану — слайм едет за ним (как `finger_touching_screen_x` в оригинале).
- В дуэли внизу 3 карты: Щит / Чист (убрать мусор) / +HP, у каждой кулдаун.

## Что портировано (по скриптам CodeCube)
| Оригинал | Godot |
|---|---|
| Script2 игрок (круг+скин+лицо+тень, вращение) | `scripts/player.gd` (SlimePlayer) |
| Script5 управление пальцем | `SoloGame._gui_input` (тач/мышь, клемп) |
| Script6 режим первый (3 мусора+монета+сердце, 3 HP, тряска slimeShake, вспышка) | `scripts/solo_game.gd` mode solo |
| Script20 онлайн 1 на 1 | mode pvp — тот же додж + враг-бот (матчмейкинг `/PvP` заменён ботом, см. ниже) |
| Script21 дуэль 1 на 1 | mode duel — 100 HP, щиты (`shield.png`), 3 карты 10/12/15с, бот лечится |
| Script10/12/15 выбор скина (9 шт, цены 25/75, ключи j..) | экран shop, Save `skins_owned/skin_selected` |
| Script13 настройки (RGB, громкость, 3 трека, 7 фонов, ТГК, донат) | экран settings, ключи `bg_r/bg_g/bg_b/volume/music_style/theme` |
| Script8 промокоды (код `67` → +250, ключ Prom) | поле промокода, `PROMO_CODES` в `main.gd` |
| Script16 об игре | экран about (тексты 1:1) |
| Script14 рекорд и счёт + Script18 лидеры | локальный топ-7 (Save) + Firebase `/GodotLider` |
| Script11 монеты (MON) | Save `MON`, алмаз в шапке |
| Script1/3/4/7 теги и навигация | `show(name)` экраны menu/modes/shop/settings/about/leaders/game |
| Script9 фон (7 тем) | `THEMES`, оверлейные фоны |
| Звуки/шрифт | `assets/sounds` (coin/hit/deny/pop/bgm1-3), `assets/fonts/barcode.ttf` |

## Firebase
База та же: `https://slime-ccode-default-rtdb.europe-west1.firebasedatabase.app`.
- `/Lider/<dev>` `{s}` — личный рекорд (совместимо с оригиналом).
- `/GodotLider/<dev>` `{s,n,w}` — таблица порта (сортировка по очкам, топ-7).
- `/hb/<dev>` `{t,n}` — heartbeat, счётчик онлайна (свежие <120с).
- Монеты/скины — только локально (в оригинале `/coins/<dev>`, сюда не тянем).
Без интернета всё работает офлайн, сеть только для лидеров/онлайна.

## Расхождения с оригиналом (честно)
- Мусор: в архиве все 4 спрайта — один и тот же ящик (заглушки автора), использованы как есть.
- PvP/дуэль играют против бота: серверный матчмейкинг CodeCube (`/PvP/wait|claim|...`, 27+32 КБ Lua) требует живого лобби-сервера; бот повторяет правила (движение, HP, подбор, карты), endpoints под реальный мультиплеер зарезервированы в `firebase.gd`.
- Шрифт-баркод оригинала (`IDAutomationHC39M`) лежит в `assets/fonts`, но русские тексты набраны системным шрифтом (баркод не имеет кириллицы).
- `magma` (Image45) отсутствует в архиве — темы без неё (6+классика).
