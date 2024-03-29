# 1. Инфо:
Шматов Арсений, 153501
Тема приложения: Сайт продажи фруктов
СУБД: Postgre SQL

# 2. Функциональные требования:
  1. Авторизация пользователя.
  2. Управление пользователями (CRUD).
  3. Ролевая система(Клиент, Сотрудник, Админ).
  4. Ведение журнала действий пользователя.(Покупки, Отзывы)
  6. Просмотр сортудников(Клиент)
  7. Управление Фруктами, Производитлями (Сотрудник).
  8. Управление отзывами CRUD (Админ).
     
# 3. Список таблиц для базы данных:
  1. "Фрукты":

    Поля:
        ID (INT, PRIMARY KEY, AUTOINCREMENT, NN)
        Название (VARCHAR(50), NN)
        Дата изготовления (DATETIME, NN)
        Цена (INT, NN)
        Срок годности(INT, NN)
        ID производителя(FOREIGN KEY REFERENCES Производители(ID), NN)
    Связи:  
       Связь с таблицей "Производители" в отношении "Многие к одному" (Many-to-One) через поле ID производителя.

  2. "Заказы":

    Поля:
        ID (INT, PRIMARY KEY, AUTOINCREMENT, NN)
        Дата создания (DATETIME, NN)
        Сумма заказа (INT, NN)
        Количество товара(INT, NN)
        ID клиента (INT, FOREIGN KEY REFERENCES Клиенты(ID), NN)
        ID фрукта (INT, FOREIGN KEY REFERENCES Фрукты(ID), NN)
        
    Связи:
       Связь с таблицей "Клиенты" в отношении "Многие к одному" (Many-to-One) через поле ID клиента.
       Связь с таблицей "Фрукты" в отношении "Многие к одному" (Many-to-One) через поле ID фрукта.

  3. "Клиенты":

    Поля:
        ID (INT, PRIMARY KEY, AUTOINCREMENT, NN)
        Адрес (VARCHAR(200), NN) 
        ID пользователя (INT, UNIQUE, NN)
   Связи:
       Связь с таблицей "Пользователи" в отношении "Один к одному" (One-to-One) через поле ID клиента.

  4. "Роли":

    Поля:
        ID (INT, PRIMARY KEY, AUTOINCREMENT, NN)
        Название роли (VARCHAR(25), UNIQUE, NN)

  5. "Отзывы":

    Поля:
        ID (INT, PRIMARY KEY, AUTOINCREMENT, NN)
        Текст отзыва (TEXT, NN)
        Оценка (INT, NN)
        ID фрукта (INT, FOREIGN KEY REFERENCES Фрукты(ID), NN)
        ID клиента (INT, FOREIGN KEY REFERENCES Клиенты(ID), NN)
    Связи:
        Связь с таблицей "Фрукты" в отношении "Многие к одному" (Many-to-One) через поле ID автомобиля.
        Связь с таблицей "Клиенты" в отношении "Многие к одному" (Many-to-One) через поле ID клиента.

  6. "Сотрудники":

    Поля:
        ID (INT, PRIMARY KEY, AUTOINCREMENT, NN)
        Зарплата (INT, NN)
        ID пользователя (INT, UNIQUE, NN)
        
        ID времени (INT, FOREIGN KEY REFERENCES Рабочее время сотрудников(ID))
    Связи:
        Связь с таблицей "Рабочее время сотрудников" в отношении "Многие к одному" (Many-to-One) через поле ID времени.
       Связь с таблицей "Пользователи" в отношении "Один к одному" (One-to-One) через поле ID клиента.
       
  7. "Рабочее время сотрудников":
    
    Поля:
        ID (INT, PRIMARY KEY, AUTOINCREMENT, NN)
        Дата и время начала работы (DATETIME, NN)
        Дата и время окончания работы (DATETIME, NN)
        
  8. "Доставка":
      
    Поля:
        ID (INT, PRIMARY KEY, AUTOINCREMENT, NN)
        ID заказа (INT, UNIQUE, NN)
        Дата доставки (DATETIME, NN)
    Связи:
        Связь с таблицей "Заказы" в отношении "Один к одному" (One-to-One) через поле ID заказа.
      
  9. "Производители":

    Поля:
        ID (INT, PRIMARY KEY, AUTOINCREMENT, NN)
        Страна производителя (VARCHAR(50), NN)
        Имя комании (VARCHAR(50), NN)
        
 10. "Пользователи":

    Поля:
        ID (INT, PRIMARY KEY, AUTOINCREMENT, NN)
        Имя ((VARCHAR(50), NN)
        Фамилия ((VARCHAR(50), NN)
        Телефон (CHAR(13) ~ '+375[0-9]{9}' NN,)
        Пароль ((VARCHAR(50), NN)
        ID Роли (INT, FOREIGN KEY REFERENCES Роли(ID))
    Связи:
        Связь с таблицей "Роли" в отношении "Многие к одному" (Many-to-One) через поле ID Роли.

  11. "Должности":
    Поля:
        ID (INT, PRIMARY KEY, AUTOINCREMENT, NN)
        Название(VARCHAR(50), NN)
      
  12. "Должности/Сотрудники"(вспомогательная):
        ID (INT, PRIMARY KEY, AUTOINCREMENT, NN)
        ID должности(INT, FOREIGN KEY REFERENCES(Должности), NN)
        ID сотрудника(INT, FOREIGN KEY REFERENCES(Сотрудники), NN)
    Связи:
        Связь между Должности/Сотрудники(Many to many) через поля  ID должности и ID сотрудника
      
        

# 4. Use-case:
  Неавторизованный пользователь:
  
    Просматривать список сотрудников
    Просматривать каталог фруктов
    Просматривать отзывы
    Авторизовываться 
    
  Авторизованный пользователь(Клиент):
    
    Все, что и неавторизованный пользователь
    Совершать заказ
    Оставлять отзыв
    
  Сотрудник:
   
    Все, что и клиент
    CRUD к фруктам, Производителям
    
  Админ:
  
    Все, что и сотрудник
    CRUD ко всем моделям
    
# 5. Диаграмма: 

![image](https://github.com/ArseniiShmatov09/Python_Labs_Shmatov_Arsenii_153505/assets/94675119/b0c63305-9511-420c-a901-82a86d353d7b)

![image](https://github.com/ArseniiShmatov09/Python_Labs_Shmatov_Arsenii_153505/assets/94675119/88c304f9-bd17-4379-ad9f-3933c589598f)

