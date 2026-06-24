# Сайт-приглашение на день рождения Кирилла — План реализации

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Создать одностраничный сайт-приглашение в космической тематике и разместить на GitHub Pages.

**Architecture:** Единственный HTML-файл с инлайн CSS и JS (без фреймворков). Никаких сборщиков, зависимостей и бэкенда. README с инструкцией по деплою.

**Tech Stack:** HTML5, CSS3 (keyframe-анимации), Google Fonts, GitHub Pages.

---

## Файловая структура

```
kirill/
├── index.html      — главная (и единственная) страница сайта
└── README.md       — инструкция по деплою на GitHub Pages
```

---

### Task 1: Создать `index.html` — страница приглашения

**Files:**
- Create: `index.html`

- [ ] **Step 1: Написать HTML-каркас**

```html
<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Кирилл приглашает на день рождения!</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Nunito:wght@400;700;800;900&display=swap" rel="stylesheet">
  <style>
    /* CSS будет здесь */
  </style>
</head>
<body>
  <!-- HTML контент будет здесь -->
  <script>
    // JS будет здесь
  </script>
</body>
</html>
```

- [ ] **Step 2: Написать CSS — фон, звёзды, общие стили**

Стили включают:
- `body`: `#0B0E27` фон, Nunito шрифт, overflow-x: hidden, min-height: 100vh
- Контейнер `.stars` — абсолютное позиционирование на весь экран, pointer-events: none
- Псевдоэлементы `::before` и `::after` на `.stars` для двух слоёв звёзд (box-shadow techniquе: генерируем 50-100 случайных позиций для звёзд через box-shadow)
- `.star` классы с анимацией мерцания (opacity pulse)

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Nunito', sans-serif;
  background: #0B0E27;
  color: #fff;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  overflow-x: hidden;
  position: relative;
}

/* Звёздное небо */
.stars {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 0;
}

.stars::before,
.stars::after {
  content: '';
  position: absolute;
  width: 2px;
  height: 2px;
  border-radius: 50%;
  animation: twinkle 3s ease-in-out infinite alternate;
}

.stars::before {
  box-shadow:
    20px 40px 0 #fff, 80px 120px 0 #fff, 150px 60px 0 #fff,
    220px 180px 0 #fff, 310px 90px 0 #fff, 400px 200px 0 #fff,
    500px 50px 0 #fff, 580px 170px 0 #fff, 680px 100px 0 #fff,
    750px 220px 0 #fff, 100px 300px 0 #fff, 300px 350px 0 #fff,
    500px 380px 0 #fff, 700px 320px 0 #fff, 200px 450px 0 #fff,
    450px 420px 0 #fff, 620px 480px 0 #fff, 800px 400px 0 #fff,
    900px 150px 0 #fff, 1000px 250px 0 #fff;
  animation-delay: 0s;
}

.stars::after {
  width: 1px;
  height: 1px;
  box-shadow:
    50px 80px 0 #FFD700, 180px 200px 0 #FFD700, 350px 140px 0 #FFD700,
    480px 280px 0 #FFD700, 600px 60px 0 #FFD700, 820px 180px 0 #FFD700,
    950px 320px 0 #FFD700, 150px 380px 0 #FFD700, 550px 350px 0 #FFD700,
    780px 450px 0 #FFD700, 320px 500px 0 #FFD700, 680px 550px 0 #FFD700,
    880px 500px 0 #FFD700, 1020px 400px 0 #FFD700;
  animation-delay: 1.5s;
}

@keyframes twinkle {
  0% { opacity: 0.3; }
  100% { opacity: 1; }
}
```

- [ ] **Step 3: Написать CSS — ракета**

Анимация ракеты: пролёт снизу-вверх по диагонали, чуть покачиваясь.

```css
.rocket {
  position: fixed;
  z-index: 1;
  font-size: 48px;
  animation: fly 6s ease-in-out infinite;
  pointer-events: none;
}

@keyframes fly {
  0% {
    transform: translate(-100px, 100vh) rotate(-30deg);
    opacity: 0;
  }
  10% {
    opacity: 1;
  }
  90% {
    opacity: 1;
  }
  100% {
    transform: translate(calc(100vw + 100px), -100px) rotate(-30deg);
    opacity: 0;
  }
}
```

- [ ] **Step 4: Написать CSS — основной контент**

```css
.content {
  position: relative;
  z-index: 2;
  text-align: center;
  padding: 2rem;
  max-width: 600px;
}

h1 {
  font-size: clamp(1.8rem, 5vw, 3rem);
  font-weight: 900;
  color: #FF6B35;
  margin-bottom: 0.5rem;
  line-height: 1.2;
}

