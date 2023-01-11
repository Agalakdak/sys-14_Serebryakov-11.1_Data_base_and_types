# Домашнее задание к занятию 11.1. «Базы данных, их типы» студента "Серебряков Руслан"

### Задание 1. СУБД

### Кейс
Крупная строительная компания, которая также занимается проектированием и девелопментом, решила создать 
правильную архитектуру для работы с данными. Ниже представлены задачи, которые необходимо решить для
каждой предметной области. 

Какие типы СУБД, на ваш взгляд, лучше всего подойдут для решения этих задач и почему? 
 
1.1. Бюджетирование проектов с дальнейшим формированием финансовых аналитических отчётов и прогнозирования рисков.
СУБД должна гарантировать целостность и чёткую структуру данных.

1.1.* Хеширование стало занимать длительно время, какое API можно использовать для ускорения работы? 

1.2. Под каждый девелоперский проект создаётся отдельный лендинг, и все данные по лидам стекаются в CRM к 
маркетологам и менеджерам по продажам. Какой тип СУБД лучше использовать для лендингов и для CRM? 
СУБД должны быть гибкими и быстрыми.

1.2.* Можно ли эту задачу закрыть одной СУБД? И если да, то какой именно СУБД и какой реализацией?

1.3. Отдел контроля качества решил создать базу по корпоративным нормам и правилам, обучающему материалу 
и так далее, сформированную согласно структуре компании. СУБД должна иметь простую и понятную структуру.

1.3.* Можно ли под эту задачу использовать уже существующую СУБД из задач выше и если да, то как лучше это 
реализовать?

1.4. Департамент логистики нуждается в решении задач по быстрому формированию маршрутов доставки материалов 
по объектам и распределению курьеров по маршрутам с доставкой документов. СУБД должна уметь быстро работать
со связями.

1.4.* Можно ли к этой СУБД подключить отдел закупок или для них лучше сформировать свою СУБД в связке с СУБД 
логистов?

1.5.* Можно ли все перечисленные выше задачи решить, используя одну СУБД? Если да, то какую именно?

*Приведите ответ в свободной форме.*

---

1.1 Обычная SQL бд или PostgreSQL т.к. это устойчивая структура и здесь требуется дальнейшее формирование финансовых аналитических отчетов.
1.1* Возможно MongoDB API

1.2 Если я правильно понял задачу, то я думаю, что лучше всего подойдёт NoSQL БД которая будет организована по типу Graph
1.2*  

1.3 Подойдёт обычная реляционная база данных. При условии, что к ней будет дописано приложение. Иначе - скорее всего документо-ориентированная бд подойдёт т.к. данные в ней хранятся в виде документов. 
1.3*Да, SQL или PostgreSQL, как конкретно реализовать ... Я могу сказать только, что БД должна представлять собой структуру типа Document.

1.4 Я думаю, что бд типа Graph подойдут для этой задачи. Т.к. они ~~ запутанные, а я тут как раз запутался https://www.meme-arsenal.com/memes/d707db09206cb8f470ac1a432adf6c7e.jpg ~~ используют структуру графов для семантических запросов.
Данные хранятся в виде узлов, ребер и свойст. Это подходит для данной задачи.

1.5* СУБД с открытым исходным кодом, на сколько я знаю MongoDB имеет открытый исходный код и в теории туда можно "звезти" "любой" желаемый функционал.


---
---


### Задание 2. Транзакции

2.1. Пользователь пополняет баланс счёта телефона, распишите пошагово, какие действия должны произойти для того, чтобы 
транзакция завершилась успешно. Ориентируйтесь на шесть действий.

2.1.* Какие действия должны произойти, если пополнение счёта телефона происходило бы через автоплатёж?

*Приведите ответ в свободной форме.*

---

1. Пользователь проводит инициацию запроса на пополнение баланса (предположим, что пользователь хочет пополнить баланс телефона через сбербанк).
  а) Открывает приложение
  б) Вводи пароль
  в) Выбирает нужную опцию
  г) Вводит номер
  д) Вводит сумму для пополнения
  е) Всё проверяет и нажимает кнопку "пополнить"
2. Сигнал по сети "идёт" к ближайшей телекоммуникационной вышке(далее сокращенно ТВ).
3. От ТВ сигнал идёт ... скорее всего на сервер сбера.
4. Сбер получает запрос и обрабатывает его.
  а) БД получает запрос из сети.
  б) БД производит поиск пользователя -> находит его
  в) Проверяет его баланс -> если баланс меньше чем нужно, то отправляет сообщение об ошибке ~~ типа  ~~ "Денег нет :(" ~~ иначе переходит к следующему пункту 
  г) Отправляет запрос оператору связи о переводе денег на счёт
5. Оператор связи получает запрос и обрабатывает его.
  а) БД получает запрос
  б) Производит поиск пользователя -> пользователь найден (иначе возвращает сообщение об ошибке)
  в) "Смотрит" его баланс и изменяет согласно запросу который пришел из сбера.
  г) Отправляет пользователю сообщение об пополнении счета.
6. Пользователь получает сообщение от сбера, от мегафона, о том, что операция завершена успешно. 

=) 

---
---

### Задание 3. SQL vs NoSQL

3.1. Напишите пять преимуществ SQL-систем по отношению к NoSQL. 

3.1.* Какие, на ваш взгляд, преимущества у NewSQL систем перед SQL и NoSQL.

*Приведите ответ в свободной форме.*

---

3.1 SQL системы это обычные реляционные базы данных они обладают следующими преимуществами
1) Они стандартны т.е. я думаю, что есть большое количество инструментов для работы с реляционными БД.
2) Обладают жесткой структурой, а это позволяет переносить одну и ту же БД на разные СУБД
3) Данные хранятся структурированно.
4) Я предполагаю, что с реляционным базами данных меньше "экзотики" и нетривиальных задач (Ну до дех пор, пока мы решаем тривиальные задачи)
5) Обеспечивают целостность данных.
6) Присутствуют транзацкии которые обеспечивают надёжную работу.

---
---

### Задание 4. Кластеры

Необходимо производить большое количество вычислений при работе с огромным количеством данных, под эту задачу 
выделено 1000 машин. 

На основе какого критерия будете выбирать тип СУБД и какая модель *распределённых вычислений* 
здесь справится лучше всего и почему?

*Приведите ответ в свободной форме.*

---

Тип СУБД я буду выбирать исходя из количества машин и того, как они могут взаимодействовать между собой. Я предполагаю, что машины все связаны друг с другом и равны между собой.
Я бы выбрал NoSQL с моделью "Сеть" т.к. сетевые базы данных имеют иерархическую структуру, но в отличие от иерархических баз данных, где у одного дочернего элемента может быть только один родитель, сетевой узел может иметь отношения с несколькими объектами.















Задания,помеченные звёздочкой, — дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже разобраться в материале.
