# Domain-specific-content-generation

## Что это такое?
   Это новый подход, который позволяет генерировать изображения объектов в различных контекстах.
## Почему над этим работают?
   Это уникальное решение.
   Уже существуют нейронные сети, которые позволяют генерировать изображения по текстовому описанию, но это всегда будут разные объекты. Например, если попросить изобразить собаку конкретной породы, в конкретной позе на фоне эйфелевой башни - это всегда будут разные собаки. Представленное решение способно на основе 3-5 фотографий одной собаки генерировать изображения с ней в разных контекстов с сохранением отличительных черт и естественности. Современные модели не могут точно реконструировать внешний вид заданных предметов, а лишь создают вариации содержания изображения.
## Как формулируется задача?
   Необходимо создать модель, которая по входящим 3-5 изображениям одного и того же объекта будет генерировать его в различных контекстах, связать изображение и текст так, чтобы сохранить уникальные черты объекта и не потерять естественность. 
## В чем ее основная идея?
    В данной работе исследователи представляют новый подход к "персонализации" диффузионных моделей "текст-изображение" (их адаптации к потребностям пользователя при генерации изображений). Цель - расширить языковой словарь модели таким образом, чтобы она связывала новые слова с конкретными темами, которые пользователь хочет генерировать. Для этого предлагается методика представления заданного субъекта с помощью редких токенов-идентификаторов и тонкуая настройка предварительно обученного фреймворка преобразования текста в изображение на основе диффузии. Тонкая настройка модели преобразования текста в изображение осуществляется с помощью входных изображений и текстовых подсказок, содержащих уникальный идентификатор, за которым следует название класса предмета (например, "A [V] dog").
## В чем ее новаторство?
    Это иновационное решение, которое позволяет решить новую сложную задачу генерации изображений на основе субъекта.
    Для предотвращения явления, при котором модель ассоциирует название класса с конкретным экземпляром, предлагается использовать автогенную функцию потерь.
   	Также данный подход позволяет решать множество новых задач: реконтекстуализацию, художественную рендеризацию, синтез новых представлений, модификацию свойств.
## Какие получились результаты?
    Авторы представили пример генерации изображения с несколькими входными изображениями на дополнительном контексте, получилось очень точно все воспроизвести.
   	Был создан датасет, состоящий из 30 различных классов из животных и неодушевленных объектов.
   	Было проведено сравнение результатов с Textual Inversion (единственной сопоставимой работе, которая ориентирована на предмет и текст и генерирует изображения), DreamBooth (Imagen) и DreamBooth (Stable Diffusion). По всем метрикам (DINO, CLIP-I, CLIP-T) результаты DreamBooth (Imagen) оказались более приближены к реальным изображениям.
   	Также авторы говорят об ограничениях данного метода, приводят несколько неудачных примеров генерации. Возможные причины - слабый приоритет для таких контекстов, сложность генерации как предмета, так и заданного понятия вместе из-за низкой вероятности совместного использования. Вторая причина - смешение контекста и внешнего вида, когда внешний вид субъекта изменяется под воздействием контекста подсказки, например с изменением цвета объекта. Третья - чрезмерную подгонка к реальным изображениям, которая происходит, когда подсказка похожа на исходную обстановку, в которой находится объект. Было замечено, что такие предметы, как рюкзак легче поддаются генерации, чем кошки и собаки.

