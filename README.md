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
### Реализовать совместную работу и передачу данных в связке Python - Google-Sheets – Unity.
Ход работы: 
1. Я создал google таблицу и добавил пользователя, а после написал код на python для заполнения ячеек нужными данными в таблице
```py
import gspread
import numpy as np

gc = gspread.service_account(filename='unitydatascince-370917-682594e4a037.json')
sh = gc.open('UnitySheets')
price = np.random.randint(2000, 10000, 11)
mon = list(range(1, 11))

i = 0
while i <= len(mon):
    i += 1
    if i == 0:
        continue
    else:
        temp_inf = ((price[i - 1] - price[i - 2]) / price[i - 2]) * 100
        temp_inf = str(temp_inf)
        temp_inf = temp_inf.replace('.', ',')
        sh.sheet1.update(('A' + str(i)), str(i))
        sh.sheet1.update(('B' + str(i)), str(price[i - 1]))
        sh.sheet1.update(('C' + str(i)), str(temp_inf))
        print(temp_inf)
```

2. Результаты выполнения в простанстве имен main.py и заполненная автоматическими этими же данными google таблица:
![image](https://user-images.githubusercontent.com/104893843/206854024-0d545429-7528-4524-af95-a0ef5e95e7b9.png)
![image](https://user-images.githubusercontent.com/104893843/206854035-720ce92c-ce19-4340-b209-3bd78f08a02b.png)
![image](https://user-images.githubusercontent.com/104893843/206920345-150cae1c-ccb8-44c1-a0a8-97ecc985cda4.png)

После этого был написанн C# скрипт для юнити чтобы подгрузить данные из гугл таблиц в юнити и связать это с звуком в зависимости от данных.

Код записанный в скрипте С№:
```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.Networking;
using SimpleJSON;

public class NewBehaviourScript : MonoBehaviour
{
    public AudioClip goodSpeak;
    public AudioClip normalSpeak;
    public AudioClip badSpeak;
    private AudioSource selectAudio;
    private Dictionary<string, float> dataSet = new Dictionary<string, float>();
    private bool statusStart = false;
    private int i = 1;

 
    // Start is called before the first frame update
    void Start()
    {
        StartCoroutine(GoogleSheets());

    }

    // Update is called once per frame
    void Update()
    {
        if (dataSet["Mon_" + i.ToString()] <= 10 & statusStart == false & i != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioGood());
            Debug.Log(dataSet["Mon_" + i.ToString()]);
        }

        if (dataSet["Mon_" + i.ToString()] > 10 & dataSet["Mon_" + i.ToString()] <= 100 & statusStart == false & i != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioNormal());
            Debug.Log(dataSet["Mon_" + i.ToString()]);
        }

        if (dataSet["Mon_" + i.ToString()] >= 100 & statusStart == false & i != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioBad());
            Debug.Log(dataSet["Mon_" + i.ToString()]);
        }
    }

    IEnumerator GoogleSheets()
    {
        UnityWebRequest curentResp = UnityWebRequest.Get("https://sheets.googleapis.com/v4/spreadsheets/11OrVsuBftaqx-aVzEqo8SA8FyxlovmJQdGOqDjuu2VE/values/Лист1?key=AIzaSyCkKLOv5Wvmfpkco4Bp-LfoCPYLK3YyldU");
        yield return curentResp.SendWebRequest();
        string rowResp = curentResp.downloadHandler.text;
        var rowJson = JSON.Parse(rowResp); 
        foreach (var itemRowJson in rowJson["values"]) 
        {
            var parseJson = JSON.Parse(itemRowJson.ToString());
            var selectRow = parseJson[0].AsStringList;
            dataSet.Add(("Mon_" + selectRow[0]), float.Parse(selectRow[2]));
        }
    }

    IEnumerator PlaySelectAudioGood()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = goodSpeak;
        selectAudio.Play();
        yield return new WaitForSeconds(3);
        statusStart = false;
        i++;
    }

    IEnumerator PlaySelectAudioNormal()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = normalSpeak;
        selectAudio.Play();
        yield return new WaitForSeconds(3);
        statusStart = false;
        i++;
    }

    IEnumerator PlaySelectAudioBad()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = badSpeak;
        selectAudio.Play();
        yield return new WaitForSeconds(4);
        statusStart = false;
        i++;
    }
}
```
Результаты выполнения скрипта:
![image](https://user-images.githubusercontent.com/104893843/206923040-8adfb059-bbd5-4564-8fc8-212d35e0092e.png)



## Задание 2
### Сделать подгрузку результатов 1 лабы в гугл таблицы.
Файл 1 лабораторной работы был модифицирован и были сделанны 4 измерения на 1, 10, 100, 1000 итераций после чего данные об A, B, LOSS были внесенны в таблицу

```py
import gspread
import numpy as np
# define data, and change list to array

x = [3, 21, 22, 34, 54, 34, 55, 67, 89, 99]
x = np.array(x)
y = [2, 22, 24, 65, 79, 82, 55, 130, 150, 199]
y = np.array(y)

def model(a, b, x):
    return a * x + b

def loss_function(a, b, x, y):
    num = len(x)
    prediction = model(a, b, x)
    return (0.5 / num) * (np.square(prediction - y)).sum()

def optimize(a, b, x, y):
    num = len(x)
    prediction = model(a, b, x)
    da = (1.0 / num) * ((prediction - y) * x).sum()
    db = (1.0 / num) * ((prediction - y).sum())
    a = a - Lr*da
    b = b - Lr*db
    return a, b

def iterate(a, b, x, y, times):
    for i in range(times):
        a, b = optimize(a, b, x, y)
    return a, b

gc = gspread.service_account(filename="unitydatascince-370917-682594e4a037.json")
sh = gc.open("UnitySheets")


def Send(i: int, a, b, loss):
    sh.sheet1.update("A" + str(i), str(a))
    sh.sheet1.update("B" + str(i), str(b))
    sh.sheet1.update("C" + str(i), str(loss))
    print(a, b, loss)


a = np.random.rand(1)
b = np.random.rand(1)
Lr = 0.000001


a, b = iterate(a, b, x, y, 1)
prediction = model(a, b, x)
loss = loss_function(a, b, x, y)
Send(1, a, b, loss)

a, b = iterate(a, b, x, y, 10)
prediction = model(a, b, x)
loss = loss_function(a, b, x, y)
Send(2, a, b, loss)

a, b = iterate(a, b, x, y, 100)
prediction = model(a, b, x)
loss = loss_function(a, b, x, y)
Send(3, a, b, loss)

a, b = iterate(a, b, x, y, 1000)
prediction = model(a, b, x)
loss = loss_function(a, b, x, y)
Send(4, a, b, loss)
```

![image](https://user-images.githubusercontent.com/104893843/206924118-1d7ac37f-2633-4055-9738-9dc4271b9fbc.png)
![image](https://user-images.githubusercontent.com/104893843/206924162-a7e29fe9-0195-4821-a640-08fc666aa48c.png)


## Задание 3
Был переписан скрипт из 1 задания для подгрузки данных об A, B, LOSS из гугл таблицы После чего в зависимости от LOSS проигрывался звук: LOSS > 1500 = Badaudio , LOSS <= 1500 && LOSS > 500 = Noramlaudio , LOSS <= 500 = Goodaudio Результат работы скрипта:

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.Networking;
using SimpleJSON;
using System.Globalization;

public class NewBehaviourScript : MonoBehaviour
{
    public AudioClip goodSpeak;
    public AudioClip normalSpeak;

    public AudioClip badSpeak;

    private AudioSource selectAudio;
    private Dictionary<string, double> dataSet = new Dictionary<string, double>();
    private bool statusStart = false;
    private int i = 0;


    // Start is called before the first frame update
    void Start()
    {
        StartCoroutine(GoogleSheets());
    }

    // Update is called once per frame
    void Update()
    {
        if (statusStart == false & i != dataSet.Count && dataSet["Loss_" + i.ToString()] <= 500)
        {
            StartCoroutine(PlaySelectedaudioGood());
            Debug.Log(dataSet["Loss_" + i.ToString()]);
        }

        if (statusStart == false & i != dataSet.Count && dataSet["Loss_" + i.ToString()] > 500 && dataSet["Loss_" + i.ToString()] < 1500)
        {
            StartCoroutine(PlaySelectedaudioNormal());
            Debug.Log(dataSet["Loss_" + i.ToString()]);
        }

        if (statusStart == false & i != dataSet.Count && dataSet["Loss_" + i.ToString()] >= 1500)
        {
            StartCoroutine(PlaySelectedaudioBad());
            Debug.Log(dataSet["Loss_" + i.ToString()]);
        }
    }

    IEnumerator GoogleSheets()
    {
        UnityWebRequest currentResp = UnityWebRequest.Get("https://sheets.googleapis.com/v4/spreadsheets/11OrVsuBftaqx-aVzEqo8SA8FyxlovmJQdGOqDjuu2VE/values/Лист1?key=AIzaSyCkKLOv5Wvmfpkco4Bp-LfoCPYLK3YyldU");
        yield return currentResp.SendWebRequest();
        string rawResp = currentResp.downloadHandler.text;
        var rawJson = JSON.Parse(rawResp);
        for (var i = 0; i < rawJson["values"].Count; i++)
        {
            var item = rawJson["values"][i];
            var parseJson = JSON.Parse(item.ToString());
            var selectedRow = parseJson.AsStringList;
            var value = selectedRow[2];
            var loss = double.Parse(value, CultureInfo.InvariantCulture);
            dataSet.Add("Loss_" + i.ToString(), loss);
        }
    }

    IEnumerator PlaySelectedaudioGood()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = goodSpeak;
        selectAudio.Play();
        yield return new WaitForSeconds(3);
        statusStart = false;
        i++;
    }

    IEnumerator PlaySelectedaudioNormal()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = normalSpeak;
        selectAudio.Play();
        yield return new WaitForSeconds(4);
        statusStart = false;
        i++;
    }

    IEnumerator PlaySelectedaudioBad()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = badSpeak;
        selectAudio.Play();
        yield return new WaitForSeconds(2);
        statusStart = false;
        i++;
    }
}
```

![image](https://user-images.githubusercontent.com/104893843/206925083-805194bb-8c54-4b29-b767-546ad9facc79.png)

## Выводы
Я научился подгружать данные в google таблицу и выгружать их оттуда помощи связки python , C#
