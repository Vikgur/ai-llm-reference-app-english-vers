# Table of Contents

- [Repository Structure](#repository-structure)
- [Repository Organization Principles](#repository-organization-principles)
- [Top-level Repository](#top-level-repository)
  - [README.md](#readmemd)
  - [LICENSE](#license)
  - [SECURITY.md](#securitymd)
  - [CODEOWNERS](#codeowners)
  - [.env.example](#envexample)
- [Directory app/](#directory-app)
- [Directory models/](#directory-models)
- [Directory docker/](#directory-docker)
- [Directory helm/](#directory-helm)
- [Directory k8s/](#directory-k8s)
- [Directory ci/](#directory-ci)
- [Directory security/](#directory-security)
- [Directory observability/](#directory-observability)
- [Directory scripts/](#directory-scripts)
- [Directory docs/](#directory-docs)
- [Extension Points](#extension-points)
- [Conclusion](#conclusion)
- [Purpose of Directories and Files](#purpose-of-directories-and-files)
  - [README.md](#readmemd-1)
  - [LICENSE](#license-1)
  - [SECURITY.md](#securitymd-1)
  - [CODEOWNERS](#codeowners-1)
  - [.gitignore](#gitignore)
  - [.editorconfig](#editorconfig)
  - [.env.example](#envexample)
  - [app/](#app)
    - [app/README.md](#appreadmemd)
    - [app/api/](#appapi)
      - [app/api/main.py](#appapimainpy)
      - [app/api/routes.py](#appapiroutespy)
      - [app/api/schemas.py](#appapischemaspy)
      - [app/api/deps.py](#appapidepspy)
    - [app/llm/](#appllm)
      - [app/llm/tokenizer/](#appllmtokenizer)
        - [app/llm/tokenizer/vocab.json](#appllmtokenizervocabjson)
        - [app/llm/tokenizer/tokenizer.py](#appllmtokenizertokenizerpy)
        - [app/llm/tokenizer/README.md](#appllmtokenizerreadmemd)
      - [app/llm/embeddings/](#appllmembeddings)
        - [app/llm/embeddings/embedding.py](#appllmembeddingsembeddingpy)
        - [app/llm/embeddings/weights.bin](#appllmembeddingsweightsbin)
        - [app/llm/embeddings/README.md](#appllmembeddingsreadmemd)
      - [app/llm/transformer/](#appllmtransformer)
        - [app/llm/transformer/attention.py](#appllmtransformerattentionpy)
        - [app/llm/transformer/ffw.py](#appllmtransformerffwpy)
        - [app/llm/transformer/decoder.py](#appllmtransformerdecoderpy)
        - [app/llm/transformer/model.py](#appllmtransformermodelpy)
      - [app/llm/decoding/](#appllmdecoding)
        - [app/llm/decoding/sampler.py](#appllmdecodingsamplerpy)
        - [app/llm/decoding/decoder.py](#appllmdecodingdecoderpy)
        - [app/llm/decoding/guards.py](#appllmdecodingguardspy)
      - [app/llm/postprocess/](#appllmpostprocess)
        - [app/llm/postprocess/filters.py](#appllmpostprocessfilterspy)
        - [app/llm/postprocess/redaction.py](#appllmpostprocessredactionpy)
        - [app/llm/postprocess/policy.py](#appllmpostprocesspolicypy)
      - [app/llm/version.py](#appllmversionpy)
    - [app/config/](#appconfig)
      - [app/config/runtime.yaml](#appconfigruntimeyaml)
      - [app/config/limits.yaml](#appconfiglimitsyaml)
      - [app/config/logging.yaml](#appconfigloggingyaml)
    - [app/tests/](#apptests)
      - [app/tests/.gitkeep](#apptestsgitkeep)
  - [models/](#models)
    - [models/v1/](#modelsv1)
      - [models/v1/weights.bin](#modelsv1weightsbin)
      - [models/v1/checksum.sha256](#modelsv1checksumsha256)
      - [models/v1/model-card.md](#modelsv1model-cardmd)
    - [models/registry/](#modelsregistry)
      - [models/registry/.gitkeep](#modelsregistrygitkeep)
  - [docker/](#docker)
    - [docker/app/](#dockerapp)
      - [docker/app/Dockerfile](#dockerappdockerfile)
      - [docker/app/entrypoint.sh](#dockerappentrypointsh)
    - [docker/README.md](#dockerreadmemd)
  - [helm/](#helm)
    - [helm/charts/](#helmcharts)
    - [helm/charts/ai-llm-reference-app/](#helmchartsai-llm-reference-app)
      - [helm/charts/ai-llm-reference-app/Chart.yaml](#helmchartsai-llm-reference-appchartyaml)
      - [helm/charts/ai-llm-reference-app/templates/](#helmchartsai-llm-reference-apptemplates)
        - [helm/charts/ai-llm-reference-app/templates/deployment.yaml](#helmchartsai-llm-reference-apptemplatesdeploymentyaml)
        - [helm/charts/ai-llm-reference-app/templates/service.yaml](#helmchartsai-llm-reference-apptemplatsserviceyaml)
        - [helm/charts/ai-llm-reference-app/templates/hpa.yaml](#helmchartsai-llm-reference-apptemplateshpayaml)
        - [helm/charts/ai-llm-reference-app/templates/networkpolicy.yaml](#helmchartsai-llm-reference-apptemplatesnetworkpolicyyaml)
        - [helm/charts/ai-llm-reference-app/templates/podsecurity.yaml](#helmchartsai-llm-reference-apptemplatespodsecurityyaml)
        - [helm/charts/ai-llm-reference-app/templates/_helpers.tpl](#helmchartsai-llm-reference-apptemplates_helperstpl)
      - [helm/charts/ai-llm-reference-app/values.yaml](#helmchartsai-llm-reference-appvaluesyaml)
    - [helm/values/](#helmvalues)
      - [helm/values/dev.yaml](#helmvaluesdevyaml)
      - [helm/values/stage.yaml](#helmvaluesstageyaml)
      - [helm/values/prod.yaml](#helmvaluesprodyaml)
  - [k8s/](#k8s)
    - [k8s/base/](#k8sbase)
      - [k8s/base/namespace.yaml](#k8sbasenamespaceyaml)
      - [k8s/base/resourcequota.yaml](#k8sbaseresourcequotayaml)
      - [k8s/base/limitrange.yaml](#k8sbaselimitrangeyaml)
    - [k8s/security/](#k8ssecurity)
      - [k8s/security/psa.yaml](#k8ssecuritypsayaml)
      - [k8s/security/seccomp.yaml](#k8ssecurityseccompyaml)
      - [k8s/security/apparmor.yaml](#k8ssecurityapparmoryaml)
    - [k8s/manifests/](#k8smanifests)
      - [k8s/manifests/.gitkeep](#k8smanifestsgitkeep)
  - [ci/](#ci)
    - [ci/README.md](#cireadmemd)
    - [ci/entrypoints/](#cientrypoints)
      - [ci/entrypoints/build.yaml](#cientrypointsbuildyaml)
      - [ci/entrypoints/test.yaml](#cientrypointstestyaml)
      - [ci/entrypoints/release.yaml](#cientrypointsreleaseyaml)
    - [ci/policies/](#cipolicies)
      - [ci/policies/llm-input.rego](#cipoliciesllm-inputrego)
      - [ci/policies/llm-output.rego](#cipoliciesllm-outputrego)
      - [ci/policies/model-integrity.rego](#cipoliciesmodel-integrityrego)
    - [ci/artifacts/](#ciartifacts)
      - [ci/artifacts/.gitkeep](#ciartifactsgitkeep)
  - [security/](#security)
    - [security/threat-model/](#securitythreat-model)
      - [security/threat-model/threat-model.md](#securitythreat-modelthreat-modelmd)
    - [security/sbom/](#securitysbom)
      - [security/sbom/.gitkeep](#securitysbomgitkeep)
    - [security/attestations/](#securityattestations)
      - [security/attestations/.gitkeep](#securityattestationsgitkeep)
    - [security/runtime/](#securityruntime)
      - [security/runtime/seccomp.json](#securityruntimeseccompjson)
      - [security/runtime/readonly-fs.yaml](#securityruntimereadonly-fsyaml)
    - [security/README.md](#securityreadmemd)
  - [observability/](#observability)
    - [observability/metrics/](#observabilitymetrics)
      - [observability/metrics/prometheus.yaml](#observabilitymetricsprometheusyaml)
    - [observability/logs/](#observabilitylogs)
      - [observability/logs/fluent-bit.yaml](#observabilitylogsfluent-bityaml)
    - [observability/traces/](#observabilitytraces)
      - [observability/traces/otel.yaml](#observabilitytracesotelyaml)
    - [observability/dashboards/](#observabilitydashboards)
      - [observability/dashboards/.gitkeep](#observabilitydashboardsgitkeep)
  - [scripts/](#scripts)
    - [scripts/local-run.sh](#scriptslocal-runsh)
    - [scripts/kind-up.sh](#scriptskind-upsh)
    - [scripts/verify.sh](#scriptsverifysh)
  - [docs/](#docs)
    - [docs/architecture.md](#docsarchitecturemd)
    - [docs/llm-internals.md](#docsllm-internalsmd)
    - [docs/llm-security.md](#docsllm-securitymd)
    - [docs/supply-chain.md](#docssupply-chainmd)
    - [docs/deployment.md](#docsdeploymentmd)
    - [docs/repository-structure.md](#docsrepository-structuremd)

---

# Repository Structure

This document explains the structure of `ai-llm-reference-app` as a **deliberate architectural design**, not just a file hierarchy.

Structure goals:  
– strict separation of responsibilities  
– transparency of security and supply chain  
– audit and threat modeling convenience  
– scalability within a Sovereign AI platform  

The repository is designed to be:  
– read linearly  
– formally verifiable  
– extendable without breaking trust boundaries  

---

# Repository Organization Principles

The structure is built around the following principles:

– **Separation of responsibility**  
– **Security-first layout**  
– **Immutable artifacts**  
– **Explicit boundaries**  

Code, model, security, CI/CD, and runtime are **intentionally separated** into different directories.

---

# Top-level Repository

The repository root contains **governing and contract files**, not implementation.

## README.md  
Entry point. Explains *why* the repository exists and its role in Sovereign AI.

## LICENSE  
Legal usage framework. A required element of a trusted supply chain.

## SECURITY.md  
Project security governance. Defines scope, disclosure, and expectations.

## CODEOWNERS  
Formalizes ownership and change control.

## .env.example  
Documents expected runtime variables without exposing secrets.

Other files (`.gitignore`, `.editorconfig`) ensure consistency but do not carry architectural significance.

---

# Directory app/

`app/` is the **only location with application runtime code**.

It implements:  
– API  
– LLM inference pipeline  
– security guards  
– runtime configuration  

Important:  
– code is unaware of Kubernetes  
– code does not manage CI/CD  
– code contains no infrastructure logic  

This simplifies auditing and reduces the attack surface.

---

# Directory models/

`models/` contains the **model as an artifact**, not as part of the code.

It includes:  
– weights  
– checksum  
– model card  

The model is:  
– versioned separately  
– immutable  
– subject to integrity verification  

This separation is critical for sovereign and regulated environments.

---

# Directory docker/

`docker/` describes **how code becomes a runtime artifact**.

It contains:  
– Dockerfile  
– entrypoint  

Important:  
– build is deterministic  
– container is minimal  
– security assumptions are enforced  

---

# Directory helm/

`helm/` is the **declarative description of application deployment**.

It contains:  
– Kubernetes Deployment  
– Service  
– HPA  
– NetworkPolicy  
– Pod Security settings  

The Helm chart:  
– contains no application logic  
– reflects runtime policy

---

# Directory k8s/

`k8s/` contains **base and security Kubernetes manifests**.

Purpose:  
– namespace isolation  
– resource quotas  
– security profiles  

This is not application deployment, but the **environment in which it is allowed to operate**.

---

# Directory ci/

`ci/` describes **CI/CD contracts**, not their implementation.

It contains:  
– pipeline entrypoints  
– security policies  
– artifact interfaces  

The actual implementation resides in:  
**ai-secure-ci-cd-platform**

---

# Directory security/

`security/` is the **project’s security artifact hub**.

It contains:  
– threat model  
– SBOM  
– attestations  
– runtime security profiles  

Security is separated so that:  
– it can be audited independently  
– it is not mixed with code  

---

# Directory observability/

`observability/` describes:  
– metrics  
– logs  
– traces  
– dashboards  

This is an observability contract, not runtime data.

---

# Directory scripts/

`scripts/` contains:  
– local utilities  
– validation scripts  
– auxiliary tools  

They do not participate in production runtime.

---

# Directory docs/

`docs/` is the **formal project documentation**.

Each document:  
– addresses a single concern  
– references others  
– does not duplicate code  

Documentation is part of security and governance, not an add-on.

---

# Extension Points

The repository is designed as **part of an ecosystem**.

Extensions occur:  
– via the CI/CD platform  
– via governance repositories  
– via infrastructure repositories  

The `ai-llm-reference-app` itself remains:  
– minimal  
– verifiable  
– controlled

---

# Conclusion

The repository structure:  
– reflects the architecture  
– reinforces security  
– simplifies auditing  

This is a **design document in the form of a file system**.

---

# Purpose of Directories and Files

## README.md
Main entry point of the repository.  
Captures project purpose, responsibility boundaries, and documentation links.  
DevSecOps significance: rapid understanding of architecture, security model, and project maturity.

## LICENSE
Project license.  
Defines legal terms of use and distribution.  
DevSecOps significance: legal transparency of the supply chain and open-source compliance.

## SECURITY.md
Single point for describing the project’s security policy.  
Contains disclosure rules, scope of security checks, and links to security documentation.  
DevSecOps significance: formalization of security posture and vulnerability management process.

## CODEOWNERS
File assigning code and directory owners.  
Defines responsible parties for review and changes.  
DevSecOps significance: change control, reducing risk of unauthorized edits.

## .gitignore
Rules to exclude files from Git.  
Prevents committing temporary, sensitive, and local artifacts.  
DevSecOps significance: secret protection and repository cleanliness.

## .editorconfig
Unified code formatting rules.  
Synchronizes style across IDEs and team members.  
DevSecOps significance: reduces diff noise, ensures predictable reviews and CI.

## .env.example
Example environment variables without secrets.  
Documents required runtime parameters.  
DevSecOps significance: secure configuration management and leak prevention.

## app/
Main application and LLM logic.  
Contains API, model, runtime configuration, and tests.  
DevSecOps significance: clear separation of business logic from infra and security boundaries.

## app/README.md
Документация уровня приложения.  
Описывает запуск, интерфейсы и внутренние зависимости.  
DevSecOps-смысл: снижение bus-factor и ускорение онбординга.

## app/api/
HTTP API слой приложения.  
Точка входа пользовательских запросов к LLM.  
DevSecOps-смысл: контроль поверхности атаки и enforcement input/output policy.

### app/api/main.py
Инициализация приложения и runtime.  
Связывает конфигурацию, роуты и middleware.  
DevSecOps-смысл: единая точка включения security- и observability-хуков.

### app/api/routes.py
Определение API-эндпоинтов.  
Маршрутизирует запросы к бизнес-логике.  
DevSecOps-смысл: явная модель API, удобная для threat modeling.

### app/api/schemas.py
Схемы входных и выходных данных.  
Используются для валидации и сериализации.  
DevSecOps-смысл: строгий input control и снижение риска prompt injection.

### app/api/deps.py
Зависимости и common hooks API.  
Используется для DI, auth, лимитов и контекстов.  
DevSecOps-смысл: централизованное применение security-контролей.

## app/llm/
Реализация reference LLM внутри приложения.  
Содержит все этапы LLM pipeline в явном и читаемом виде.  
DevSecOps-смысл: прозрачность модели, контролируемые attack surfaces.

### app/llm/tokenizer/
Токенизация входного текста.  
Преобразует пользовательский ввод в дискретные токены.  
DevSecOps-смысл: первая линия защиты от некорректного и вредоносного ввода.

### app/llm/tokenizer/vocab.json
Словарь токенов модели.  
Определяет допустимое пространство входных данных.  
DevSecOps-смысл: ограничение input domain и снижение вариативности атак.

### app/llm/tokenizer/tokenizer.py
Логика токенизации и детокенизации.  
Реализует правила разбиения текста.  
DevSecOps-смысл: контроль размера и структуры prompt.

### app/llm/tokenizer/README.md
Документация по токенизации.  
Описывает ограничения и допущения.  
DevSecOps-смысл: упрощение анализа input-related угроз.

### app/llm/embeddings/
Embedding слой модели.  
Преобразует токены в векторное представление.  
DevSecOps-смысл: фиксированная и воспроизводимая математика модели.

### app/llm/embeddings/embedding.py
Реализация embedding-логики.  
Связывает токены и их векторы.  
DevSecOps-смысл: детерминированность и проверяемость вычислений.

### app/llm/embeddings/weights.bin
Веса embedding слоя.  
Является частью model artifact.  
DevSecOps-смысл: объект контроля целостности и supply-chain trust.

### app/llm/embeddings/README.md
Описание embedding слоя.  
Фиксирует архитектурные решения.  
DevSecOps-смысл: аудит модели без чтения кода.

### app/llm/transformer/
Ядро transformer-архитектуры.  
Реализует attention и feed-forward блоки.  
DevSecOps-смысл: изолированный и обозримый compute-контур.

### app/llm/transformer/attention.py
Self-attention механизм.  
Определяет контекстное взаимодействие токенов.  
DevSecOps-смысл: понимание вычислительной сложности и DoS-рисков.

### app/llm/transformer/ffw.py
Feed-forward сеть трансформера.  
Обеспечивает нелинейность модели.  
DevSecOps-смысл: предсказуемая нагрузка и контроль ресурсов.

### app/llm/transformer/decoder.py
Decoder-блок трансформера.  
Комбинирует attention и FFN.  
DevSecOps-смысл: единая точка анализа inference-логики.

### app/llm/transformer/model.py
Сборка полной transformer-модели.  
Определяет архитектуру и порядок слоёв.  
DevSecOps-смысл: прозрачная модель для security review.

### app/llm/decoding/
Этап генерации выходных токенов.  
Определяет стратегию inference и контроль вариативности.  
DevSecOps-смысл: управление детерминизмом, нагрузкой и выходными рисками.

### app/llm/decoding/sampler.py
Реализация sampling-стратегий.  
Управляет randomness и вероятностным выбором токенов.  
DevSecOps-смысл: предотвращение неконтролируемого поведения модели.

### app/llm/decoding/decoder.py
Логика пошагового декодирования.  
Связывает модель и sampling.  
DevSecOps-смысл: контроль inference-loop и DoS-поверхности.

### app/llm/decoding/guards.py
Защитные ограничения decoding-процесса.  
Лимиты длины, шагов и условий остановки.  
DevSecOps-смысл: защита от resource exhaustion и runaway generation.

### app/llm/postprocess/
Постобработка выходного текста модели.  
Последний этап перед возвратом пользователю.  
DevSecOps-смысл: enforcement output policy и data loss prevention.

### app/llm/postprocess/filters.py
Фильтрация нежелательного контента.  
Удаление или блокировка запрещённых паттернов.  
DevSecOps-смысл: снижение репутационных и compliance-рисков.

### app/llm/postprocess/redaction.py
Редакция чувствительных данных.  
Скрытие токенов, секретов и PII.  
DevSecOps-смысл: предотвращение data exfiltration.

### app/llm/postprocess/policy.py
Policy-driven контроль вывода.  
Применение правил и ограничений.  
DevSecOps-смысл: согласование поведения модели с governance.

### app/llm/version.py
Версионирование модели и pipeline.  
Фиксирует API и model version.  
DevSecOps-смысл: трассируемость и воспроизводимость inference.

## app/config/
Runtime-конфигурация приложения.  
Отделена от кода и модели.  
DevSecOps-смысл: безопасное управление параметрами и лимитами.

### app/config/runtime.yaml
Основные runtime-настройки.  
Параметры запуска и поведения.  
DevSecOps-смысл: контролируемый runtime без hardcode.

### app/config/limits.yaml
Лимиты ресурсов и операций.  
Ограничения на запросы и генерацию.  
DevSecOps-смысл: защита от abuse и DoS.

### app/config/logging.yaml
Конфигурация логирования.  
Формат, уровни и sinks логов.  
DevSecOps-смысл: аудит и incident response.

## app/tests/
Тестовый контур приложения.  
Предназначен для unit и security-тестов.  
DevSecOps-смысл: регрессия и контроль изменений.

### app/tests/.gitkeep
Заглушка для сохранения директории в Git.  
Обозначает намеренное наличие тестового слоя.  
DevSecOps-смысл: явное место для security и functional tests.

## models/
Хранилище model artifacts.  
Отделено от application-кода.  
DevSecOps-смысл: контроль supply chain и immutability модели.

### models/v1/
Конкретная версия модели.  
Фиксированный набор весов и метаданных.  
DevSecOps-смысл: воспроизводимость и версионирование inference.

### models/v1/weights.bin
Бинарные веса модели.  
Используются для inference без модификаций.  
DevSecOps-смысл: объект контроля целостности и подписи.

### models/v1/checksum.sha256
Контрольная сумма весов.  
Используется для валидации integrity.  
DevSecOps-смысл: защита от подмены модели.

### models/v1/model-card.md
Model Card для версии модели.  
Описывает назначение, ограничения и риски.  
DevSecOps-смысл: прозрачность и ответственное использование модели.

### models/registry/
Локальный реестр моделей.  
Точка расширения для нескольких версий.  
DevSecOps-смысл: управляемая эволюция моделей.

### models/registry/.gitkeep
Заглушка для фиксации структуры.  
Обозначает намеренный registry слой.  
DevSecOps-смысл: подготовка к model lifecycle management.

## docker/
Docker-артефакты проекта.  
Изолирует runtime от хоста.  
DevSecOps-смысл: воспроизводимая и безопасная сборка.

### docker/app/
Docker-контур приложения.  
Содержит образ LLM API.  
DevSecOps-смысл: единый entrypoint для CI/CD.

### docker/app/Dockerfile
Описание сборки контейнера.  
Фиксирует зависимости и шаги build.  
DevSecOps-смысл: детерминированная и проверяемая сборка.

### docker/app/entrypoint.sh
Скрипт запуска контейнера.  
Инициализирует runtime и проверки.  
DevSecOps-смысл: контроль старта и fail-fast поведение.

### docker/README.md
Документация по контейнеризации.  
Описывает build и runtime assumptions.  
DevSecOps-смысл: корректное использование контейнеров в CI и prod.

## helm/
Helm-уровень деплоя приложения.  
Инкапсулирует Kubernetes-ресурсы и политики.  
DevSecOps-смысл: декларативный, воспроизводимый и проверяемый deployment.

### helm/charts/
Набор Helm-чартов проекта.  
Определяет стандарт развёртывания.  
DevSecOps-смысл: единый deployment blueprint.

### helm/charts/ai-llm-reference-app/
Основной Helm-чарт приложения.  
Описывает все runtime-компоненты.  
DevSecOps-смысл: централизованный контроль архитектуры в k8s.

### helm/charts/ai-llm-reference-app/Chart.yaml
Метаданные Helm-чарта.  
Имя, версия и зависимости.  
DevSecOps-смысл: управляемое версионирование deployment-артефактов.

### helm/charts/ai-llm-reference-app/templates/
Шаблоны Kubernetes-манифестов.  
Рендерятся в runtime-ресурсы.  
DevSecOps-смысл: policy-by-design на уровне инфраструктуры.

### helm/charts/ai-llm-reference-app/templates/deployment.yaml
Deployment манифест приложения.  
Определяет pods, ресурсы и security context.  
DevSecOps-смысл: изоляция и контроль исполнения.

### helm/charts/ai-llm-reference-app/templates/service.yaml
Service для доступа к приложению.  
Экспонирует API внутри кластера.  
DevSecOps-смысл: контролируемая сетевой доступ.

### helm/charts/ai-llm-reference-app/templates/hpa.yaml
Horizontal Pod Autoscaler.  
Масштабирование по метрикам.  
DevSecOps-смысл: защита от перегрузок и DoS.

### helm/charts/ai-llm-reference-app/templates/networkpolicy.yaml
NetworkPolicy для pods.  
Ограничивает сетевые соединения.  
DevSecOps-смысл: zero-trust внутри кластера.

### helm/charts/ai-llm-reference-app/templates/podsecurity.yaml
Pod security контекст.  
Запрещает небезопасные capabilities.  
DevSecOps-смысл: runtime hardening.

### helm/charts/ai-llm-reference-app/templates/_helpers.tpl
Вспомогательные шаблоны Helm.  
Переиспользуемые функции и имена.  
DevSecOps-смысл: единообразие и снижение ошибок.

### helm/charts/ai-llm-reference-app/values.yaml
Базовые значения чарта.  
Дефолтная конфигурация.  
DevSecOps-смысл: безопасные значения по умолчанию.

### helm/values/
Values-файлы окружений.  
Отделены от чарта.  
DevSecOps-смысл: чёткое разделение code и config.

### helm/values/dev.yaml
Настройки dev-окружения.  
Минимальные лимиты и упрощённый режим.  
DevSecOps-смысл: безопасное локальное тестирование.

### helm/values/stage.yaml
Настройки stage-окружения.  
Максимально близки к prod.  
DevSecOps-смысл: валидация перед продом.

### helm/values/prod.yaml
Настройки production.  
Жёсткие лимиты и security-политики.  
DevSecOps-смысл: надёжный и контролируемый runtime.

## k8s/
Низкоуровневые Kubernetes-манифесты и security-базис.  
Используются как фундамент для Helm.  
DevSecOps-смысл: enforced baseline до уровня приложения.

### k8s/base/
Базовые namespace-level ограничения.  
Определяют границы ресурсов.  
DevSecOps-смысл: защита кластера от resource abuse.

### k8s/base/namespace.yaml
Namespace приложения.  
Логическая и security-граница.  
DevSecOps-смысл: изоляция workloads.

### k8s/base/resourcequota.yaml
Квоты ресурсов на namespace.  
Ограничение CPU, memory, objects.  
DevSecOps-смысл: защита от DoS и runaway workloads.

### k8s/base/limitrange.yaml
Лимиты по умолчанию для pods и containers.  
Запрещает запуск без ресурсов.  
DevSecOps-смысл: принудительный resource hygiene.

### k8s/security/
Кластерные и namespace security-политики.  
Runtime enforcement.  
DevSecOps-смысл: hardening execution среды.

### k8s/security/psa.yaml
Pod Security Admission policy.  
Запрещает небезопасные pod-спеки.  
DevSecOps-смысл: prevention вместо detection.

### k8s/security/seccomp.yaml
Seccomp-профиль для контейнеров.  
Ограничивает системные вызовы.  
DevSecOps-смысл: снижение kernel attack surface.

### k8s/security/apparmor.yaml
AppArmor-профиль.  
Контроль доступа к файловой системе и процессам.  
DevSecOps-смысл: runtime confinement.

### k8s/manifests/
Место для дополнительных k8s-манифестов.  
Расширение базовой архитектуры.  
DevSecOps-смысл: controlled extensibility.

### k8s/manifests/.gitkeep
Фиксирует директорию в репозитории.  
Подготовка под расширение.  
DevSecOps-смысл: структурная дисциплина.

## ci/
CI/CD уровень проекта.  
Политики, entrypoints и артефакты.  
DevSecOps-смысл: автоматизированный security-gated pipeline.

### ci/README.md
Описание CI/CD модели проекта.  
Связь с ai-secure-ci-cd-platform.  
DevSecOps-смысл: прозрачность supply chain.

### ci/entrypoints/
Точки входа CI pipeline.  
Разделение стадий.  
DevSecOps-смысл: детерминированные этапы.

### ci/entrypoints/build.yaml
Сборка образов и артефактов.  
Immutable outputs.  
DevSecOps-смысл: воспроизводимая сборка.

### ci/entrypoints/test.yaml
Тестирование кода и политик.  
Fail-fast.  
DevSecOps-смысл: раннее выявление рисков.

### ci/entrypoints/release.yaml
Релиз и публикация артефактов.  
Подписи и attestations.  
DevSecOps-смысл: доверенный выпуск.

### ci/policies/
OPA/Rego политики для LLM и supply chain.  
Policy-as-code.  
DevSecOps-смысл: автоматическое enforcement.

### ci/policies/llm-input.rego
Политики валидации входных запросов.  
Ограничения prompt.  
DevSecOps-смысл: защита от prompt injection.

### ci/policies/llm-output.rego
Политики контроля ответов модели.  
Фильтрация и ограничения.  
DevSecOps-смысл: предотвращение data leakage.

### ci/policies/model-integrity.rego
Политики целостности модели.  
Проверка хэшей и источников.  
DevSecOps-смысл: защита от model tampering.

### ci/artifacts/
Хранилище CI-артефактов.  
SBOM, attestations, metadata.  
DevSecOps-смысл: auditable supply chain.

### ci/artifacts/.gitkeep
Фиксация директории.  
Подготовка под CI outputs.  
DevSecOps-смысл: структурная предсказуемость.

## security/
Централизованный security-контур проекта.  
Threat modeling, supply chain и runtime controls.  
DevSecOps-смысл: безопасность как системный слой.

### security/threat-model/
Модель угроз проекта.  
Формализует attack surfaces и риски.  
DevSecOps-смысл: threat-driven design.

### security/threat-model/threat-model.md
Документ с описанием угроз и допущений.  
Используется для mapping security-контролей.  
DevSecOps-смысл: обоснованная безопасность.

### security/sbom/
Артефакты Software Bill of Materials.  
Для кода и модели.  
DevSecOps-смысл: прозрачность состава.

### security/sbom/.gitkeep
Фиксация директории SBOM.  
Подготовка под автоматическую генерацию.  
DevSecOps-смысл: supply chain readiness.

### security/attestations/
Криптографические attestations.  
Provenance и integrity доказательства.  
DevSecOps-смысл: доверие к артефактам.

### security/attestations/.gitkeep
Фиксация директории attestations.  
Подготовка под CI outputs.  
DevSecOps-смысл: auditable security.

### security/runtime/
Runtime security конфигурации.  
Используются при деплое.  
DevSecOps-смысл: защита в исполнении.

### security/runtime/seccomp.json
Seccomp-профиль контейнера.  
Ограничение системных вызовов.  
DevSecOps-смысл: минимизация kernel attack surface.

### security/runtime/readonly-fs.yaml
Конфигурация read-only файловой системы.  
Запрещает запись в контейнере.  
DevSecOps-смысл: защита от persistence атак.

### security/README.md
Описание security-подхода репозитория.  
Навигация по security-артефактам.  
DevSecOps-смысл: единая точка понимания.

## observability/
Наблюдаемость системы.  
Метрики, логи и трассировки.  
DevSecOps-смысл: контроль поведения и инцидентов.

### observability/metrics/
Метрики приложения и runtime.  
Экспорт в Prometheus.  
DevSecOps-смысл: мониторинг и capacity planning.

### observability/metrics/prometheus.yaml
Конфигурация сбора метрик.  
Определяет scrape targets.  
DevSecOps-смысл: измеримость системы.

### observability/logs/
Сбор и обработка логов.  
Централизованный pipeline.  
DevSecOps-смысл: forensic readiness.

### observability/logs/fluent-bit.yaml
Конфигурация Fluent Bit.  
Парсинг и отправка логов.  
DevSecOps-смысл: надёжный логинг.

### observability/traces/
Distributed tracing.  
Отслеживание запросов.  
DevSecOps-смысл: диагностика latency и аномалий.

### observability/traces/otel.yaml
OpenTelemetry конфигурация.  
Экспорт трейсов.  
DevSecOps-смысл: end-to-end visibility.

### observability/dashboards/
Дашборды наблюдаемости.  
Визуализация метрик и логов.  
DevSecOps-смысл: оперативное принятие решений.

### observability/dashboards/.gitkeep
Фиксация директории дашбордов.  
Подготовка под Grafana.  
DevSecOps-смысл: структурированная observability.

## scripts/
Вспомогательные скрипты для локальной работы и валидации.  
Не участвуют в production runtime.  
DevSecOps-смысл: воспроизводимость и локальная проверка без упрощений.

### scripts/local-run.sh
Локальный запуск приложения.  
Используется для быстрой проверки изменений.  
DevSecOps-смысл: ранняя валидация без обхода security-контуров.

### scripts/kind-up.sh
Подъём локального Kubernetes-кластера (kind).  
Имитация prod-like окружения.  
DevSecOps-смысл: тестирование deployment и security-политик.

### scripts/verify.sh
Проверка целостности и корректности окружения.  
Запуск базовых проверок.  
DevSecOps-смысл: guardrail перед изменениями.

## docs/
Документация проекта.  
Фиксирует архитектурные и security-решения.  
DevSecOps-смысл: design-as-documentation.

### docs/architecture.md
Логическая и runtime-архитектура системы.  
Компоненты и trust boundaries.  
DevSecOps-смысл: обоснование архитектурных решений.

### docs/llm-internals.md
Внутреннее устройство LLM.  
Пайплайн inference.  
DevSecOps-смысл: понимание attack surfaces.

### docs/llm-security.md
Security-модель LLM.  
Угрозы и контроли.  
DevSecOps-смысл: threat-driven security.

### docs/supply-chain.md
Supply chain и CI/CD модель.  
SBOM, attestations, подписи.  
DevSecOps-смысл: доверие к артефактам.

### docs/deployment.md
Модель безопасного деплоя.  
Контейнеры и Kubernetes.  
DevSecOps-смысл: контролируемый runtime.

### docs/repository-structure.md
Объяснение структуры репозитория.  
Навигация и принципы.  
DevSecOps-смысл: intentional design.
