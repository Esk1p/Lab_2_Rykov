# РАЗРАБОТКА ИГРОВЫХ СЕРВИСОВ [in GameDev]
Отчет по лабораторной работе #2 выполнил(а):
- Рыков Дмитрий Алексеевич
- РИ000024
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
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 2.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 3.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Выводы.

## Цель работы
Cоздание интерактивного приложения и изучение принципов интеграции в него игровых сервисов.
## Задание 1
### По теме видео практических работ 1-5 повторить реализацию игры на Unity. Привести описание выполненных действий.
## Ход работы:
1) Выбор игровых моделей и настройка анимаций;
2) Написание скрипта для движения персонажа;

## Результат выполнения хода работы
### 1) Выбор игровых моделей и настройка анимаций
Я решил не использовать модели, которые были показаны преподавателем, а потому нашел свои. В качестве героя вместо дракона я взял аниме девочку из ассета "Unity-Chan! Model", в котором также были все необходимые анимации.
![image](https://user-images.githubusercontent.com/91608946/194338117-0856c957-4204-4a44-b758-f01c4787f40e.png)

Вместо энергетического щита я решил использовать корзину из ассета "Crate and Barrels".
![image](https://user-images.githubusercontent.com/91608946/194338827-0d49eb75-81bd-486e-a108-9f59b22c7ed4.png)

Вместо драконьих яиц взял мишку из ассета "FREE Christmas Presents / Low Poly".
![image](https://user-images.githubusercontent.com/91608946/194339413-80a560ed-ad7b-44fb-8df0-a0d5373c2756.png)

Затем, после выбора моделей, я приступил к настройке анимаций. Мною был создан контроллер анимаций, в котором содержалась анимация бега персонажа, затем контроллер был подключен к префабу модели. Вот, что вышло в результате: 
![nFUk6KYiCO](https://user-images.githubusercontent.com/91608946/194358546-ff8e6747-64fc-496f-9005-cdcd9c4ddeed.gif)


### 1) Написание скрипта для движения персонажа

Скрипт для движения персонажа выглядит следующим образом:
```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class TyanMove : MonoBehaviour
{
    // Создание переменных
    public GameObject taddyPrefab;

    public float speed = 1;

    public float timeBetweenTaddyDrops = 1f;

    public float leftRightDistance = 10f;

    public float chanceDirection = 0.1f;

    void Start()
    {
        Invoke("DropTaddy", 2f);
    }
    
    // Функция для сбрасывания подарков
    void DropTaddy(){
        Vector3 myVector = new Vector3(0.0f,0.0f,0.0f);
        GameObject taddy = Instantiate<GameObject>(taddyPrefab);
        taddy.transform.position = transform.position + myVector;
        Invoke("DropTaddy", 2f);
    }
    

    void Update()
    {
      
        //Часть кода, для задания скорости персонажа + настройки необходимого угла его отображения

        Vector3 pos = transform.position;
        pos.x += speed * Time.deltaTime;
        transform.position = pos;

        if (pos.x < -leftRightDistance){
            speed = Mathf.Abs(speed);
        }
        else if (pos.x > leftRightDistance){
            speed = -Mathf.Abs(speed);
        }

        if (speed >0){
            gameObject.transform.rotation = Quaternion.Euler(0, 90, 0);
        }
        else{
            gameObject.transform.rotation = Quaternion.Euler(0, 270, 0);
        }
  
    }

    //Функция для рандомного изменения направления персонажа
    private void FixedUpdate() {
        if (Random.value < chanceDirection){
            speed *= -1;
        }
        
    }


}
```




## Выводы
В результате выполнения лабораторной работы №2 мы создали интерактивное приложение и изучили принципы интеграции в него игровых сервисов.


