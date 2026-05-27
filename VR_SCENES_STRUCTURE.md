# VR project: структура и логика сцен

Этот файл описывает структуру и работу четырех ключевых сцен WebXR:
- examples/webxr_vr_blockchain_architecture.html
- examples/webxr_vr_block_structure_integrity.html
- examples/webxr_vr_keys_access_decision.html
- examples/webxr_vr_consensus_arena.html

Ниже кратко собраны общие паттерны и специфическая логика каждой сцены.

## Общая архитектура сцен

Все четыре файла устроены одинаково на уровне каркаса:

1) HTML + HUD
- В каждой сцене есть HUD (#hud) с кнопками и показателями состояния.
- Есть кнопка скрытия панели (Hide/Show Panel) и быстрый хоткей H.
- Верстка и стили HUD описаны прямо в самом HTML (inline CSS).

2) Импорт three.js
- Используется importmap:
  - "three": ../build/three.module.js
  - "three/addons/": ./jsm/
- Внутри модуля подключаются OrbitControls, VRButton, XRControllerModelFactory.

3) Основной цикл
- init(): создание сцены, камеры, рендера, света, пола/сетки, декоративного окружения.
- setupVRControllers(): подключение XR контроллеров и лучей (ray).
- setupVRPanel()/setupVRControlPanel(): создание VR-панели управления в 3D.
- bindEvents(): обработчики кнопок HUD, клавиш и ресайза.
- animate(): главный цикл с renderer.setAnimationLoop или renderer.render.

4) Взаимодействие
- VR-лучи используются через Raycaster, список интерактивных объектов хранится в vr.interactiveTargets.
- Все интерактивные объекты получают userData.onActivate.
- Поддерживаются хаптики контроллеров (gamepad.hapticActuators).

5) Динамические ярлыки
- Все текстовые таблички в сцене реализованы через canvas + CanvasTexture.
- Функции createWorldLabel/createVrLabel/refreshWorldPanelLabels обновляют подписи.

6) История и timeline
- В каждой сцене есть history-снимки состояния.
- Таймлайн можно прокручивать на HUD и на VR-панели (слайдер).
- При переключении в прошлое логика уходит из Live режима.

7) Аудио
- Каждая сцена создает AudioListener и простые буферы звука.
- Аудио активируется после пользовательского взаимодействия (unlock/resume AudioContext).

## Scene 1: Architecture Comparison
Файл: examples/webxr_vr_blockchain_architecture.html

Суть: сравнение централизованной и децентрализованной архитектуры сети.

Ключевые элементы:
- Две отдельные группы города: centralized.group и decentralized.group.
- Узлы (nodes) и маршруты (routes) с движущимися "пакетами".
- Режимы:
  - Centralized (Bank City): центральный сервер + клиенты.
  - Decentralized (Blockchain City): кольцо узлов и сетка связей.
- Инциденты:
  - DDoS (ddos), пожар (fire), разрыв сегмента (segment).
- Логика:
  - toggleCentralServer(), disableRandomNode(), switchMode().
  - updateNetworkState() пересчитывает статусы узлов, маршрутов и UI.

## Scene 2: Block Integrity Lab
Файл: examples/webxr_vr_block_structure_integrity.html

Суть: визуальная демонстрация целостности цепочки блоков.

Ключевые элементы:
- Цепочка блоков (blockCount) с prevHash и hash.
- computeHash(): упрощенный FNV-подобный хэш для демонстрации.
- Выбор блока, tamper/restore/remint:
  - tamperSelectedTransaction() ломает цепочку.
  - restoreSelectedTransaction() возвращает оригинальную транзакцию.
  - remintChain() пересчитывает хэши начиная с сломанного блока.
- firstBrokenIndex показывает место разрыва.
- Инспектор сравнивает expected prevHash и actual prevHash.
- Tutorial на 4 шага ведет пользователя через сценарий.
- VR-панель включает:
  - выбор блоков, tamper/restore/remint/reset;
  - TX Pad для сборки транзакции;
  - timeline слайдер.

## Scene 3: Cryptographic Keys
Файл: examples/webxr_vr_keys_access_decision.html

Суть: пятишаговая проверка доступа по ключам в режиме owner-only.

Ключевые элементы:
- Три актера: Alice (owner), Bob, Eve.
- Vault policy: только владелец может открыть доступ.
- Pipeline из 5 шагов:
  1) формат ключа
  2) регистрация ключа
  3) соответствие владельцу (holder)
  4) проверка owner-only
  5) подпись с nonce
- generateNonce(), pseudoHash(), buildSignature() формируют подпись.
- После нескольких нарушений включается lockout.
- Визуал:
  - дверь хранилища, барьер, луч доступа;
  - подсветка терминалов акторов.
- VR-панель дублирует кнопки HUD и метрики.

## Scene 4: Consensus Arena
Файл: examples/webxr_vr_consensus_arena.html

Суть: сравнительный симулятор Proof of Work vs Proof of Stake.

Ключевые элементы:
- Режимы pow/pos с конфигами (latency, energy, compute, failureChance).
- Профили: Learning и Stress-Test.
- Валидаторы с stake и hash power.
- Этапы пайплайна:
  1) proposer
  2) gossip/vote
  3) finalization
- Возможны partition и fork в PoW.
- Метрики:
  - round metrics, rewards/slashing, throughput.
- VR-панель: переключение режима, старт раунда, профиль, partition, auto-run.

## Используемая структура проекта (из этих сцен)

- build/three.module.js: базовая сборка three.js.
- examples/jsm/: модули add-ons (OrbitControls, VRButton, XRControllerModelFactory).
- examples/main.css: общий стиль для примеров (дополняется inline CSS в каждой сцене).
- Все сцены живут в examples/ и являются самостоятельными HTML.

## Как читать и расширять

1) Сцена = один HTML файл, внутри все: UI, логика, 3D, VR.
2) Базовый каркас одинаковый: init() + animate() + VR interaction.
3) Для новой сцены проще всего копировать структуру одной из существующих и менять:
   - state
   - сборку 3D объектов
   - UI и VR-панель
   - правила симуляции и метрики
