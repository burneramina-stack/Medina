# Быстрые команды

> Полезные команды для работы с проектом

---

## Создание файлов

### Новое историческое событие
```bash
cp research/history/_template.md research/history/YYYY-название-события.md
```

### Новое политическое событие
```bash
cp research/politics/_template.md research/politics/YYYY-название.md
```

### Новое свидетельство
```bash
cp research/testimonies/_template.md research/testimonies/YYYY-тип-номер.md
```

### Новая глава
```bash
cp manuscript/chapters/_template.md manuscript/chapters/chapter-XX.md
```

---

## Поиск

### Найти все файлы с определенным тегом
```bash
grep -r "#первая_война" research/
```

### Найти упоминание слова/имени
```bash
grep -r "Дудаев" .
```

### Найти все файлы, измененные сегодня
```bash
find . -name "*.md" -mtime 0
```

### Найти все незаполненные TODO в исследованиях
```bash
grep -r "\- \[ \]" research/
```

---

## Статистика

### Сколько файлов в каждой категории
```bash
echo "История: $(ls research/history/*.md 2>/dev/null | wc -l)"
echo "Политика: $(ls research/politics/*.md 2>/dev/null | wc -l)"
echo "Язык: $(ls research/language/*.md 2>/dev/null | wc -l)"
echo "География: $(ls research/geography/*.md 2>/dev/null | wc -l)"
echo "Культура: $(ls research/culture/*.md 2>/dev/null | wc -l)"
echo "Свидетельства: $(ls research/testimonies/*.md 2>/dev/null | wc -l)"
echo "Главы: $(ls manuscript/chapters/*.md 2>/dev/null | wc -l)"
```

### Общее количество слов в рукописи
```bash
wc -w manuscript/chapters/*.md
```

### Последние измененные файлы
```bash
ls -lt **/*.md | head -10
```

---

## Организация

### Создать backup всего проекта
```bash
tar -czf ../medina-backup-$(date +%Y%m%d).tar.gz .
```

### Список всех файлов со свидетельствами
```bash
ls -1 research/testimonies/*.md
```

### Список всех глав по порядку
```bash
ls -1 manuscript/chapters/chapter-*.md | sort
```

---

## Git команды

### Сохранить изменения
```bash
git add .
git commit -m "Добавлено: [краткое описание]"
git push
```

### Посмотреть что изменилось
```bash
git status
git diff
```

### История изменений файла
```bash
git log --follow research/history/название-файла.md
```

---

## Полезные алиасы

Добавьте в `~/.bashrc` или `~/.zshrc`:

```bash
# Быстрый переход в проект
alias medina='cd /home/user/Medina'

# Создать новое историческое событие
alias newhist='cp /home/user/Medina/research/history/_template.md'

# Создать новую главу
alias newchap='cp /home/user/Medina/manuscript/chapters/_template.md'

# Статистика проекта
alias medstats='cd /home/user/Medina && echo "История: $(ls research/history/*.md 2>/dev/null | wc -l)" && echo "Главы: $(ls manuscript/chapters/*.md 2>/dev/null | wc -l)"'
```

---

## Проверки качества

### Найти файлы без источников
```bash
for file in research/**/*.md; do
  if ! grep -q "## Источники" "$file"; then
    echo "Нет источников: $file"
  fi
done
```

### Найти файлы без тегов
```bash
for file in research/**/*.md; do
  if ! grep -q "## Теги" "$file" && ! grep -q "#" "$file"; then
    echo "Нет тегов: $file"
  fi
done
```

### Список файлов по дате создания
```bash
ls -lt research/**/*.md
```

---

## Экспорт (будущее)

### Объединить все главы в один файл
```bash
cat manuscript/chapters/chapter-*.md > manuscript/full-draft.md
```

### Создать список всех источников
```bash
grep -h "^[0-9]\." research/**/*.md | sort | uniq > sources-list.txt
```

---

_Используйте эти команды для ускорения работы!_
