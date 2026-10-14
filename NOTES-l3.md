## Варіант

журнал 35, варіант 5, прізвище Chaban

## 1. stash list

```
stash@{0}: On lab3/variant-5-chaban: чернетка ліцензії v5
```

Я сховав зміни та новий файл draft-v5.txt через `-u`, а `-m` задав зрозумілу назву запису. Після `stash pop` запис зник зі списку, а файли повернулися.

## 2. cherry-pick

```
32a830d  Уточнити ліцензію   (feature/pick-5)
1f8effc  Уточнити ліцензію   (lab3/variant-5-chaban)
```

Хеші різні, бо cherry-pick робить копію патча як новий коміт з іншим батьківським комітом і часом створення. Зміст (рядок у LICENSE.md) той самий.

## 3. reflog

```
28d1f7d HEAD@{0}: commit (amend): Зафіксувати ліцензію, варіант 5
1f8effc HEAD@{1}: cherry-pick: Уточнити ліцензію
```

Amend замінив останній локальний коміт новим, а старий хеш лишився в reflog. Коміт ще не був запушений, тому amend безпечний.

## 4. revert

```
717ff99 Revert "Зіпсувати рядок"
de4394f Зіпсувати рядок
28d1f7d Зафіксувати ліцензію, варіант 5
eb03ee8 Add draft-v5
388e8a9 Add LICENSE.md
e94f4df Initial commit
```

Поганий коміт вже був на origin, тому я скасував його через `git revert`, а не reset. Історія зберігається, а поганого рядка на кінчику гілки вже немає.

## 5. тег

```
tag v0.1-chaban
Tagger: flawedlikeu <volodymyrchabann@gmail.com>
Date:   Wed Oct 14 10:02:29 2026 +0300

Перший зріз варіанта 5
```

Тег annotated (`git cat-file -t` показує `tag`), створений з `-a` і запушений на origin. Через detached HEAD я вийшов гілкою recover/v5.

## 6. rebase -i

```
pick d6c5d11 # WIP: чернетка
squash a3e0e7b # fix typo
```

Підсумкове повідомлення: `Уточнити ліцензію` (коміт 6c35803). Дві чернеткові правки злилися в один коміт, після цього я запушив тільки через `--force-with-lease` у свою гілку.

## 7. blame

```
28d1f7da (flawedlikeu 2026-10-14 09:44:04 +0300 3) Ліцензія: MIT-NC навчальна (lab3-v5)
```

## 8. fork

origin — це мій форк, upstream — оригінальний репозиторій. Спершу роблю `git fetch upstream`, щоб отримати свіжі зміни оригіналу. Свої зміни пушу в origin. Pull request відкриваю з моєї гілки в `upstream/main`.
