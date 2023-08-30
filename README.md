# Domain-specific-content-generation
<a name="Оглавление"></a>
## Оглавление
- [Изучение статьи](#Изучениестатьи)
     - [Что это такое?](#Чтоэтотакое?)
     - [Почему над этим работают?](#Почемунадэтимработают?)
     - [Как формулируется задача?](#Какформулируетсязадача?)
     - [В чем ее основная идея?](#Вчемееосновнаяидея?)
     - [В чем ее новаторство?](#Вчемееноваторство?)
     - [Какие получились результаты?](#Какиеполучилисьрезультаты?)
- [Практическая часть](#Практическаячасть)
     - [Промежуточные результаты с картинками](#Промежуточныерезультатыскартинками)
     - [Конечные результаты с картинками](#Конечныерезультатыскартинками)
     - [Наблюдения](#Наблюдения)
     - [... и проблемы](#проблемы)
- [Запуск](#Запуск)

<a name="Изучениестатьи"></a>
## Изучение статьи
<a name="Чтоэтотакое?"></a>
### Что это такое?
Это новый подход, который позволяет генерировать изображения объектов в различных контекстах.  
[Оглавление](#Оглавление)
<a name="Почемунадэтимработают?"></a>
### Почему над этим работают?
Это уникальное решение.  
Уже существуют нейронные сети, которые позволяют генерировать изображения по текстовому описанию, но это всегда будут разные объекты. Например, если попросить изобразить собаку конкретной породы, в конкретной позе на фоне эйфелевой башни - это всегда будут разные собаки. Представленное решение способно на основе 3-5 фотографий одной собаки генерировать изображения с ней в разных контекстов с сохранением отличительных черт и естественности.  
![image](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/79bb83f9-f24f-4506-9762-efa5beb25c34)
  
Современные модели не могут точно реконструировать внешний вид заданных предметов, а лишь создают вариации содержания изображения.  
[Оглавление](#Оглавление)
<a name="Какформулируетсязадача?"></a>
### Как формулируется задача?
Необходимо создать модель, которая по входящим 3-5 изображениям одного и того же объекта будет генерировать его в различных контекстах, связать изображение и текст так, чтобы сохранить уникальные черты объекта и не потерять естественность.  
[Оглавление](#Оглавление)
<a name="Вчемееосновнаяидея?"></a>
### В чем ее основная идея?
В данной работе исследователи представляют новый подход к "персонализации" диффузионных моделей "текст-изображение" (их адаптации к потребностям пользователя при генерации изображений). Цель - расширить языковой словарь модели таким образом, чтобы она связывала новые слова с конкретными темами, которые пользователь хочет генерировать. Для этого предлагается методика представления заданного субъекта с помощью редких токенов-идентификаторов и тонкуая настройка предварительно обученного фреймворка преобразования текста в изображение на основе диффузии. Тонкая настройка модели преобразования текста в изображение осуществляется с помощью входных изображений и текстовых подсказок, содержащих уникальный идентификатор, за которым следует название класса предмета (например, "A [V] dog").  
[Оглавление](#Оглавление)
<a name="Вчемееноваторство?"></a>
### В чем ее новаторство?
Это иновационное решение, которое позволяет решить новую сложную задачу генерации изображений на основе субъекта. Для предотвращения явления, при котором модель ассоциирует название класса с конкретным экземпляром, предлагается использовать автогенную функцию потерь. Также данный подход позволяет решать множество новых задач: реконтекстуализацию, художественную рендеризацию, синтез новых представлений, модификацию свойств.  
![image](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/2d41f718-a001-4153-bb5b-16c2648c7f3e)
  
[Оглавление](#Оглавление)
<a name="Какиеполучилисьрезультаты?"></a>
### Какие получились результаты?
Авторы представили пример генерации изображения с несколькими входными изображениями на дополнительном контексте, получилось очень точно все воспроизвести. Был создан датасет, состоящий из 30 различных классов из животных и неодушевленных объектов. Было проведено сравнение результатов с Textual Inversion (единственной сопоставимой работе, которая ориентирована на предмет и текст и генерирует изображения), DreamBooth (Imagen) и DreamBooth (Stable Diffusion). По всем метрикам (DINO, CLIP-I, CLIP-T) результаты DreamBooth (Imagen) оказались более приближены к реальным изображениям. Также авторы говорят об ограничениях данного метода, приводят несколько неудачных примеров генерации. Возможные причины - слабый приоритет для таких контекстов, сложность генерации как предмета, так и заданного понятия вместе из-за низкой вероятности совместного использования. Вторая причина - смешение контекста и внешнего вида, когда внешний вид субъекта изменяется под воздействием контекста подсказки, например с изменением цвета объекта. Третья - чрезмерную подгонка к реальным изображениям, которая происходит, когда подсказка похожа на исходную обстановку, в которой находится объект. Было замечено, что такие предметы, как рюкзак легче поддаются генерации, чем кошки и собаки.  
[Оглавление](#Оглавление)
<a name="Практическаячасть"></a>
## Практическая часть
<a name="Промежуточныерезультатыскартинками"></a>
### Промежуточные результаты с картинками
В процессе работы получилось дообучить модель на небольшом домене из 10 картинок с героем Cinnamonroll 512x512 пикселей. Примеры картинок:  
<img src="https://user-images.githubusercontent.com/55783463/264398227-f035bb43-9bb9-4ee0-b0c6-f0f63bc26480.png" width="256" height="256" title="Github Logo">
<img src="https://user-images.githubusercontent.com/55783463/264429121-f7628fe1-644c-4dd4-8525-df22f7078221.jpg" width="256" height="256" title="Github Logo">

Изначально было решено увеличить количество эпох до 500 и изменить batch size на 10, learning rate для энкодера = 5e-5, learning rate для unet = 3e-4, random seed = 40. В качестве INFERENCE_PROMPT для тестирования использовалась фраза "cinnamoroll a toy". Получился следующий результат:  
![загруженное (16)](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/5fee849f-3bba-4701-af94-650d4bb974a3)
![загруженное (4)](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/dda15d97-eded-492a-ba5e-d17d7ee84b43)    
Для "cinnamoroll ridding a bycicle" получаются пугающие огромные зайцы на настоящих велосипедах, не как на картинке из обучающего набора:  
![загруженное (15)](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/f547699e-b4e6-4692-b35d-a9a287953727)
![загруженное (14)](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/b05f0857-05b6-41c2-b7c3-fab90a47dbff)    
Для "crochet toy cinnamoroll" получаются лунтики:  
![загруженное (5)](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/e3d9c4a0-95e0-4338-adbd-a14510261fb9)
![загруженное (9)](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/2121eda3-7d01-4b24-9aa8-cb2cc3154e78)
![загруженное (13)](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/a70ea377-f1bf-49fa-90eb-dab510c49c70)    
Для "cup with printed cinnamoroll" самые красивые изображения(я бы хотела такую кружку):  
![загруженное (2)](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/f9d2301b-c6c7-4a32-848b-b54320e9617a)
![загруженное (1)](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/1ee545e9-d14c-4348-a53e-a5bbfe361e8c)    
Для "art of cinnamoroll eating strawberry" тоже лунтики:  
![загруженное (7)](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/7d15432e-54e7-46ac-8f1d-132126601362)
![загруженное (6)](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/e69911c4-92b4-4477-a1a2-ef0dc56a169b)    
Для "art of cooking cinnamoroll" получается такой mood ▓▒░(°◡°)░▒▓:  
![загруженное (3)](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/7e0f3311-80ae-4f1b-9bcd-beecdd320f50)    
    
При меньшем количестве эпох получались совсем невнятные изображения, например при epoch = 300, batch size = 1, learning rate для энкодера = 1e-5, learning rate для unet = 3e-4, random seed = 40, prompt = 'cinnamoroll a toy':  
![загруженное](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/27d3cc75-a605-428b-b15d-6286f4328f62)    
Или другой пример epoch = 300, batch size = 1, learning rate для энкодера = 1e-5, learning rate для unet = 3e-4, random seed = 40, prompt = 'crochet toy cinnamoroll':  
![загруженное (8)](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/a138f58c-ab8e-4f99-aba3-7754b208addb)  
[Оглавление](#Оглавление)  
<a name="Конечныерезультатыскартинками"></a>
### Конечные результаты с картинками
При epoch = 500, batch size = 1 (т.к. картинок и так мало и если брать 10 то значения просто будут усредняться), learning rate для энкодера = 1e-5, learning rate для unet = 3e-4, seed = 123.  
prompt = 'cinnamoroll a toy', guidance = 13, LORA_SCALE_UNET = 0.5, LORA_SCALE_TEXT_ENCODER = 0.1  
![image](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/122f0f3e-73fb-4d20-82f3-1585ec48cb0f)
![image](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/5ed8d6dc-4d4e-4c0a-9dff-a5e24d7bb570)
![image](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/ab03be00-066a-429a-afb2-184736efae3b)
![image](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/19086ad6-d914-4beb-841e-4f171bb39d86)

prompt = 'crochet toy cinnamoroll', guidance = 11, LORA_SCALE_UNET = 0.5, LORA_SCALE_TEXT_ENCODER = 0.1 (очень много неудачных вариантов):
![image](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/c350eaf3-402a-4a3f-a2e3-56db75b28938)
![image](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/fbd65aa2-0dfa-419c-b567-c00315e636d5)

prompt = 'cinnamoroll eat strawberry', guidance = 11.8, LORA_SCALE_UNET = 0.5, LORA_SCALE_TEXT_ENCODER = 0.1:
![image](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/aa71b88b-ad53-42c0-b7c5-c95c53eeff14)
![image](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/d4f5f2d8-9f19-4a0a-a632-b79fd3da5e76)
![image](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/ba5b24c3-8602-4bd0-9191-00b30b3f62a1)

prompt = 'cup with printed cinnamoroll', guidance = 11.8, LORA_SCALE_UNET = 0.5, LORA_SCALE_TEXT_ENCODER = 0.1:
![image](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/c417e3dd-b019-4b13-a294-e7242a728211)
![image](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/3190339f-1aad-4381-b6d4-77b5932b6fe4)
![image](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/74990133-8bb6-42b2-994c-8eae811c6873)

Решила проверить есть ли зависимость от порядка слов, prompt = 'cinnamoroll printed on cup', guidance = 11.8, LORA_SCALE_UNET = 0.5, LORA_SCALE_TEXT_ENCODER = 0.1:
![image](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/a803159e-167b-47c9-8146-cf17a00c422a)
![image](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/da8bb6cb-e177-4a87-b003-eb9d80c2700a)
![image](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/bd069753-bb85-4229-8bc8-6ef9d5b0ae29)

prompt = 'cinnamoroll ridding bicycle', guidance = 13.8, LORA_SCALE_UNET = 0.8, LORA_SCALE_TEXT_ENCODER = 0.2
Ожидание(из датасета):  
![5](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/aaf41ab6-1142-464d-b86c-f156e5a2a1dd)
Реальность:  
![image](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/756f6c88-cc91-471b-b597-4d7f03eacde7)
![image](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/6e5c07d6-cec6-4e77-a323-542648948a91)
![image](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/86d9aad9-2a35-4005-8b63-d2838b125f99)
![image](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/6d691497-2cd6-4ad7-af15-da6eb183f201)
![image](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/34bb2b24-0b0b-4599-87c8-9563ae2a60d6)

prompt = 'black colored cinnamoroll', guidance = 9, LORA_SCALE_UNET = 0.9, LORA_SCALE_TEXT_ENCODER = 0.1
![image](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/0d55bca9-5f26-4c48-8c13-82a7857d0f3a)
prompt = 'black colored cinnamoroll', guidance = 13.2, LORA_SCALE_UNET = 0.9, LORA_SCALE_TEXT_ENCODER = 0.1
![image](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/57e82a53-9eec-4a5c-befb-65eec8fdb3ba)

Сколько бы я ни пыталась у меня не получилось изобразить prompt = 'cinnamoroll with a green frog shaped cap on head', guidance = 13.8, LORA_SCALE_UNET = 0.8, LORA_SCALE_TEXT_ENCODER = 0.5  
Ожидание(из датасета):  
![3](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/ffb16f26-b582-436c-93ef-3ecab79e182b)  
Реальность:  
![image](https://github.com/compfee/Domain-specific-content-generation/assets/55783463/f7ea372c-e8d2-49ed-bad4-b3096f4e947b)  

  [Оглавление](#Оглавление)
<a name="Наблюдения"></a>
### Наблюдения
- Самые лучшие изображения получаются с какими то простыми объектами, например с кружками.
- Сеть выдает более правдивые(если так можно судить) результаты, если выкрутить GUIDANCE на 9-15.
- При большем количестве эпох результаты не становятся сильно лучше, чем при 500, если увеличивать learning rate, то само собой результаты ухудшаются.
- Решила посмотреть, как дообучают модель другие люди, в случае добавления текстовых файлов с ключевыми словами результаты генерации оказываются лучше.  
[Оглавление](#Оглавление)
<a name="проблемы"></a>
### ... и проблемы
В самом начале я столкнулась с ошибкой при запуске обучения:  

>TypeError: Accelerator.__init__() got an unexpected keyword argument 'logging_dir'

Оказалось что в файле train_lora_dreambooth.py необходимо заменить logging_dir на project_dir т. к. [версия устарела](https://github.com/huggingface/accelerate/issues/1550#issuecomment-1580974666)  

[Оглавление](#Оглавление)
<a name="Запуск"></a>
## Запуск
- С помощью  [Google Colab](https://colab.research.google.com/drive/1KSWUJNQqrKeELghrk3esOyG6FdGI4HEn?usp=sharing) запустить ноутбук.
- Создать папки input и output
- Указать их в качестве OUTPUT_DIR и IMAGES_FOLDER_OPTIONAL, а также все learning rate
- Загрузить в input изображения
- Предварительно перед запуском обучения заменить 493 строчку в файле /content/lora/training_scripts/train_lora_dreambooth.py.  

Было:  
```python
accelerator = Accelerator(
        gradient_accumulation_steps=args.gradient_accumulation_steps,
        mixed_precision=args.mixed_precision,
        log_with="tensorboard",
        logging_dir=logging_dir,
    )
```  
Стало:  
```python
accelerator = Accelerator(
        gradient_accumulation_steps=args.gradient_accumulation_steps,
        mixed_precision=args.mixed_precision,
        log_with="tensorboard",
        project_dir=logging_dir,
    )
```
Готово! °˖✧◝(⁰▿⁰)◜✧˖°  
[Оглавление](#Оглавление)








