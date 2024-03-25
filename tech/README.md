# Техническая документация

В этом разделе описана техническая документация, основные правила написания кода 
и наш общий стиль написания, которого мы все придерживаемся во время разработки

## Навигация

<!-- TOC -->
* [Техническая документация](#техническая-документация)
  * [Навигация](#навигация)
  * [Перед ознакомлением](#перед-ознакомлением)
  * [Правила написания кода](#правила-написания-кода)
    * [Общие правила и концепции](#общие-правила-и-концепции)
    * [Оформление кода](#оформление-кода)
      * [1. Комментирование кода](#1-комментирование-кода)
      * [2. Пиши документационные комментарии к методам](#2-пиши-документационные-комментарии-к-методам)
      * [3. Типизация входных и выходных параметров](#3-типизация-входных-и-выходных-параметров)
      * [4. Читаемые названия переменных и методов](#4-читаемые-названия-переменных-и-методов)
      * [5. Методы всегда должны что-то возвращать](#5-методы-всегда-должны-что-то-возвращать)
      * [6. Ранний возврат из функции](#6-ранний-возврат-из-функции)
      * [7. Документация к API](#7-документация-к-api)
        * [7.1 Как писать документацию к API](#71-как-писать-документацию-к-api)
    * [Структура кода](#структура-кода)
      * [Laravel](#laravel)
      * [Yii2](#yii2)
      * [Front (Vue)](#front-vue)
<!-- TOC -->

---

## Перед ознакомлением

Эта документация писалась разными командами, которые работают с разными фреймворками и разным стеком.
Поэтому в этом разделе могут встречаться различные специфичные примеры кода на Yii2, Laravel, ванильном PHP.

> Важно понять, что описанная документация в этом документе - это общие правила и практики которые не привязаны к конкретной технологии

> Поэтому если где-то в примере кода указан тип возвращаемого значение объект Yii2 - ЭТО НЕ ЗНАЧИТ что эти правила не применимы к Laravel, Symfony или другому фреймворку

> Раздел все еще дописывается. Наберитесь терпения

## Правила написания кода

### Общие правила и концепции

Несмотря на то что за долгое время разработки мы выработали удобную для каждого разработчика методологию написания кода,
никто не отменял соблюдение основных правил и концепций.

В своем коде мы стараемся придерживаться следующих концептов:

- [PHP Standards Recommendations (@blankbuffoon)](https://github.com/BlankBuffoon/PSRRus)

> Раздел дорабатывается

### Оформление кода

Базовые правила, которым нужно следовать при написании **ЛЮБОГО КОДА**:

#### 1. Комментирование кода

Это помогает **Вам**, в первую очередь, быстрее ориентироваться в коде. Помогает вспомнить через время, что происходит в методе. 
А так же помогает другим разработчикам проще разбираться в Вашем коде. Не нужно комментировать всё подряд, достаточно каких-то важных моментов.

Например:
- Важная переменная для метода - напиши что в ней лежит
- Два вложенных цикла foreach друг в друга - напиши что там происходит, внутри для действий оставь коммент
- Даже простое приравнивание может быть важным - если считаешь, что какая-то незначительная вещь играет важную роль - напиши коммент

#### 2. Пиши документационные комментарии к методам

**Пример:**

```php
<?php

    /**
     * Получает отфильтрованный список товаров на основе модели $model.
     *
     * @param Product $model Модель товара
     * @return Request запрос с необходимыми параметрами 
     */
    private function getFilteredProducts(Product $model, Request $request): array
    {
        // какой-то код

        return $products;
    }
```

В такой комментарий должны входить:
- Описание метода - что он делает, кому он делает, зачем он делает. Не стесняйся описывать, слова бесплатные. 
Особенно важно писать описание, если ты сам(-а) написал(-а) метод
- Входные и выходные параметры - их типы, описание

Будет хорошо, если по ходу работы с кодом вы будете писать такие комментарии даже к тем методам, которые писали не вы (но это не критично). 
Если встретили какой-то сложный или непонятный метод и разобрались в нем - напишите описание, что делает метод, для потомков.

#### 3. Типизация входных и выходных параметров

Особенно важно для новых методов, которые вы пишите. Пишешь метод - пиши типизацию. 
Переписываешь старый метод - постарайся написать типизацию (это не всегда возможно, но я в тебя верю!). Пример выше.

#### 4. Читаемые названия переменных и методов

- В переменной лежит массив с параметрами - $parametrs
- В переменной лежит шаблон для excel-файла - $excelTemplate
- Метод получает отфильтрованный список товаров - getFilteredProducts
- Переменная с количеством пользователей - $userCount
- Переменная со списком email-адресов - $emailList
- Метод для отправки сообщения пользователю - sendMessageToUser
- Переменная с текущей датой - $currentDate
- Метод для расчета общей суммы заказа - calculateTotalOrderAmount
- Переменная с информацией о профиле пользователя - $userProfileInfo
- Метод для проверки прав доступа - checkAccessRights
- Переменная с результатами поиска - $searchResults
- Метод для обновления статуса заказа - updateOrderStatus
- Переменная для хранения настроек конфигурации - $configSettings
- Переменная хранит экземпляр модели FabricatorProduct - $fabricatorProductModel

#### 5. Методы всегда должны что-то возвращать

Методы всегда должны что-то возвращать. Это могут быть различные типы данных:

1. Базовые типы данных:
    - Целые числа (int),
    - Строки (string),
    - Логические значения (bool),
    - Вещественные числа (float).

2. Сложные типы:
    - Массивы (array),
    - Объекты (object).

3. Специальные значения:
    - null, когда метод не может вернуть какое-либо конкретное значение или результат операции не определен.

4. Экземпляры классов:
    - Экземпляры пользовательских классов, включая модели данных, компоненты, помощники и другие объекты, определенные в приложении или фреймворке.

5. Результаты запросов к базе данных _(специфично для фреймворка)_:
    - Экземпляры ActiveRecord, представляющие строки из базы данных,
    - Массивы экземпляров ActiveRecord,
    - Объекты DataProvider, используемые для постраничного вывода и фильтрации данных.

6. HTTP-ответы:
    - Объекты Response, предназначенные для отправки HTTP-ответов клиенту, включая статус ответа, заголовки и тело ответа.

7. Исключения:
    - Методы могут генерировать исключения (throw new Exception), которые должны быть перехвачены в вызывающем коде.

8. Специфические значения фреймворка:
    - ActiveQuery для построения и выполнения запросов к базе данных,
    - this для обеспечения цепочки вызовов методов.

Вот несколько примеров что можно возвращать:

```php
<?php

// Базовые типы данных

public function calculateSum(int $a, int $b): int {
    return $a + $b;
}

// Сложные типы

public function getUserData(int $userId): array {
    return User::find()->where(['id' => $userId])->asArray()->one();
}

// Специальные значения

public function findModel(int $id): ?FabricatorProductImExport {
    $fabricatorProductImExportModel = FabricatorProductImExport::findOne($id);
    if ($fabricatorProductImExportModel !== null) {
        return $fabricatorProductImExportModel;
    }

    return null; // или просто `return;`
}

// Экземпляры классов

public function createNewUser(array $userData): User {
    $user = new User();
    $user->attributes = $userData;
    $user->save();
    return $user;
}

// HTTP-ответы

public function actionDownloadFile($filePath) {
    Yii::$app->response->sendFile($filePath);
}

// Исключения

public function checkPermission($user, $permission): void {
    if (!$user->hasPermission($permission)) {
        throw new ForbiddenHttpException('You do not have permission to perform this action.');
    }
}

// Использование DataProvider для постраничного вывода

public function searchUsers($params): ActiveDataProvider {
    $query = User::find();
    // Конфигурация запроса на основе $params
    return new ActiveDataProvider([
        'query' => $query,
        'pagination' => [
            'pageSize' => 20,
        ],
    ]);
}

// Возвращение boolean в результате выполнения операции

public function deleteUser($id): bool {
    $user = User::findOne($id);
    if ($user !== null) {
        return $user->delete() > 0;
    }
    return false;
}

// Возвращение объекта Response для редиректа

public function redirectToHome(): Response {
    return Yii::$app->response->redirect(Url::to(['/site/index']));
}

// Возвращение строки (например, JSON)

public function getUserJson($id): string {
    $user = User::findOne($id);
    return Json::encode($user);
}

```

#### 6. Ранний возврат из функции

Правило раннего возврата из функции (early return) является популярным подходом в программировании, который улучшает читаемость кода, уменьшая его вложенность и делая его более понятным. Этот подход заключается в том, что вместо использования глубоких условных вложенностей (if-else структур) функция возвращает значение как можно раньше, как только выполнены определённые условия.

**Пример без раннего возврата**
```php
<?php

function calculateDiscount($customer) {
    if ($customer->isPremium()) {
        if ($customer->years > 5) {
            return 0.1; // 10% скидка
        } else {
            return 0.05; // 5% скидка
        }
    } else {
        return 0; // Нет скидки
    }
}
```

**Пример с ранним возвратом**
```php
<?php

function calculateDiscount($customer) {
    if (!$customer->isPremium()) {
        return 0; // Ранний возврат, нет скидки
    }
    
    if ($customer->years > 5) {
        return 0.1; // Ранний возврат, 10% скидка
    }
    
    return 0.05; // Ранний возврат по умолчанию, 5% скидка
}
```
Во втором примере код стал более линейным и понятным. Вместо вложенных условий используются ранние возвраты, которые сразу же показывают условия, при которых функция завершает свою работу.

**Проверка доступа пользователя**

**Пример без раннего возврата**
```php
<?php

function checkAccess($user, $permission) {
    if ($user->hasRole('admin')) {
        return true; // Администраторам разрешен любой доступ
    } else {
        if ($user->hasPermission($permission)) {
            return true; // Пользователю разрешен доступ
        } else {
            return false; // Доступ запрещен
        }
    }
}
```

**Пример с ранним возвратом**
```php
<?php

function checkAccess($user, $permission) {
    if ($user->hasRole('admin')) {
        return true; // Ранний возврат для администраторов
    }
    
    if ($user->hasPermission($permission)) {
        return true; // Ранний возврат, если пользователь имеет разрешение
    }
    
    return false; // Ранний возврат по умолчанию, доступ запрещен
}
```

**Валидация данных формы**

**Пример без раннего возврата**
```php
<?php

function validateForm($data) {
    $errors = [];
    if (!empty($data['email'])) {
        if (!filter_var($data['email'], FILTER_VALIDATE_EMAIL)) {
            $errors['email'] = 'Invalid email format';
        }
    } else {
        $errors['email'] = 'Email is required';
    }

    if (!empty($data['password'])) {
        if (strlen($data['password']) < 8) {
            $errors['password'] = 'Password must be at least 8 characters';
        }
    } else {
        $errors['password'] = 'Password is required';
    }

    return $errors;
}
```

**Пример с ранним возвратом**
```php
<?php

function validateForm($data) {
    $errors = [];

    if (empty($data['email'])) {
        $errors['email'] = 'Email is required';
        return $errors; // Ранний возврат, если email отсутствует
    }
    
    if (!filter_var($data['email'], FILTER_VALIDATE_EMAIL)) {
        $errors['email'] = 'Invalid email format';
        return $errors; // Ранний возврат, если email невалиден
    }

    if (empty($data['password'])) {
        $errors['password'] = 'Password is required';
        return $errors; // Ранний возврат, если пароль отсутствует
    }

    if (strlen($data['password']) < 8) {
        $errors['password'] = 'Password must be at least 8 characters';
        // Ранний возврат не используется, если это последняя проверка
    }

    return $errors;
}
```
Во втором примере каждой проверки код стал более прямолинейным и легко читаемым. Ранние возвраты позволяют сразу же прервать выполнение функции, если выполняется определённое условие, упрощая тем самым логику валидации и уменьшая вложенность.

**Пример из нашего проекта**

**Пример без раннего возврата**
```php
/**
 * Получает отфильтрованный список товаров на основе модели $model.
 *
 * @param FabricatorProductInfoModelExport $model Модель для экспорта
 * @return FabricatorProduct Массив отфильтрованных товаров
 */
private function getFilteredProducts(FabricatorProductInfoModelExport $model, array $queryParamsFilter): array
{
    $products = [];

    if (array_key_exists("uuids", $queryParamsFilter)) {
        $uuids = $queryParamsFilter['uuids'];
        $productQuery = FabricatorProduct::find()
            ->where(['fabricator_id' => $queryParamsFilter['fabricator_id']]);

        if (count($uuids) > 0) {
            $productQuery->andWhere(['uuid' => $uuids]);
        }

        $products = $productQuery->all();
    } else {
        $params = [
            'sort' => 'created_at',
            'filter' => $queryParamsFilter,
            'per-page' => 0,
        ];

        $searchModel = new FabricatorProductFilter();
        $searchModel->fabricator_id = $queryParamsFilter['fabricator_id'];
        $dataProvider = $searchModel->search($params);
        $products = $dataProvider->getModels();
    }

    return $products;
}
```

**Пример с ранним возвратом**
```php
<?php
/**
 * Получает отфильтрованный список товаров на основе модели $model.
 *
 * @param FabricatorProductInfoModelExport $model Модель для экспорта
 * @return FabricatorProduct Массив отфильтрованных товаров
 */
private function getFilteredProducts(FabricatorProductInfoModelExport $model, array $queryParamsFilter): array
{
    if (array_key_exists("uuids", $queryParamsFilter)) {
        $uuids = $queryParamsFilter['uuids'];
        $productQuery = FabricatorProduct::find()
            ->where(['fabricator_id' => $queryParamsFilter['fabricator_id']]);

        if (count($uuids) > 0) {
            $productQuery->andWhere(['uuid' => $uuids]);
        }

        return $productQuery->all();
    } else {
        $params = [
            'sort' => 'created_at',
            'filter' => $queryParamsFilter,
            'per-page' => 0,
        ];

        $searchModel = new FabricatorProductFilter();
        $searchModel->fabricator_id = $queryParamsFilter['fabricator_id'];
        $dataProvider = $searchModel->search($params);
        return $dataProvider->getModels();
    }
}
```

В этом примере, вместо создания пустого массива $products в начале и заполнения его в разных частях условного блока, мы немедленно возвращаем результаты, как только они становятся известны. Это делает код более читаемым и линейным, так как уменьшается вложенность блоков кода и сокращается общее количество строк кода. Также это упрощает понимание потока выполнения метода, поскольку каждый блок условий занимается только одной задачей, и результаты этих задач возвращаются как можно скорее.

#### 7. Документация к API

Документацию к API мы пишем для всех методов, к которым обращаемся через API.

В основном это разные action-ы, методы контроллеров, REST API контроллеры, и т.д. Если Вы пишете вспомогательный метод (например, какой-то фильтр данных, сортировка и др.) - к таким методам не нужно писать документацию API.

- Пишешь метод, к которому будешь обращаться с фронтенда - пиши swagger
- Пишешь метод, который будет сортировать данные в массиве для какой-то генерации - не пиши swagger
- Пишешь метод, которому будешь обращаться по API - пиши swagger

##### 7.1 Как писать документацию к API

В каждой команде мы пишем документацию по-разному. Где-то мы вручную пишем спецификации `@OpenAPI`. Где-то подключаем библиотеки которые генерируют документацию в зависимости от описанного PHPDoc.

Зачастую, мы стараемся описывать правила написания документации к проекту сразу внутри раздела его документации (например в confluence), или внутри его репозитория.

> С тем как описывать документацию к API лучше обратиться к своему Лиду, или посмотреть в репозиторий/доку самого проекта

### Структура кода

Мы стараемся выносить логику в соответствующие для нее места. На текущий момент, разделение логики и принцип разделения ответственности кода - один из важнейших для нас принципов.

Структуризация кода напрямую зависит от используемой технологии, но на данные момент мы точно можем выделить следующие принципы:

#### Laravel

> Скоро напишу. Честно. @blankbuffoon (25.03.2024)

#### Yii2

> Скоро напишу. Честно. @blankbuffoon (25.03.2024)

#### Front (Vue)

> Скоро напишу. Честно. @blankbuffoon (25.03.2024)
