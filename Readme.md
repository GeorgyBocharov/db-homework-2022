Я запустил mongo-db в докере через docker-compose.yaml файл.
Потом залил в бд данный из датасета iris, используя библиотеку pymongo питона. Данные залил несколько раз, чтобы их было больше.
Затем пробовал запускать запросы на поиск с фильтрацией без индекса и с индексом на указанный параметр. Запросы запускал через MongoDB Compass.

MongoDb в докере:
![image](https://user-images.githubusercontent.com/31734802/157730864-9809b33a-277f-4370-8d27-31459ffd427f.png)

Скрин docker-compose:
![image](https://user-images.githubusercontent.com/31734802/157732292-0d00a5d0-7a7b-4ec5-8cab-48e778808a4d.png)


Запрос без индекса
![image](https://user-images.githubusercontent.com/31734802/157727944-9487a442-20dc-48d1-a89a-80aa25e781c6.png)
Запрос с индексом
![image](https://user-images.githubusercontent.com/31734802/157729660-3c15985e-89f4-46bf-a1fd-37741406d253.png)
Я создал возрастающий индекс для поля sepal_length. Благодаря индексу при запросе данных с большими значениями sepal_length запрос выполняется быстрее, однако при 
запросе данных с низким значением sepal_length запрос работает ощутимо медленее, чем при отсутсвии индекса. 




