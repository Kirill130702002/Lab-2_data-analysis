# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #1 выполнил(а):
- Упаев Кирилл Анатольевич 
- РИ-210943
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | * | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

Структура отчета

- Данные о работе: название работы, фио, группа, выполненные задания.
- Цель работы.
- Задание 1.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 2.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 3.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Выводы.
- ✨Magic ✨

## Цель работы
Ознакомиться с основными операторами зыка Python на примере реализации линейной регрессии.

## Задание 1

### Пошагово выполнить каждый пункт раздела "ход работы" с описанием и примерами реализации задач

![image](https://user-images.githubusercontent.com/104893843/205671922-0fd8fa83-5145-43bc-9052-5ca0c237d5e3.png)
![image](https://user-images.githubusercontent.com/104893843/205975039-ba9d2d84-d2c7-4850-810a-29f7892ab695.png)
![image](https://user-images.githubusercontent.com/104893843/205975136-c1f549fa-3723-4c4b-89e1-28f275601a82.png)


## Задание 2
Ссылка на ipynb http://localhost:8888/notebooks/Анализ%20данных_УрФУ/Лабораторная%20работа%201%20(шаг%202).ipynb из Jupyter notebook Prediction с кол-вом итераций увеличивает свою точность.

![image](https://user-images.githubusercontent.com/104893843/205989622-b0d4f13a-e40a-43f1-a7f4-24589d8b438d.png)
![image](https://user-images.githubusercontent.com/104893843/205989664-ce101601-ba53-44ed-94e3-6e102cb1bc05.png)
![image](https://user-images.githubusercontent.com/104893843/205989708-41a10576-5599-4c77-85d3-c22f12152271.png)
![image](https://user-images.githubusercontent.com/104893843/205989783-128b52a5-156b-46f3-980e-5cad8bd742b5.png)
![image](https://user-images.githubusercontent.com/104893843/205989838-3ac623a0-91a0-430f-b8af-33d768711bdc.png)
![image](https://user-images.githubusercontent.com/104893843/205989882-864b2439-005d-4d98-a338-89ca9cc1291a.png)
![image](https://user-images.githubusercontent.com/104893843/205989933-55d7cdbe-8303-4c45-b6e2-c0edebc7ad72.png)
![image](https://user-images.githubusercontent.com/104893843/205989974-0e0a785b-cadc-4740-8364-bed19ecd0920.png)
![image](https://user-images.githubusercontent.com/104893843/205990031-10575f94-98be-42f5-a8fa-c6c8c0568d92.png)




## Задание 3

### Должна ли величина loss стремиться к нулю при изменении исходных данных? Ответьте на вопрос, приведите пример выполнения кода, который подтверждает ваш ответ.

При изменинии весов a,b с большим кол-вом итераций loss , который является разницей между предсказанным значениеми реальным, будет убывать потому что предсказанное значение будет все ближе подбираться к реальному. Пример сравнение loss для 10000 и 1000000 итераций, где loss убывает:
![image](https://user-images.githubusercontent.com/104893843/205990924-6b040f4b-d9fa-4a72-8af6-f8550bb6d503.png)

### Какова роль параметра Lr? Ответьте на вопрос, приведите пример выполнения кода, который подтверждает ваш ответ. В качестве эксперимента можете изменить значение параметра.
Lr является скоростью и точностю обучения и если оно слишком велико то мы можем пропустить оптимальные веса, однако для этого нам понадобится меньше итераций обучения. пример для Lr = 0.000100 , где всего после 5 итераций мы уже имеем loss 237
![image](https://user-images.githubusercontent.com/104893843/205994568-85e23b3e-5eb3-4bfc-8f6a-d4d637b85aed.png)


### Выводы
Нужно уметь балансировать кол-вом итераций и Lr параметром для достижения наиболее оптимального анализа данных.