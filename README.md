# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #1 выполнил(а):
- Турницкий Никита Александрович
- ри 210943
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | # | 20 |
| Задание 3 | # | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

Структура отчета

- Данные о работе: название работы, фио, группа, выполненные задания.
- Цель работы. 
- Задание 1.
- В проекте Unity реализовать перцепотрон, который умеет производитдь вычесления:
    OR
    AND
    NAND
    XOR
- Задание 2.
- построить глафик зависомости количества эпох от ошиби обучения, указать от чего зависит необходимое количество эпох   обучения. 
- Задание 3.
- построить визуальную модель работы перцептрона на сцене unity 
- Выводы.
- ✨Magic ✨

## Цель работы
познакомиться с программными средствами для организции
передачи данных между инструментами google, Python и Unity

## Задание 1
### Реализовать совместную работу и передачу данных в связке Python
- Google-Sheets – Unity.
Ход работы:
1. Настроить гугл api для работы с google sheets
  ![alt text](https://github.com/Devilboi99/Labs-2/blob/master/изображение_2022-11-22_143024041.png)
2. создать таблицу 
   ![alt text](https://github.com/Devilboi99/Labs-2/blob/master/изображение_2022-11-22_143217457.png)
3. настроить питон подсоеденить к таблицы и вывести данные
    ![alt text](https://github.com/Devilboi99/Labs-2/blob/master/работа%20в%20python%20and%20google%20sheetsjpg.jpg)
4. использовать эти данные в проете unity
     ![alt text](https://github.com/Devilboi99/Labs-2/blob/master/Unity%20работа%20голоса.jpg)
```css
public class NewBehaviourScript : MonoBehaviour
{
    public AudioClip goodSpeak;
    public AudioClip normalSpeak;
    public AudioClip badSpeak;
    private AudioSource selectAudio;
    private Dictionary<string,float> dataSet = new Dictionary<string, float>();
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
        if (statusStart || i == dataSet.Count)
            return;
        
        if (dataSet["Mon_" + i.ToString()] <= 10 )
            StartCoroutine(PlaySelectAudio(goodSpeak));
        
        if (dataSet["Mon_" + i.ToString()] > 10 && dataSet["Mon_" + i.ToString()] < 100)
            StartCoroutine(PlaySelectAudio(normalSpeak));
        
        if (dataSet["Mon_" + i.ToString()] >= 100)
            StartCoroutine(PlaySelectAudio(badSpeak));
        
        
        Debug.Log(dataSet["Mon_" + i.ToString()]);
    }

    IEnumerator GoogleSheets()
    {
        UnityWebRequest curentResp = UnityWebRequest.Get("https://sheets.googleapis.com/v4/spreadsheets/1KFYtu94ek1KHm5P0GMD-CqJtNClE99yCFGe-795-EGE/values/Лист1?key=AIzaSyAZc30RVQXbXiDVHAqL65aCNip5CPEbPJU");
        yield return curentResp.SendWebRequest();
        var rawResp = curentResp.downloadHandler.text;
        var rawJson = JSON.Parse(rawResp);
        foreach (var itemRawJson in rawJson["values"])
        {
            var parseJson = JSON.Parse(itemRawJson.ToString());
            var selectRow = parseJson[0].AsStringList;
            dataSet.Add(("Mon_" + selectRow[0]), float.Parse(selectRow[3]));   // здесь я до этого накосячил с таблицей поэтому в 4 элементе данные
        }
    }

    IEnumerator PlaySelectAudio(AudioClip typeSpeak)
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = typeSpeak;
        selectAudio.Play();
        yield return new WaitForSeconds(3);
        statusStart = false;
        i++;
    }
}

```
- научить работь его с and (Ему потербовалась в среднем больше попыток, чтоб понять как работает and)
![alt text](https://github.com/Devilboi99/Labs-4/blob/master/изображение_2022-11-21_150908044.png)
- научить работать с nand (в среднем работает так же как и and)
![alt text](https://github.com/Devilboi99/Labs-4/blob/master/изображение_2022-11-21_151303532.png)
- научить работать с xor 
![alt text](https://github.com/Devilboi99/Labs-4/blob/master/изображение_2022-11-21_152122564.png)
Как было сказано в лекций, парцетрон не может обучиться на не линейных операция, собственно, видно, что он это и не может (было 500 тренировок)

## Выводы
понял, что такое парцентрон: его минусы, зачем он нужен и как его использовать.

## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**

```css
    Console.Log("hello world");
```
