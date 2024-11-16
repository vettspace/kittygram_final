# Kittygram
### Социальная сеть для любителей кошек

![Статус сборки](https://github.com/vettspace/kittygram_final/actions/workflows/main.yml/badge.svg)

## О проекте

**Kittygram** — это современная социальная платформа, созданная для объединения всех, кто обожает кошек. Здесь пользователи могут делиться фотографиями своих пушистых друзей, отмечать их достижения и взаимодействовать с публикациями других участников сообщества.

### Основные возможности:
- Регистрация и аутентификация пользователей
- Создание профилей для котиков с возможностью добавления фотографий
- Управление и добавление достижений питомцев
- Просмотр и взаимодействие с публикациями других пользователей
- Редактирование и удаление собственных публикаций

## Технологический стек

### Backend:
- **Python 3**
- **Django**
- **Django REST Framework**
- **PostgreSQL**
- **Gunicorn**

### Frontend:
- **React**
- **JavaScript**
- **Node.js**

### Инфраструктура:
- **Docker**
- **Nginx**
- **GitHub Actions (CI/CD)**

## Развертывание проекта

### Предварительные требования:
1. Установленные Docker и Docker Compose
2. Установленный Git

### Шаги по установке:

1. Клонируйте репозиторий:
   ```bash
   git clone https://github.com/vettspace/kittygram_final.git
   cd kittygram_final
   ```

2. Создайте файл `.env` в корневой директории проекта и добавьте следующие переменные:
   ```
   POSTGRES_DB=kittygram
   POSTGRES_USER=kittygram_user
   POSTGRES_PASSWORD=your_password
   DB_HOST=kittygram
   DB_PORT=5432
   SECRET_KEY=your_django_secret_key
   DEBUG=False
   ALLOWED_HOSTS=your_domain,localhost,127.0.0.1
   ```

3. Запустите проект с помощью Docker Compose:
   ```bash
   sudo docker compose -f docker-compose.production.yml up -d
   ```

4. Выполните миграции и соберите статические файлы:
   ```bash
   sudo docker compose -f docker-compose.production.yml exec backend python manage.py migrate
   sudo docker compose -f docker-compose.production.yml exec backend python manage.py collectstatic
   ```

### Настройка Nginx:

1. Установите Nginx:
   ```bash
   sudo apt install nginx -y
   ```

2. Настройте конфигурацию сервера:
   ```nginx
   server {
       server_name ваш_домен;
       server_tokens off;
       
       location / {
           proxy_pass http://127.0.0.1:9000;
           proxy_set_header Host $host;
           proxy_set_header X-Real-IP $remote_addr;
       }
   }
   ```

## CI/CD

Проект настроен на автоматическое развертывание при пуше в основную ветку. Убедитесь, что в настройках репозитория GitHub добавлены необходимые секреты:
- `DOCKER_USERNAME`
- `DOCKER_PASSWORD`
- `HOST`
- `USER`
- `SSH_KEY`
- `SSH_PASSPHRASE`

## Автор

**Виталий Орлов**  
GitHub: [vettspace](https://github.com/vettspace)