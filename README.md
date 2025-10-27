# MSA-GoFuture: Архитектура микросервисной платформы

Проект посвящен миграции монолитной ride-sharing платформы "GoFuture" на микросервисную архитектуру с поддержкой событийно-ориентированного подхода, глобального развертывания, ML-платформы и мультитенантности.

---

## Задание 1: Проектирование доменов

**Директория:** [`Task1/`](./Task1/)

### Результаты

- **Нефункциональные требования** ([result.md](./Task1/result.md#1-список-нефункциональных-требований)): 10 требований для целевой архитектуры
- **Диаграмма C2 To-Be** ([изображение](./Task1/img/GoFuture_ToBeArchitecture_C2.png) | [исходник](./Task1/diagrams/C2-to-be.puml)): 9 микросервисов с механизмами обратной совместимости
- **Очередность выделения сервисов** ([result.md](./Task1/result.md#3-описание-очерёдности-выделения-сервисов)): обоснование порядка миграции
- **План миграции** ([result.md](./Task1/result.md#4-план-миграции)): пошаговая стратегия перехода от монолита

**Ключевые технологии:** Kafka, RabbitMQ+Celery, Kong, PostgreSQL, Redis, Elasticsearch, Django/FastAPI

---

## Задание 2: Архитектура событийной платформы

**Директория:** [`Task2/`](./Task2/)

### Результаты

- **Диаграмма C2 событийной платформы** ([изображение](./Task2/img/GoFuture_EventPlatform_C2.png) | [исходник](./Task2/diagrams/C2-event-platform.puml)): Kafka, producers, consumers, stream processing
- **Доменные события** ([result.md](./Task2/result.md#1-доменные-события)): модели событий для Booking, Driver, Payment, Pricing
- **Kafka топики** ([result.md](./Task2/result.md#2-kafka-топики)): схемы с партиционированием по region_id
- **Saga Pattern** ([result.md](./Task2/result.md#4-saga-pattern)): Choreography для координации распределенных транзакций
- **Мониторинг** ([result.md](./Task2/result.md#6-мониторинг)): Prometheus, Grafana, Alertmanager с ключевыми метриками

**Ключевые технологии:** Kafka, Flink, Schema Registry (Avro), ClickHouse

---

## Задание 3: Глобальное развертывание

**Директория:** [`Task3/`](./Task3/)

### Результаты

- **Диаграмма C2 multi-region** ([изображение](./Task3/img/GoFuture_GlobalDeployment_C2.png) | [исходник](./Task3/diagrams/C2-global-deployment.puml)): 3 региона с Edge Security
- **Выбор регионов** ([result.md](./Task3/result.md#1-обоснование-выбора-регионов)): Россия, Сингапур, Сан-Паулу
- **Схема репликации** ([result.md](./Task3/result.md#2-схема-репликации-данных)): Patroni для PostgreSQL, Kafka MirrorMaker
- **Геомаршрутизация** ([result.md](./Task3/result.md#3-схема-геомаршрутизации)): GeoDNS + Health Checks
- **Диаграмма Failover** ([изображение](./Task3/img/GoFuture_Failover_C2.png) | [исходник](./Task3/diagrams/C2-failover.puml)): сценарии отказа и переключения
- **Таблица сценариев отказа** ([result.md](./Task3/result.md#4-план-failover)): 5 сценариев с механизмами восстановления
- **Стратегия compliance** ([result.md](./Task3/result.md#5-стратегия-соответствия-регуляторным-требованиям)): GDPR, LGPD, PDPA, PCI DSS

**Ключевые технологии:** Patroni, Kafka MirrorMaker, GeoDNS, WAF (Yandex SmartWeb), Qrator

**SLA:** 99.99% availability

---

## Задание 4: Data & ML Platform

**Директория:** [`Task4/`](./Task4/)

### Результаты

- **Диаграмма C2 Data & ML Platform** ([изображение](./Task4/img/GoFuture_DataML_Platform_C2.png) | [исходник](./Task4/diagrams/C2-data-ml-platform.puml)): полный пайплайн от источников до BI
- **Архитектура пайплайна** ([result.md](./Task4/result.md#1-источники-данных)): Ingestion → Storage → Processing → ML → BI
- **ML Use Cases** ([result.md](./Task4/result.md#5-ml-platform)): динамическое ценообразование, прогноз спроса, обнаружение фрода
- **Качество данных** ([result.md](./Task4/result.md#8-качество-данных)): валидация, lineage, идемпотентность

**Ключевые технологии:** Kafka Connect, Spark, dbt, MLflow, Feast, Airflow

**Data Lake слои:** Bronze → Silver → Gold

---

## Задание 5: Мультитенантная платформа

**Директория:** [`Task5/`](./Task5/)

### Результаты

- **Диаграмма C2 мультитенантной архитектуры** ([изображение](./Task5/img/GoFuture_Multitenant_Architecture_C2.png) | [исходник](./Task5/diagrams/C2-multitenant-architecture.puml)): IAM, Tenant Management, Data Isolation
- **Диаграмма C3 процесса онбординга** ([изображение](./Task5/img/GoFuture_Onboarding_Flow_C3.png) | [исходник](./Task5/diagrams/C3-onboarding-flow.puml)): автоматизированный workflow
- **Модель изоляции данных** ([result.md](./Task5/result.md#1-модель-изоляции-данных)): гибридный подход (Dedicated + Shared DB)
- **Таблица ролей** ([result.md](./Task5/result.md#таблица-ролей-и-доступов)): 6 ролей с уровнями доступа
- **Процесс онбординга** ([result.md](./Task5/result.md#3-автоматизированный-onboarding)): 7 шагов автоматизации через Airflow
- **Мониторинг multi-tenant** ([result.md](./Task5/result.md#4-мониторинг-мультитенантного-окружения)): метрики per-tenant, квоты, алерты

**Ключевые технологии:** Keycloak (SSO + RBAC), Kong, PostgreSQL RLS, Airflow, Prometheus, Grafana

---

## Эволюция архитектуры

```
Монолит (исходное состояние)
    ↓
Task1: Микросервисная архитектура (9 сервисов)
    ↓
Task2: Event-Driven архитектура (Kafka + Saga)
    ↓
Task3: Multi-Region развертывание (99.99% SLA)
    ↓
Task4: Data & ML Platform (ML-driven бизнес)
    ↓
Task5: Multi-Tenant SaaS (изоляция партнёров)
```

---

## Технологический стек

| Категория | Технологии |
|-----------|------------|
| **API Gateway** | Kong |
| **Микросервисы** | Django, FastAPI |
| **Event Streaming** | Kafka, Schema Registry (Avro) |
| **Message Queue** | RabbitMQ + Celery |
| **Базы данных** | PostgreSQL, Redis, ClickHouse, Elasticsearch |
| **Stream Processing** | Flink |
| **Data Processing** | Spark, dbt |
| **ML Platform** | MLflow, Feast |
| **Orchestration** | Apache Airflow, Kubernetes |
| **IAM** | Keycloak (SSO + RBAC) |
| **Мониторинг** | Prometheus, Grafana, Loki, Alertmanager |
| **Репликация** | Patroni, Kafka MirrorMaker |
| **Geo-Routing** | GeoDNS |
| **Security** | WAF (Yandex SmartWeb), DDoS (Qrator), Firewall |
| **Data Quality** | Great Expectations, OpenLineage |
| **Cloud** | Yandex Cloud |

---

## Ключевые метрики проекта

- **Микросервисы:** 9 сервисов
- **Регионы:** 3 (Россия, Сингапур, Сан-Паулу)
- **Нагрузка:** 500k+ конкурентных поездок
- **Availability:** 99.99%
- **Модели изоляции:** Dedicated + Shared DB
- **Роли:** 6 ролей с RBAC
- **ML Use Cases:** 3 (ценообразование, прогноз спроса, фрод)
- **Диаграммы:** 7 (C2/C3)
- **Документация:** ~900 строк
