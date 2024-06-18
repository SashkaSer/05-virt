# Домашнее задание к занятию "`ELK`" - `Введение в виртуализацию`

### Задание 1
К сожалению мой пробный период в Я.Облаке закончился, но есть ВМ у другого провайдера. В принципе с облаками рабоать умею. Вдсиной пользуюсь уже больше года, дешево и сердито.

![elastic](https://github.com/SashkaSer/05-virt/blob/main/img/vdsina.png)`

### Задание 2
Выберите один из вариантов платформы в зависимости от задачи. Здесь нет однозначно верного ответа так как все зависит от конкретных условий: финансирование, компетенции специалистов, удобство использования, надежность, требования ИБ и законодательства, фазы луны.

Тип платформы:

* физические сервера;
* паравиртуализация;
* виртуализация уровня ОС;

Задачи:

* высоконагруженная база данных MySql, критичная к отказу;
* различные web-приложения;
* Windows-системы для использования бухгалтерским отделом;
* системы, выполняющие высокопроизводительные расчёты на GPU.  
Объясните критерии выбора платформы в каждом случае.  


Высоконагруженная база данных MySql, критичная к отказу. Я бы использовал паравиртуализацию на основе Hyper-V, есть живая миграция машин между нодами. Диски в основном живут на СХД, которая более надеждная, чем сервера. Можно полностью бэкапировать машины через Microsoft System Center Data Protection Manager к примеру на ленты. Но есть нюанс, если на железном сервере будут жрушщие сеть машины, то может быть просадка по каналу связи. 

Различные web-приложения. Для них больше подойдет виртуализация уровня ОС, так как приложения весьма легковесные и микросервисные. Web-приложения легко заворачиваются в контейнеры. Если использовать паравиртуализацию, то потребуются доп ресурсы для работы гостевой ОС.

Windows-системы для использования бухгалтерским отделом. Паравиртуализацию на основе Hyper-V, легко админить.

Системы, выполняющие высокопроизводительные расчёты на GPU. Только железные сервера. Насколько я помню есть сложности с пробросом GPU в ВМ. Да и и прослойка в виде гипервизора будет замедлять работу.

### Задание 3
Выберите подходящую систему управления виртуализацией для предложенного сценария. Опишите ваш выбор.

Сценарии:

1. 100 виртуальных машин на базе Linux и Windows, общие задачи, нет особых требований. Преимущественно Windows based-инфраструктура, требуется реализация программных балансировщиков нагрузки, репликации данных и автоматизированного механизма создания резервных копий.
2. Требуется наиболее производительное бесплатное open source-решение для виртуализации небольшой (20-30 серверов) инфраструктуры на базе Linux и Windows виртуальных машин.
3. Необходимо бесплатное, максимально совместимое и производительное решение для виртуализации Windows-инфраструктуры.
4. Необходимо рабочее окружение для тестирования программного продукта на нескольких дистрибутивах Linux.

1. Hyper-V. Если преимущественно Win инфраструктура, админы умеют работать с Win. Для управления использовать SCVMM, нарезать права пользователям в AD и они сами смогут создавать ВМ и управлять ими. Резервные копии делать при помощи DPM, мониторинг SCOM.
2. KVM. Достаточно прост для инженеров. Для 20-30 машин в целом подойдет.
3. Xen. Он кросплатформенный и достаточно стабилен в работе.
4. Если рабочее окружение на одной машине и им пользуется один человек, то можно VirtualBox. Можно так же использовать KVM. В целом и Hyper-V тоже подойдет. Вопрос в личных предпочтениях прошлом опыте работы с гипервизорами. 

### Задание 4
Опишите возможные проблемы и недостатки гетерогенной среды виртуализации (использования нескольких систем управления виртуализацией одновременно) и что необходимо сделать для минимизации этих рисков и проблем. Если бы у вас был выбор, создавали бы вы гетерогенную среду или нет?

Проблемы:
* Нужно держать несколько команд инженеров под каждое решение
* Проблемы с бекапированием, мониторингом, накладные расходы на автоматизацию и прочее.
* Накладные расходы на покупку лицензий и поддежки
* В зависимости от вендора гипервизора могут быть проблемы с подбором оборудования

Что можно сделать? Избавиться от гетерогенности и перевести все на одно решение. При планировании новых инсталяций облаков отказаться от гетерогенности. Если избавиться от гетерогенности нельзя, то нужны сильные команды для поддержки.

Я бы не использовал гетерогенную среду.


