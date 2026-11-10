# Автовспышка задней камеры

[Обращение №67434](https://bugs.telegram.org/c/67434)

Статус проекта: ожидает воспроизведения.

## Проверка

Проверить отдельно фото и видео при постоянном слабом освещении. Записать выбранный API, доступные режимы и фактический запрос камеры.

## Что запрашивает клиент

В [CameraController.recordVideo](https://github.com/DrKLO/Telegram/blob/7be672ead283d022812d75c729d3a04dd4c2a2c6/TMessagesProj/src/main/java/org/telegram/messenger/camera/CameraController.java#L649-L701) обе ветки записи Camera1 явно передают torch при выбранном on и off при выбранном auto. Это объясняет, почему при старте видео драйвер может получить off даже до преобразования параметров в HAL. Для Camera2 здесь отдельная ветка. Для фото [CameraSession](https://github.com/DrKLO/Telegram/blob/7be672ead283d022812d75c729d3a04dd4c2a2c6/TMessagesProj/src/main/java/org/telegram/messenger/camera/CameraSession.java#L418-L425) передаёт выбранный режим, если не запрошен фонарь. Нужен замер при слабом свете отдельно для фото и видео, с подтверждением активного API. По исходникам нельзя установить, сработала ли вспышка на конкретном телефоне.
