# Лабораторная работа №9. Использование GitHub Actions для CI/CD в .NET

## Цели лабораторной работы
1. Освоить основы работы с GitHub Actions.
2. Настроить автоматическую сборку и тестирование .NET-приложения.
3. Настроить автоматическое развертывание приложения.

## Документация
[Документация по GH Actions](https://docs.github.com/ru/actions)

## Описание задания
В рамках этой лабораторной работы вы настроите Continuous Integration и Continuous Deployment (CI/CD) для простого .NET-приложения с использованием GitHub Actions.

## Требования

1. Установленный Git.
2. Установленный .NET SDK.
3. Аккаунт на GitHub.

## Шаги выполнения

### Шаг 1: Создание .NET-приложения

1. Создайте новое .NET-приложение командой:
   ```bash
   dotnet new console -n SampleApp
   cd SampleApp
   ```

2. Инициализируйте новый репозиторий Git:
   ```bash
   git init
   ```

3. Сделайте первый коммит:
   ```bash
   git add .
   git commit -m "Initial commit"
   ```

4. Создайте новый репозиторий на GitHub и свяжите его с локальным репозиторием:
   ```bash
   git remote add origin https://github.com/your-username/SampleApp.git
   git push -u origin master
   ```

### Шаг 2: Настройка GitHub Actions для CI

1. Создайте папку `.github/workflows`:
   ```bash
   mkdir -p .github/workflows
   ```

2. Создайте файл `ci.yml` в папке `.github/workflows` со следующим содержимым:
   ```yaml
   name: .NET CI

   on:
     push:
       branches: [ master ]
     pull_request:
       branches: [ master ]

   jobs:
     build:

       runs-on: ubuntu-latest

       steps:
       - uses: actions/checkout@v2
       - name: Setup .NET
         uses: actions/setup-dotnet@v1
         with:
           dotnet-version: '6.0.x'
       - name: Restore dependencies
         run: dotnet restore
       - name: Build
         run: dotnet build --no-restore
       - name: Test
         run: dotnet test --no-build --verbosity normal
   ```

3. Сделайте коммит и пуш изменений:
   ```bash
   git add .
   git commit -m "Setup GitHub Actions for CI"
   git push
   ```

4. Перейдите на страницу Actions вашего репозитория на GitHub, чтобы убедиться, что запуск выполнен успешно.

### Шаг 3: Настройка GitHub Actions для CD

1. Добавьте следующие шаги в конец вашего файла `ci.yml` для развёртывания:
   ```yaml
   jobs:
     build:
       ...
       
       steps:
       ...
       - name: Publish
         run: dotnet publish -c Release -o out
       - name: Deploy to Azure App Service
         uses: azure/webapps-deploy@v2
         with:
           app-name: 'YOUR_APP_SERVICE_NAME'
           slot-name: 'production'
           publish-profile: ${{ secrets.AzureWebAppPublishProfile }}
           package: './out'
   ```

2. На портале Azure создайте новый веб-приложение и скачайте профиль публикации.

3. Перейдите в настройки вашего репозитория на GitHub, добавьте секрет `AzureWebAppPublishProfile` и вставьте туда содержимое файла профиля публикации.

4. Сделайте коммит и пуш изменений:
   ```bash
   git add .
   git commit -m "Setup GitHub Actions for CD"
   git push
   ```

### Проверка работы
Перейдите в раздел Actions вашего репозитория на GitHub и убедитесь, что оба workflow выполняются корректно при каждом пуше. Убедитесь, что ваше приложение развёрнуто на Azure.

## Самостоятельная работа
### Задание 1: Автоматическая сборка и тестирование проекта
**Задание:** Настройте GitHub Actions для автоматической сборки и тестирования проекта на .NET при каждом push в ветку `main`.

1. Создайте workflow файл в `.github/workflows` и назовите его `build-and-test.yml`.
2. Настройте триггер на событие `push` для ветки `main`.
3. Настройте шаги для:
    - Установки .NET SDK.
    - Сборки проекта.
    - Запуска юнит-тестов.
4. Убедитесь, что все шаги прошли успешно для подтверждения задания.

Понял! Вот вариант задания, который не включает деплой в облако.

### Задание 2: Генерация и публикация отчетов о покрытии кода
**Задание:** Настройте GitHub Actions для генерации и публикации отчетов о покрытии кода при каждом push в ветку `main`.

1. Создайте workflow файл в `.github/workflows` и назовите его `code-coverage.yml`.
2. Настройте триггер на событие `push` для ветки `main`.
3. Добавьте шаги для:
    - Установки .NET SDK.
    - Сборки проекта.
    - Запуска тестов с генерацией отчетов о покрытии кода (используя инструменты типа Coverlet).
    - Публикации отчетов о покрытии кода в формате HTML в GitHub Pages (используйте `gh-pages` branch).
4. Убедитесь, что отчеты о покрытии кода доступны на GitHub Pages и содержат актуальные данные.

#### Пример `code-coverage.yml`:

```yaml
name: CI - Code Coverage

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v2

    - name: Set up .NET Core
      uses: actions/setup-dotnet@v2
      with:
        dotnet-version: '6.0.x'  # Укажите вашу версию .NET

    - name: Restore dependencies
      run: dotnet restore

    - name: Build project
      run: dotnet build --configuration Release

    - name: Run tests with coverage
      run: dotnet test --configuration Release --collect:"XPlat Code Coverage"

    - name: Generate coverage report
      run: |
        REPORT_DIR=$(pwd)/coverage
        mkdir -p $REPORT_DIR
        reportgenerator -reports:**/coverage.cobertura.xml -targetdir:$REPORT_DIR -reporttypes:Html

    - name: Deploy coverage report to GitHub Pages
      uses: peaceiris/actions-gh-pages@v3
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        publish_dir: ./coverage
```

Для выполнения этого задания необходимо:

1. Добавить инструмент для анализа покрытия кода, например, Coverlet, в проект на .NET.
2. Настроить генерацию отчетов о покрытии кода в формате HTML.
3. Настроить GitHub Pages для публикации отчетов.

Работая над этим заданием, студенты научатся:

- Использовать покрытия кода для анализа качества тестирования.
- Интегрировать инструменты тестирования и генерации отчетов с CI/CD процессами.
- Публиковать отчеты на GitHub Pages для удобного доступа и просмотра.

### Задание 3: Анализ кода с помощью SonarCloud
**Задание:** Настройте GitHub Actions для запуска анализа кода с помощью SonarCloud при каждом pull request в ветку `main`.

1. Создайте workflow файл в `.github/workflows` и назовите его `code-analysis.yml`.
2. Настройте триггер на событие `pull_request` для ветки `main`.
3. Добавьте шаги для:
    - Установки .NET SDK.
    - Установки SonarCloud CLI.
    - Конфигурации и запуска анализа кода с использованием SonarCloud (с использванием токенов).
4. Убедитесь, что результаты анализа кода отображаются в панели SonarCloud.

### Задание 4: Генерация документации с помощью DocFX
**Задание:** Настройте GitHub Actions для автоматической генерации документации проекта с помощью DocFX и публикации её в GitHub Pages.

1. Создайте workflow файл в `.github/workflows` и назовите его `generate-docs.yml`.
2. Настройте триггер на событие `push` для ветки `main`.
3. Добавьте шаги для:
    - Установки DocFX.
    - Сборки и генерации документации.
    - Публикации сгенерированной документации в GitHub Pages (используйте `gh-pages` branch).
4. Убедитесь, что документация доступна на GitHub Pages.

### Задание 5: Проверка кода на соответствие стилю с использованием StyleCop
**Задание:** Настройте GitHub Actions для проверки кода на соответствие стилю с использованием StyleCop при каждом pull request в репозиторий.

1. Создайте workflow файл в `.github/workflows` и назовите его `style-check.yml`.
2. Настройте триггер на событие `pull_request`.
3. Добавьте шаги для:
    - Установки .NET SDK.
    - Установки и конфигурации StyleCop.
    - Запуска проверки стиля кода.
4. Убедитесь, что результаты проверки отображаются в интерфейсе GitHub при создании pull request.

Эти задания позволят студентам понять и применить различные аспекты автоматизации рабочего процесса с помощью GitHub Actions в контексте проектов на .NET.

## Заключение
В этой лабораторной работе вы настроили базовый процесс CI/CD для .NET-приложения с использованием GitHub Actions и Azure. Вы можете расширить и улучшить этот процесс, добавляя новые шаги и интеграции по мере необходимости.