.age-badge {
  display: inline-block;
  background: linear-gradient(135deg, #FF6B35, #FFD700);
  color: #0B0E27;
  font-weight: 900;
  font-size: clamp(2rem, 6vw, 3.5rem);
  padding: 0.3rem 1.5rem;
  border-radius: 50px;
  margin: 1rem 0 2rem;
  box-shadow: 0 0 30px rgba(255, 107, 53, 0.4);
}

.details {
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 20px;
  padding: 2rem;
  backdrop-filter: blur(10px);
}

.detail-item {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  margin-bottom: 1rem;
  font-size: clamp(1rem, 3vw, 1.3rem);
  font-weight: 600;
}

.detail-item:last-child {
  margin-bottom: 1.5rem;
}

.detail-icon {
  font-size: 1.5rem;
  width: 2rem;
  text-align: center;
}

.detail-label {
  color: #8ECAE6;
  font-weight: 700;
  margin-right: 0.25rem;
}

.map-btn {
  display: inline-block;
  background: #FF6B35;
  color: #fff;
  text-decoration: none;
  font-weight: 800;
  font-size: 1.1rem;
  padding: 0.8rem 2rem;
  border-radius: 50px;
  transition: transform 0.2s, box-shadow 0.2s;
  box-shadow: 0 4px 15px rgba(255, 107, 53, 0.4);
}

.map-btn:hover {
  transform: translateY(-2px) scale(1.05);
  box-shadow: 0 6px 25px rgba(255, 107, 53, 0.6);
}

.footer-text {
  margin-top: 2rem;
  font-size: clamp(1.2rem, 4vw, 1.8rem);
  font-weight: 800;
  color: #FFD700;
  text-shadow: 0 0 20px rgba(255, 215, 0, 0.3);
}
```

- [ ] **Step 5: Написать HTML-контент страницы (внутри `<body>`)**

```html
<div class="stars"></div>
<div class="rocket">🚀</div>

<div class="content">
  <h1>Кирилл приглашает на день рождения!</h1>

  <div class="age-badge">4 года</div>

  <div class="details">
    <div class="detail-item">
      <span class="detail-icon">🗓</span>
      <span><span class="detail-label">Дата:</span> 4 июля 2026</span>
    </div>
    <div class="detail-item">
      <span class="detail-icon">⏰</span>
      <span><span class="detail-label">Время:</span> 13:00</span>
    </div>
    <div class="detail-item">
      <span class="detail-icon">📍</span>
      <span><span class="detail-label">Место:</span> Kids Castle</span>
    </div>
    <a class="map-btn" href="#" target="_blank" rel="noopener noreferrer" id="mapLink">
      Открыть на Яндекс Картах
    </a>
  </div>

  <div class="footer-text">Ждём тебя!</div>
</div>
```

- [ ] **Step 6: Написать JS — вставка ссылки на Яндекс Карты**

```html
<script>
  // Ссылка на Яндекс Карты — замените при необходимости
  document.getElementById('mapLink').href = 'https://yandex.ru/maps/org/kids_castle/124440740971/?indoorLevel=1&ll=37.380480%2C55.841348&mode=search&sctx=ZAAAAAgBEAAaKAoSCQoRcAhVrEJAES6QoPgx7EtAEhIJhbacS3FVeT8RfQkVHF4QYT8iBgABAgMEBSgKOABAuZIHSABiY3JlYXJyPXNjaGVtZV9Mb2NhbC9HZW8vQWR2ZXJ0cy9SZWFycmFuZ2VCeUF1Y3Rpb24vU2ltaWxhck9yZ3NMaXN0QXVjdGlvbi9FbmFibGVGaWx0cmF0aW9uQnlXaW5kb3c9MWoCcnWdAc3MzD2gAQCoAQC9AQN6XdnCARHriPzJzwO248bhbJ6H8ba8BIICLNC00LXRgtGB0LrQsNGPINCY0LPRgNC%2B0LLQsNGPINC60L7QvNC90LDRgtCwigIMMTkxNDcyNjg5NjcykgIAmgIMZGVza3RvcC1tYXBzqgIMMTYxMzM4MTY0OTg1&sll=37.378226%2C55.841348&sspn=0.016437%2C0.005536&text=ltncrf%20%D0%98%D0%B3%D1%80%D0%BE%D0%B2%D0%B0%D1%8F%20%D0%BA%D0%BE%D0%BC%D0%BD%D0%B0%D1%82%D0%B0&z=16.87';
</script>
```

- [ ] **Step 7: Открыть в браузере и проверить визуально**

Открыть `index.html` в браузере (через `file://` протокол). Убедиться что:
- Звёзды мерцают
- Ракета летит
- Верстка адаптивная
- Кнопка с Яндекс Картами отображается корректно

---

### Task 2: Создать `README.md` — инструкция по деплою

**Files:**
- Create: `README.md`

- [ ] **Step 1: Написать README с инструкцией**

```markdown
# День рождения Кирилла 🚀

Сайт-приглашение на день рождения.

## Как разместить на GitHub Pages

1. Создайте репозиторий на GitHub (например, `kirill-birthday`)
2. Загрузите файлы в репозиторий:
   ```bash
   git init
   git add .
   git commit -m "initial commit"
   git remote add origin https://github.com/ВАШ_ЛОГИН/kirill-birthday.git
   git branch -M main
   git push -u origin main
   ```
3. В репозитории на GitHub:
   - Перейдите в **Settings → Pages**
   - В разделе **Branch** выберите `main` и `/ (root)`
   - Нажмите **Save**
4. Через 1-2 минуты сайт будет доступен по адресу:
   `https://ВАШ_ЛОГИН.github.io/kirill-birthday/`

## Ссылка на Яндекс Карты

Ссылка уже встроена в `index.html`. Если нужно изменить — найдите строку с `mapLink.href` в конце файла.

## Кастомизация

- **Текст:** меняйте в `<body>` index.html
- **Цвета:** правьте CSS-переменные в `<style>` index.html
- **Анимации:** меняйте параметры в `@keyframes`
```

- [ ] **Step 2: Проверить, что все файлы на месте**

```bash
ls -la
# Должны быть: index.html README.md docs/ (если docs уже есть)
```
