# Решение To-Be для MVP «Медикаменте» (C4 Model: Container Diagram)

```mermaid
C4Container
    System_Boundary(b0, "Медикаменте") {
        Container(web, "Клиентский портал", "React + Nest.js", "Предоставляет интерфейс для записи к врачу и доступа к данным")
        Container(int, "Портал сотрудников", "Angular + Java", "Управление записями, доступ к мед. картам")
        Container(pay, "Платёжный шлюз", "Python", "Интеграция с банками и 1С")
        Container(crm, "CRM-система", "PostgreSQL + Elastic", "Учёт пациентов, аналитика")
        Container(db, "СУБД", "PostgreSQL TDE", "Хранение PII и мед. данных")
        Container(storage, "Файловое хранилище", "S3 + MinIO", "Шифрованные PDF/анализы")
        Container(api, "API лаборатории", "gRPC + OAuth2", "Защищённая интеграция")
        Container(siem, "SIEM-система", "Splunk", "Аудит и мониторинг")
    }

    Rel(web, db, "Запись данных", "HTTPS/TLS 1.3")
    Rel(int, db, "Чтение/запись", "RBAC + ABAC")
    Rel(pay, db, "Обновление платежей", "TLS + MTLS")
    Rel(api, db, "Синхронизация анализов", "AES-256")
    Rel(crm, storage, "Тегирование данных", "DLP-сканирование")
    Rel(siem, db, "Сбор логов", "Syslog")
    Rel(siem, storage, "Мониторинг доступа", "AWS CloudTrail")

    UpdateLayoutConfig($c4ShapeInRow="3", $c4BoundaryInRow="2")