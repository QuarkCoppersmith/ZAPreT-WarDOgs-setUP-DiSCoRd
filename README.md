# QuarkCoppersmith/ZAPreT-WarDOgs-setUP-DiSCoRd

Форк [QuarkCoppersmith/ZAPreT-WarDOgs-setUP-DiSCoRd](https://github.com/QuarkCoppersmith/ZAPreT-WarDOgs-setUP-DiSCoRd), заранее настроенный так, чтобы работали **War Dogs** и **Discord** одновременно.

Главное отличие от оригинала — файл **`AUTO-PICK-ZAPRET.bat`**: он сам перебирает стратегии и останавливается на той, что работает сегодня. Руками по одной запускать больше не нужно.

## Как пользоваться

1. Скачать репозиторий: зелёная кнопка **Code → Download ZIP**
2. ПКМ по архиву → **Свойства** → галочка **«Разблокировать»** → ОК
3. Распаковать в путь **без кириллицы и пробелов** — например `C:\zapret`
4. ПКМ по **`AUTO-PICK-ZAPRET.bat`** → **«Запуск от имени администратора»**

Скрипт перебирает стратегии и на каждой проверяет три адреса Discord — сайт, gateway и CDN. Останавливается на первой, где отвечают все три, и оставляет её работать. Занимает от нескольких секунд до пары минут.

Доступность античита War Dogs проверяется отдельно и **на выбор стратегии не влияет** — почему, см. ниже.

Первой всегда пробуется `general (ALT11)` — она подтверждённо работает с War Dogs.

Результат последнего запуска пишется в `auto-pick-last-run.txt`.

## Что уже настроено

| Настройка | Значение | Зачем |
|---|---|---|
| Game Filter | `enabled (UDP)` | War Dogs использует UDP на портах выше 1023 |
| IPSet Filter | `any` | под фильтр попадает любой IP игры |
| `lists/list-general.txt` | 105 строк | штатные домены + Cloudflare + `codefusion.technology` (античит) |
| `lists/list-exclude.txt` | 129 строк | штатные исключения + Яндекс, Teams и прочее |

Списки — **надстройка** над оригинальными: все домены Discord и YouTube из штатной сборки на месте, ничего не удалено. Поэтому Discord не ломается.

### Почему античит не влияет на выбор стратегии

Все 8 доменов античита (`ac-*.codefusion.technology`) присутствуют **одновременно** в `list-general.txt` и в `list-exclude.txt`. В winws исключения имеют приоритет над списком обхода, поэтому zapret пропускает этот трафик нетронутым — при любой стратегии.

Скорее всего так и задумано: вмешиваться в трафик античита — плохая идея. Но следствие важно понимать: **по доступности античита нельзя отличить одну стратегию от другой**, результат будет одинаковым хоть с обходом, хоть без него. Поэтому `AUTO-PICK` выбирает стратегию по Discord, а античит показывает справочно — если он не отвечает, менять стратегию бессмысленно, проблема в сети.

Если захотите, чтобы античит всё же обходился, удалите строки `codefusion` из `lists/list-exclude.txt`. Конфиг из Discord-гайда я оставил как есть, потому что он у вас рабочий.

## Если не работает

- **Ни одна стратегия не прошла** — скрипт напишет, какая была лучшей, и запустит её. Часто этого достаточно.
- **`winws.exe` не стартует** — почти всегда антивирус забрал `WinDivert`. Добавьте папку в исключения или отключите детект PUA.
- **Нет прав администратора** — без них WinDivert не загрузится, обход не заработает в принципе.
- **Голосовой чат Discord висит на «подключении»** — нужны записи в `hosts`: запустите `service.bat` → пункт **9. Update Hosts File**. На машине, где диск откатывается после сессии, это придётся делать каждый раз.
- **Тормозят посторонние сайты** — это цена режима `IPSet any`. Вернуть: `service.bat` → **5. IPSet Filter**. Полный список лежит в `lists/ipset-all.txt.backup`.

## Ручной режим

Автоподбор ничего не ломает в оригинальной сборке — все штатные файлы на месте. Если хочется по-ста郸ту, просто запускайте `general (ALT11).bat` или любой другой напрямую, как раньше.

## Откуда взялся конфиг

Связку «ALT11 + Game Filter UDP + IPSet any + подменённые списки» подсказали на официальном Discord-сервере War Dogs. Стратегии со временем перестают работать и зависят от провайдера — поэтому и нужен автоподбор.

## Лицензия и происхождение

Оригинальный README сохранён рядом — [README-UPSTREAM.md](README-UPSTREAM.md), там полная документация по всем стратегиям и настройкам.

Оригинальный проект — [QuarkCoppersmith/ZAPreT-WarDOgs-setUP-DiSCoRd](https://github.com/QuarkCoppersmith/ZAPreT-WarDOgs-setUP-DiSCoRd), лицензия MIT. Бинарники в `bin/` взяты из [bol-van/zapret-win-bundle](https://github.com/bol-van/zapret-win-bundle) — их можно сверить по контрольным суммам с оригиналом.

Отдельная благодарность [bol-van](https://github.com/bol-van) — автору [zapret](https://github.com/bol-van/zapret).

---

<details>
<summary>NEW</summary>

### 🚀 Автоподбор стратегий

Теперь не нужно вручную запускать bat-файлы. **`AUTO-PICK-ZAPRET.bat`** сам найдёт рабочую стратегию для Discord и War Dogs.

### 🛡️ War Dogs + Discord

Специальные настройки для одновременной работы игры и голосового чата.

### 🔄 Актуальные списки

Все необходимые домены и исключения для стабильной работы.

</details>

---

<div align="center">
  <img src="https://img.shields.io/github/v/tag/QuarkCoppersmith/ZAPreT-WarDOgs-setUP-DiSCoRd?label=version&color=blue" alt="Version">
  <a href="https://github.com/QuarkCoppersmith/ZAPreT-WarDOgs-setUP-DiSCoRd/releases/tag/1.10.3">
    <img src="https://img.shields.io/github/downloads/QuarkCoppersmith/ZAPreT-WarDOgs-setUP-DiSCoRd/total?color=orange" alt="Downloads">
  </a>
  <a href="https://github.com/QuarkCoppersmith/ZAPreT-WarDOgs-setUP-DiSCoRd/releases/latest">
    <img src="https://img.shields.io/github/release-date/QuarkCoppersmith/ZAPreT-WarDOgs-setUP-DiSCoRd?color=green" alt="Last Release">
  </a>
</div>

---

### ФЕЙКИ

<details>
<summary><code>general (FAKE TLS AUTO ALT3).bat</code></summary>

Использует TLS-ClientHello для обхода блокировок.

</details>
<details>
<summary><code>general (SIMPLE FAKE ALT2).bat</code></summary>

Простая стратегия обхода с использованием подменённых данных.

</details>
<details>
<summary><code>general (FAKE TLS AUTO).bat</code></summary>

Автоматический выбор стратегии на основе TLS-ClientHello.

</details>
<details>
<summary><code>general (SIMPLE FAKE ALT).bat</code></summary>

Альтернативная простая стратегия обхода.

</details>
<details>
<summary><code>general (SIMPLE FAKE).bat</code></summary>

Базовая стратегия обхода.

</details>
<details>
<summary><code>general (FAKE TLS AUTO ALT2).bat</code></summary>

Ещё одна автоматическая стратегия на основе TLS-ClientHello.

</details>

---

### АНТИВИРУСЫ

<p>
  <img src="https://img.shields.io/github/license/QuarkCoppersmith/ZAPreT-WarDOgs-setUP-DiSCoRd?color=red" alt="License">
  <a href="https://github.com/QuarkCoppersmith/ZAPreT-WarDOgs-setUP-DiSCoRd/issues">
    <img src="https://img.shields.io/github/issues/QuarkCoppersmith/ZAPreT-WarDOgs-setUP-DiSCoRd?color=red" alt="Issues">
  </a>
  <a href="https://github.com/QuarkCoppersmith/ZAPreT-WarDOgs-setUP-DiSCoRd/contributors">
    <img src="https://img.shields.io/github/contributors/QuarkCoppersmith/ZAPreT-WarDOgs-setUP-DiSCoRd?color=yellow" alt="Contributors">
  </a>
</p>

**Важно:** Антивирусные программы могут ошибочно детектировать `WinDivert.dll` и `WinDivert64.sys` как вредоносные. Это ложное срабатывание. Для корректной работы программы добавьте папку с `zapret` в исключения антивируса или отключите детектирование PUA (Potentially Unwanted Application).

---

### Поддержка проекта

<p>
  Если у вас возникли проблемы или предложения, пожалуйста, создайте <a href="https://github.com/QuarkCoppersmith/ZAPreT-WarDOgs-setUP-DiSCoRd/issues">Issue</a> на GitHub.
</p>

---

<p align="center">
  © 2024 QuarkCoppersmith. Все права защищены.
</p>