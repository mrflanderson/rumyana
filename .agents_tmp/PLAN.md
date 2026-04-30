# План улучшений сайта РУМЯНА BAND

## 1. OBJECTIVE
Улучшить UX/UI сайта: исправить битые элементы, адаптировать навигацию под устройства (TikTok-style scroll), добавить поиск в репертуаре, убрать navbar на десктопе.

## 2. CONTEXT SUMMARY
- **Файлы:** `new_site/*.html` — 7 страниц (index, video, foto, repertuar, kontakty, cover, folk, rusalki)
- **Ассеты:** `d/` — фото, `f/` — видео
- **Проблемы:** 
  - Битые ссылки: `bayan_logo.png`, `anime_*.png`
  - Navbar не нужен на десктопе (>768px)
  - Контакты обрезаются на телефоне
  - Кнопки "Кавер-группа/Фолк/Русалки" не выделены как разделы
  - Нет поиска в репертуаре
  - Видео без обложек

## 3. APPROACH OVERVIEW
Конвертировать в **SPA с TikTok-scroll**: вертикальный swipe переключает экраны на мобильных. Navbar только на мобильных. Десктоп — боковая навигация или стрелки. Пофиксить битые картинки через emoji/fallback.

## 4. IMPLEMENTATION STEPS

### Step 1: Создать единую SPA-структуру (index.html → multi-screen)
- Все экраны в одном HTML через `<section class="screen">`
- CSS: `scroll-snap-type: y mandatory` для TikTok-эффекта
- JS: IntersectionObserver для активной страницы
- На десктопе: убрать navbar, добавить стрелки ◀ ▶ по бокам + dots справа
- На мобильных (<768px): bottom navbar сохранить, адаптировать карточки

### Step 2: Пофиксить битые картинки
- `d/bayan_logo.png` → emoji 🪗 (аккордеон/баян)
- `d/anime_*.png` → gradient placeholder + emoji 🎵
- Все bitmap-иконки контактов → emoji

### Step 3: Редизайн kontakty
- Контактные карточки: сделать компактнее
- На телефоне: 2 колонки grid, уменьшить padding
- Форму можно оставить, но сделать меньше

### Step 4: Переделать секции (Кавер-группа / Фолк / Русалки)
- Горизонтальный скролл карточек
- Добавить заголовок "Разделы" перед ними
- Стильные градиентные рамки, hover-эффекты

### Step 5: Добавить поиск в repertuar
- Input вверху: "Поиск по песням..."
- Live filter: скрывать не matching songs
- Empty state: "Такая песня не нашлась 🤷"

### Step 6: Фикс video.html и fotogalereya.html
- video: добавить gradient + emoji как fallback для обложек
- foto: gradient placeholders если фото не загружаются

### Step 7: Добавить search в репертуар
- Простой JS filter по имени/артисту
- Debounce 300ms для производительности

## 5. TESTING AND VALIDATION
- Открыть сайт → проверить все экраны через scroll
- Mobile view (F12): убедиться что navbar виден и работает
- Desktop (>768px): navbar скрыт, стрелки навигации работают
- Клик по контактам → открывает tel:/mailto:
- Поиск в репертуаре → фильтрует список песен
- Проверить все картинки → должны показывать emoji или gradient
