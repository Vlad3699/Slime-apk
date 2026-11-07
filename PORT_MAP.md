# Карта портирования Slime.ccode7 → Godot

Полный разбор оригинала: `src/SPEC.md` (в генераторе).

```
Slime.ccode7 (ZIP, portrait)
├── game.json → project.godot [application], THEMES/MUSIC в main.gd
├── Images/* → assets/sprites/ (переименованы 1:1, см. ниже)
├── Sounds/* → assets/sounds/coin.wav hit.wav deny.wav pop.mp3 bgm1-3.mp3
├── Fonts/Font1 → assets/fonts/barcode.ttf (только цифры)
├── Scripts/Script1 теги → show("menu/modes/shop/settings/about/leaders/game")
├── Scripts/Script2 игрок → player.gd
├── Scripts/Script3 добавление в теги → порядок add_child в main.gd
├── Scripts/Script4 выбор режима → _build_modes
├── Scripts/Script5 управление → solo_game._gui_input
├── Scripts/Script6 режим первый → solo_game mode solo
├── Scripts/Script7 назад → кнопки НАЗАД/выход
├── Scripts/Script8 промокоды (67→+250) → _apply_promo
├── Scripts/Script9 фон (7 тем) → THEMES + theme_tex
├── Scripts/Script10/12/15 скины → _build_shop/refresh_shop
├── Scripts/Script11 монеты (MON) → save_system MON
├── Scripts/Script13 настройки → _build_settings
├── Scripts/Script14 рекорд/счёт → REC + score_acc + insert_local_top
├── Scripts/Script16 об игре → _build_about (тексты 1:1)
├── Scripts/Script17 сеть для ИИ → пропущен (пустые HTTP-блоки)
├── Scripts/Script18 лидеры → leaders + firebase.gd
├── Scripts/Script19 блоки для ИИ → пропущен (песочница)
├── Scripts/Script20 онлайн → solo_game mode pvp (бот)
├── Scripts/Script21 дуэль → solo_game mode duel (100HP/щиты/карты/бот)
└── Scripts/Script22 ещё для ИИ → пропущен (песочница)
```

Спрайты: button_play/button_about/button_settings/button_skins/mode_solo/mode_duo/duel_vs/game_over/
bg_base/gradient/night/sunset/neon/cosmos/bubbles/heart/diamond/shadow/shield/face/
skin1..9/trash1..4/arrow_left/arrow_right/sarrow_left/sarrow_right/tg/board_brown/
price/locked/aside/leaders/finish/crown/icon1..8/all_at_once + icon.png.
