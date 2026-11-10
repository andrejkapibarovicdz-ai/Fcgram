# F_craft_gramm — v0.3 (POCO C40 / Android 11)

## Статус без преувеличений

**Реализовано в исходниках:**
- Ретро-макет списка чатов на Android Views.
- Явная плашка «ПРЕДПРОСМОТР · TDLib ещё не подключена».
- Демонстрационные строки больше не маскируются под реальные переписки: при нажатии показывается пояснение.
- Добавлен контракт `TelegramEngine` и модели состояния авторизации/диалогов для будущего адаптера.
- Добавлен workflow для сборки официальной TDLib с Java/JNI под `arm64-v8a`, Android API 23.

**Пока не реализовано и не проверено:**
- Реальный TDLib JNI-адаптер.
- Авторизация, получение диалогов и отправка сообщений.
- Сборка APK в этой среде. Здесь не запускалась Android Gradle сборка и не собиралась TDLib.

## Следующий шаг: запустить сборку TDLib

1. Создай пустой репозиторий GitHub.
2. Загрузи в него всё содержимое этого проекта.
3. Открой Actions → `Build official TDLib for Android` → `Run workflow`.
4. Дождись завершения и скачай artifact `tdlib-android-arm64-java`.

Workflow использует официальные Android build scripts из `tdlib/example/android`. Они сами проверяют окружение, загружают Android SDK, собирают OpenSSL и TDLib. Параметры сборки: Java/JNI interface, min Android API 23, ABI arm64-v8a. Для POCO C40 это предполагаемая целевая ABI; перед финальной сборкой нужно проверить ABI устройства.

После успешной сборки TDLib следующий инженерный шаг — проверить структуру скачанного архива, подключить сгенерированные Java-классы и `.so` в app module, затем реализовать адаптер через актуальные API TDLib.

## Как открыть проект с телефона

Проект можно загрузить в GitHub через браузер Android. Для локальной сборки нужна Android IDE, которая поддерживает Android Gradle Plugin 8.7.3 и JDK 17. Ранее упоминавшийся AndroidIDE является архивированным проектом; не скачивай APK IDE с неизвестных сайтов. Можно выполнить облачную сборку через GitHub Actions после добавления Gradle wrapper или настроить сборку в доверенной Android IDE.

## Telegram API credentials

Для собственного приложения разработчик получает `api_id` и `api_hash` на https://my.telegram.org. Не присылай их в этот чат и не коммить в открытый репозиторий. Код входа Telegram и пароль двухэтапной проверки никому не передавай.

## Официальные материалы
- TDLib Android build guide: https://github.com/tdlib/td/tree/master/example/android
- TDLib overview: https://core.telegram.org/tdlib
- TDLib API examples: https://github.com/tdlib/td/tree/master/example/java
