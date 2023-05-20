# Shishka Classifier

## Описание проблемы

В крупных компаниях отдел сервиса (технической поддержки) сталкивается с проблемой неверной классификации обращений, связанных с работой сервисов, необходимых для выполнения должностных обязанностей. Из-за этого операторы тратят значительное время на исправление этих ошибок. Потраченное время приносит компании дополнительные рассходы, а также препятствует своевременному поддержанию работоспособности сервисов со стороны администраторов. 

## Описание стека использованных технологий

Для анализа набора данных (далее - датасета), визуализации и выявления паттернов, а также для создания модели классификации обращений был использован следующий стек технологий:

<img src="/docs/pics/Frame18.png" alt="Python" width="75"/>
Python - это высокоуровневый язык программирования общего назначения с динамической строгой типизацией и автоматическим управлением памятью, ориентированный на повышение производительности разработчика, читаемости кода и его качества, а также на обеспечение переносимости написанных на нём программ.

---

<img src="/docs/pics/Frame17.png" alt="Pandas" width="75"/>
NumPy - это фундаментальная библиотека для математических вычислений, анализа данных и работы с n-мерными масивами, матрицами и формулами. 

---

<img src="/docs/pics/Frame19.png" alt="NumPy" width="75"/>
Pandas - это быстрый, мощный, гибкий и простой в использовании инструмент анализа данных с открытым исходным кодом и манипулирования ими, построенный на основе языка программирования Python.

---

<img src="/docs/pics/Frame9.png" alt="SeaBorn" width="75"/>
Seaborn — это библиотека для создания статистических графиков на Python. Она основывается на matplotlib и тесно взаимодействует со структурами данных pandas.

---

<img src="/docs/pics/Frame8.png" alt="StatsModels" width="75"/>
Statsmodels - это библиотека для статистического анализа данных на языке Python. Она предоставляет широкий спектр функций для выполнения различных задач, связанных с анализом данных, включая регрессионный анализ, прогнозирование временных рядов, анализ дисперсии и многое другое.

---

<img src="/docs/pics/Frame7.png" alt="ImbLearn" width="75"/>
Imbalanced-learn (imblearn) - это библиотека Python, которая предоставляет инструменты для работы с данными, которые имеют дисбаланс классов. Она предоставляет различные методы для балансировки классов, такие как SMOTE, ADASYN, RUSBoost, EasyEnsemble и другие. Библиотека также содержит инструменты для оценки качества модели, такие как ROC-AUC и Precision-Recall.

---

<img src="/docs/pics/Frame11.png" alt="CatBoost" width="75"/>
CatBoost - это библиотека машинного обучения, разработанная в России компанией Yandex. Она использует алгоритмы градиентного бустинга и работает с категориальными и числовыми признаками. CatBoost имеет ряд преимуществ перед другими библиотеками машинного обучения.


## Поиск фич и выявление паттернов 

В результате [анализа датасета](parse.ipynb), были выявлены зависимости, аномалии, фичи и паттерны, для обработки данных и предстказывания требуемых значений.
Мы обнаружили зависимости типа классификации обращения от:

- Фактического времени, затраченного на выполнение обращения ```Время затраченное на выполнение обращения = Дата закрытия - Дата обращения```. Чем меньше времени потрачено на закрытие обращения, тем больше вероятность того, что данное обращение является инцидентом;
- Времени, которое выделено на обработку обращения ```Время на выполнение = Крайний срок - Дата обращения```. Чем меньше времени потрачено на закрытие обращения, тем больше вероятность того, что данное обращение является инцидентом.

Паттерны, которые мы выделили, во время анализа датасета:

- Если статус обращение "Отменен", то тип переквалификации 0, то есть тип обращения не меняется;
- Если содердание заявки "Заявка на предоставление и отзыв прав доступа к ресурсам", то это общение является запросом.

## Описание модели

Для создания [модели классификатора](classifier.ipynb), мы использовали библиотеку машинного обучения CatBoost. Это отчественная библиотека, разработанная компанией Яндекс в 2022 году. 

Мы задали определенные гиперпараметры:

- Грубина 8;
- Коэффицент обучения 0.01;
- Количество итераций 1500;
- Остановка в случае 300 безрезультатных итераций;
- Метрика для оценки точности AUC.

Итоговая точность, на тренировачном датасете (из которого 20% данных были представленны как тестовый датасет), которой нам удалось достичь: ```Score = 0.92``` или 92%.

## Реализация UX/UI интерфейса

Для реализации пользовательского интерфеса, отражающего примерный вариант использования модели, мы использовали:

<img src="/docs/pics/Frame6.png" alt="FastAPI" width="75"/>
FastAPI - это фреймворк для создания веб-приложений на языке Python, который позволяет создавать быстрые и масштабируемые API. Он основан на принципах RESTful API, что делает его удобным для разработки веб-сервисов.
FastAPI использует асинхронное программирование и может работать с различными базами данных, такими как PostgreSQL, MySQL, SQLite и другими. Он также поддерживает интеграцию с популярными фреймворками, такими как Django, Flask и Pyramid.
Одним из главных преимуществ FastAPI является его простота в использовании. Он имеет понятный и лаконичный API, который легко понять и использовать. Кроме того, FastAPI имеет встроенную поддержку документации, что упрощает разработку и сопровождение веб-приложения.
расскажи что такое react

---

<img src="/docs/pics/Frame14.png" alt="React" width="75"/>
React - это библиотека JavaScript для создания пользовательских интерфейсов, которая позволяет создавать интерактивные и динамические веб-приложения. Она основана на концепции компонентов, которые представляют собой блоки кода, которые могут быть повторно использованы и переиспользованы в разных частях приложения. React позволяет создавать сложные интерфейсы, используя компоненты, которые взаимодействуют друг с другом и могут изменять состояние приложения в зависимости от действий пользователя.

---

Более подробное описание реализации интерфеса веб-приложения можно найти [здесь](https://github.com/BiTronicsDev/user_issue_gui) 
