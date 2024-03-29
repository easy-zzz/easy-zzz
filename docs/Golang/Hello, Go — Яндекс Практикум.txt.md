Hello, Go — Яндекс Практикум

Тема 1/4: История и идеология Go → Урок 1/4

Hello, Go

Итак, вы начинаете своё путешествие в мир Go — поздравляем!

В этой теме вы:

изучите историю возникновения Go;

разберёте особенности языка;

проанализируете задачи и проблемы, которые решает Go;

настроите окружение и напишете первую программу на Go;

узнаете самое главное: почему маскот Go — голубой суслик.

Начнём с главного: откуда взялся голубой суслик? По-английски суслик — gopher. Автор оригинального изображения — иллюстратор и писательРене Френч

, жена Роба Пайка, одного из создателей Go. Изначально она рисовала суслика для промоушена радиостанции WFMU в Нью-Джерси. Спустя несколько лет, когда стартовал проект Go и понадобился маскот, Рене адаптировала рисунок гофера. Так суслик стал талисманом нового языка программирования.

Изначально гофер был светло-коричневого цвета. Но когда решили выпустить мягкие игрушки, первые плюшевые экземпляры покрасили в синий. Так и повелось. Подробнее про гофера можно почитатьв официальном блоге Go

.

Важно знать, что правильное название языка — Go, а не Golang. Второй вариант используют потому, что go — часто употребляемый английский глагол, это затрудняет поиск материалов, относящихся к языку программирования. Из тех же соображений выбирали домен для официального сайта:golang.org

.

Зачем миру понадобился ещё один язык?

Несмотря на то что Go — сравнительно молодой язык (первая версия появилась в 2009 году, а в 2012-м состоялся первый стабильный релиз), потребность в подобном языке возникла на рынке задолго до его создания.

Требования бизнеса к программному продукту начали меняться с появлением интернета. Нужно было создавать веб-страницы быстро, не жертвуя при этом безопасностью. Серверы должны были обслуживать нескольких клиентов одновременно — чем больше, тем лучше. Но железо, которое обеспечивало работу большинства программных продуктов того времени, по-прежнему опиралось на одноядерные процессоры.

С приходом на рынок многоядерных процессоров у разработчиков появилось дополнительное пространство для оптимизации, и новые условия требовали новых подходов к проектированию ПО. В частности, оно должно было поддерживать многопоточность.

Таким образом, при создании нового языка были выдвинуты основные требования и концепции:

Язык должен быть максимально простым для изучения. Действительно, синтаксис Go крайне прост, всего лишь несколько десятков ключевых слов и синтаксических конструкций. Простота языка обеспечивает не только лёгкость освоения, но и снижение количества неявных ошибок.

Управление памятью и сборка мусора. Выделение памяти в Go управляется компилятором в зависимости от контекста. Go автоматически определяет, где требуется разместить переменную — на стеке или в куче, что избавляет от многих ошибок и уязвимостей.

Безопасность. Управление памятью осуществляется планировщиком, в результате чего нельзя выйти за пределы массива.

Безопасные указатели. В Go отсутствует арифметика указателей, к которой привыкли пользователи С/С++. Указатель только может указывать на некоторый объект, нельзя создать указатель на произвольный объект памяти.

Реализация ООП без наследования уменьшает сложность программ.

Отсутствие механизма исключений — также намеренно. Это позволяет упростить отладку программ.

Быстрая компиляция, позволяющая оперативно выполнять разработку сложных программ.

Встроенный инструментарий тестирования, сетевые возможности.

Нет средств обобщённого программирования и перегрузки функций. Это позволяет как ускорить компиляцию, так и снизить количество ошибок.

В первую очередь язык Go ориентирован на создание микросервисов — небольших программ, взаимодействующих друг с другом. 

Теперь давайте углубимся в Go — и начнём с достоинств.

Простота языка

За счёт своего объёма Go считается самым простым типизированным языком. В нём меньше пятидесяти ключевых слов, и разработчики следят за тем, чтобы новые элементы не появлялись без надобности. Например, версия 1.18, вышедшая в марте 2022-го, принесла первое изменение языка за 12 лет — новую конструкцию типизированных параметров.

Как доказательство, Go способен использовать одно ключевое словоforдля любых итераций:

Низкий риск ошибок

Из-за своей простоты и строгой типизации Go исключает большое количество ошибок на этапе разработки. К тому же в нём есть встроенный сборщик мусора, благодаря которому разработчики могут забыть про контроль и очистку памяти, которыми активно занимаются в C или C++.

Лёгкое чтение библиотек

Go полностью написан на Go. Любой разработчик, знающий этот язык, может с лёгкостью прочитать его стандартную библиотеку и понять, как всё работает. В самой библиотеке вы не встретите сложных моментов и даже сможете подсмотреть варианты обработки многопоточных сценариев.

Работа с горутинами и каналами

Горутины позволяют сделать любую функцию асинхронной. Другими словами, какую бы функцию ни написал разработчик, её можно запустить в фоновом режиме, и она будет работать. В то же время планировщик Go сам распределит нагрузку по ядрам, чтобы каждое из них было эффективно нагружено.

Запустить горутину так же просто, как вызвать функцию: нужно поставить ключевое словоgoперед вызовом.

Каналы позволяют передавать и синхронизировать данные между горутинами так, чтобы одни и те же байты не попадали в две разные горутины.

Для создания канала используется встроенная функцияmake:

И раз уж речь зашла о каналах, логично будет разобрать, как устроена многопоточность в Go.

Многопоточность

Что такое «поток» в контексте операционной системы?

Поток выполнения (native/kernel thread)— это часть процесса, в которой инструкции могут выполняться независимо и иметь доступ к общим ресурсам. За управление потоками отвечает планировщик ОС.

Многопоточность— свойство железа и софта, при котором несколько потоков могут выполняться параллельно, не мешая друг другу. Если разработчики ПО сумели эффективно распараллелить отдельные части программы, можно рассчитывать на увеличение производительности, кратное количеству доступных ядер процессора.

Но для реализации работы нескольких потоков требуется как аппаратная поддержка, так и программная. Под аппаратной подразумевается наличие выделенных ядер в процессоре под каждый поток ОС (по два сhyper-threading

), под программной — поддержка многопоточности ОС и конструкциями языка. Поэтому необходимость в разработке многопоточного софта возникла только в нулевых, когда рынок начали захватывать многоядерные процессоры:

Как видно из графика, в наши дни производители процессоров стали наращивать количество вычислительных ядер вместо рекордных показателей тактовой частоты одного ядра. Эффективно использовать такие процессоры могут только многопоточные вычисления.

Один из первых нюансов, с которым сталкиваются разработчики при проектировании многопоточного ПО, — организация доступа к общим ресурсам, а конкретно — к памяти. Неверное разделение доступов между потоками может привести к порче данных. Например, если два потока одновременно и параллельно пишут своё значение в одну и ту же переменную, какое из значений будет записано в результате? Да и в целом необходимость мыслить несколькими потоками осложняет понимание процесса выполнения программы.

Средствами языка разработчикам хотелось избавиться от головной боли, которая может возникнуть при переходе на многопоточное программирование. Разные языки предлагали разные решения этой проблемы, но так как большинство существовавших на тот момент языков создавались без учёта многопоточности, её поддержку приделывали «сбоку».

В интерпретируемых языках программирования, занимавших львиную долю рынка того времени, были дополнительные сложности. Нужно было организовать механизмы обращения к глобальному состоянию интерпретатора из нескольких потоков и обмен данными между этими потоками. Стало понятно, что необходим новый язык программирования, который бы был изначально создан с расчётом на многопоточность и позволял быстро и удобно писать приложения, использующие доступные ядра процессоров.

Для эффективного использования доступной вычислительной мощности и потоков ввода/вывода Go оперирует несколькими системными потоками, распределяя между ними ещё больше своих собственных легковесных потоков со стратегиейm*n. То есть на одном системном потоке могут исполняться несколько горутин. Если системный поток блокирован ожиданием ввода/вывода или перегружен, диспетчер Go может перенести горутину на свободный. Если захваченных системных потоков недостаточно, диспетчер Go может потребовать у системы новых.

Как Go ответил на вызовы рынка?

Возможность спроектировать язык с нуля позволила на фундаментальном уровне внедрить многие решения, чтобы разработчики могли писать многопоточный код. Существуют разные модели многопоточных вычислений, среди которых архитекторы Go выбрали модельCSP (Communicating Sequential Processes), описанную Энтони Хоаром в одноимённой статье. В этой модели программа представляет собой множество одновременно работающихподзадач, которые общаются между собой, передавая сообщения черезканалы связи.

Подзадача в Go называетсягорутиной. Горутины живут в прослойке между программой и средой выполнения под названиемruntime. Помимо прочего, рантайм отвечает за организацию конкурентного доступа множества горутин к общему ограниченному ресурсу — процессорному времени. Его задача — распределить этот ресурс так, чтобы каждая горутина смогла поработать хотя бы какое-то время, прежде чем управление перейдёт к следующей. Таким образом достигается иллюзия параллельности выполнения задач при количестве горутин, многократно превышающем количество доступных системных потоков.

В отличие отevent loop, код горутины пишется и выглядит последовательным и самостоятельным, без всякихcallback-вызовов, как в случае с горутиной в виде отдельной программы. 

Горутины пишутся и выполняются как самостоятельные потоки вычислений, но для большей совместной эффективности горутины могут взаимодействовать между собой, обмениваясь сообщениями. Каналом связи для передачи сообщений в Go выступает такая абстракция, какchannel(канал). На каналах построены все механизмы обмена и синхронизации потоков в Go.Канал— это подобие туннеля, в который одна горутина может «положить» значение, а другая — это значение оттуда «вытащить» и что-нибудь с ним сделать.

Обе абстракции — не подключаемые библиотеки или фреймворки, а встроенные конструкции синтаксиса, которые автоматически становятся одной из «киллер-фич» языка и большим преимуществом для программиста. В этом плане Go сильно оторвался от конкурентов.

Например, в популярном языке Python ближайшим аналогом горутин можно считать классProcess, а функциюPipe()из модуляmultiprocessingстандартной библиотеки — аналогом канала. Разница в том, что в Python многопоточность не реализована в базовом синтаксисе, иProcessзахватывает тяжеловесный системный процесс полностью в единоличное пользование. Лёгкие потоки с дешёвым переключением контекста симулируются в Python классомThreadиз модуляthreading. НоThreadв эталонной реализации CPython не добавляет параллелизма и не умеет использовать все ядра процессора. Одновременно может исполняться только одинThread, поэтому каналы обмена данными междуThreadпросто не нужны.

Горутины и каналы детально рассматриваются в курсе «Go-разработчик». Нам же пора возвращаться к преимуществам Go.

Самодостаточность

Go компилируется статически: когда разработчик написал программу и скомпилировал её, она помещается в один бинарник, который содержит все зависимости. Можно скомпилировать программу под нужную операционную систему и запускать её на любом компьютере с такой же ОС. Работа с Python или C++ потребует множества дополнительных файлов вроде интерпретаторов и библиотек.

Активное развитие

Ещё одна фишка Go — обратная совместимость версий, илиBackward Compatibility Promise. Даже если вы писали код на старой версии языка, новая обработает его без проблем. Этим объясняется высокий adoption rate у новых версий Go.

Однозначность синтаксиса и форматирования

Язык наглядно указывает, как нужно форматировать код, а за счёт регламентированного расположения скобок и переносов практически все компании, использующие Go, имеют похожий стиль кода. Это позволяет быстро разобраться в чужом коде, к примеру, новым разработчикам. Кроме того, в Go нельзя объявить и не использовать переменную — возникнет ошибка.

Субъективные недостатки Go

Было бы несправедливо рассмотреть только преимущества языка Go, не упомянув субъективные недостатки из опыта создателей курса.

Невозможно управлять памятью

Go управляет памятью автоматически. Встроенный сборщик мусора справляется хорошо, но в руках живого человека расход памяти сократится и будет более предсказуемым.

Неудобные моменты с библиотекой

В работе со стандартной библиотекой есть спорный момент — это язык шаблонизации и директивы форматирования дат. По сравнению с Java и C метод Go выглядит сомнительно:

Собственно, как и код:

Не хватает «батареек» из Python

Иногда в языке не хватает того, что в Python называется «батарейками», — отдельных элементов стандартной библиотеки, в которых есть всё для решения распространённых задач. В Go, например, нет встроенных базовых структур вродеdecimalи удобных функций для работы с массивами, что легко объяснить «подростковым» возрастом языка. Повзрослеет — и наберёт инструментов.

Нет тернарного оператора

В Go нет тернарного оператора, то есть возможности одной строкой проверить, является ли элементtrueилиfalse.

Например, так выглядит проверка на PHP:

Небольшая замусоренность

Этот недостаток связан с обратной совместимостью версий, преимуществом языка, которая способствует образованию некоторого мусора. Если разработчики понимают, что они плохо написали функцию или в стандартной библиотеке появилась новая единица, им приходится писать новые функции — похожие на старые, но с новыми фичами. Получается, что в Go можно встретить функции-близнецы, которые делают похожие вещи, имеют одинаковые имена, при этом от старой функции вы не можете избавиться, потому что где-то находится связанный с нею код.

Всё не просто так

Итак, теперь понятно, почему возник спрос на язык вроде Go и какие абстракции он предлагает для написания многопоточного кода. Но откуда создатели знали, чтоCSP-модельтак удачно приживётся в их языке? Чтобы ответить на этот вопрос, мысленно переместимся назад во времени — в середину 1980-х.

Plan 9

Компания Bell Labs создала свою собственную операционную систему для разработчиков под названиемPlan 9. Её разработкой занималась та же команда, что ранее создала С и Unix. Среди них выделялись два очень важных человека — это Роб Пайк и Кен Томпсон. Спойлер: они же в 2007 году приступят к разработке нового языка, который 10 ноября 2009-го увидит свет под именем Go.

Сама по себе Plan 9 не так интересна, как входящий в неё Alef — компилируемый язык на С-подобном синтаксисе, концепция которого строилась вокруг параллельного и конкурентного программирования. Под «параллельными» здесь стоит понимать вычисления, происходящие одновременно (например, на разных процессорных ядрах). Под конкурентным программированием — способ описания вычислений в нескольких потоках, которые конкурируют за системный ресурс: память, вычислительные такты, устройства ввода/вывода.

Plan 9 предлагала модель обмена данными через каналы, даже синтаксически очень похожую на модель в Go. Также был сделан упор на буферизованный ввод/вывод, несколько возвращаемых значений в функциях и необычное ООП, отдалённо напоминающее то, что реализовано в Go. При этом в одной из поздних версий были добавленыдженерики. В отличие от Go, Alef не имел сборщика мусора.

Newsqueak

Модель конкурентного и параллельного программирования была позаимствована у языка под названиемNewsqueak. Авторами Newsqueak в первой половине 1980-х выступили Лука Карделли и Роб Пайк. Сам Пайк называет язык «игрушкой», но уточняет, что работа над ним помогла понять, как реализуется CSP-модель параллелизма на практике.

Limbo

В середине 1990-х, после того как Plan 9 прохладно встретили в сообществе разработчиков, Bell Labs перебросила силы на создание новой операционной системы —Inferno. Она разрабатывалась как идейный наследник философии Plan 9, а в числе разработчиков вновь оказался Роб Пайк. Основным языком, на котором писались программы для Inferno, был специально разработанный для этогоLimbo.

В отличие от Alef, в языке Limbo исходный код не компилировался, а транслировался в байт-код. Виртуальная машина служила прослойкой, запускающей этот байт-код, и она же выступала сборщиком мусора и планировщиком для запущенных программ. Также в Limbo внедрили модули,слайсыи некоторые синтаксические конструкции, которые позже перекочевали в Go. В поздних версиях Limbo появились дженерики, но они работали в ограниченном режиме и поддерживали не все типы данных — подружитьсборщик мусора, многопоточность и дженерики оказалось крайне непростой задачей. Сам Роб Пайк называет Limbo прямым предком Go.

libthread

Inferno не взлетела и была продана Vita Nuova, а в 2000 году вышла новая версия Plan 9. Поддерживать Alef становилось всё сложнее, поэтому было решено переписать часть функционала на С. Так появилась библиотека лёгких (не системных) потоков исполненияlibthread. Она также строилась на концепции обмена данными через каналы.

Три знающих человека

По мере изучения материалов и публикаций о предыдущих проектах Роба Пайка становится понятно, что Go получился таким, какой он есть, отнюдь не просто так. В нём намеренно упрощены синтаксические конструкции, а включение дженериков оттягивали до последнего вовсе не потому, что создатели не знали об их существовании. Кстати, дженерики появились в Go 1.18 в начале 2022 года, о чём официальнообъявили в сети

.

Философия, которой следует Go, формировалась в течение многих лет, а конструкции и подходы, применяемые в языке, были проверены годами использования (в том числе промышленного) в языках-предшественниках — Alef, Newsqueak и Limbo. 

Подводя итог, можно сказать, что Go добился успеха в результате стечения обстоятельств: миру понадобилась технология, а Роб Пайк, Кен Томпсон и Роберт Гризмер уже знали, как её разработать.

Go Proverbs

Примите с долей юмора — в Go, как и везде в IT, действуют шаманские заклинания. Самые важные собраны — в основном со слов Роба Пайка — на особойстраничке

. Вот их вольный перевод:

Избегайте коммуникаций через общую, разделённую память. Наоборот, делитесь данными в памяти через сообщения.

Конкурентность и параллелизм — это не одно и то же.

Каналы для взаимодействия, мьютексы для разобщения.

Чем сложнее интерфейс, тем ненадёжней абстракция.

Нулевые значения полезны не меньше других.

Пустой интерфейсinterface{}не о многом скажет.

У всех есть свой годный стиль форматирования кода, стандартное форматированиеgofmt— годное для всех.

Копирование лучше зависимостей.

Защищай системные вызовы в коде тегами сборки.

Защищай кросс-вызовы cgo к коду C тегами сборки.

Cgo — это не Go.

Применяя пакетunsafe, не рассчитывай на какие-либо гарантии.

Лучше ясно, чем красиво.

Интроспекция ясной не бывает.

Значения ошибок — это тоже значения.

Недостаточно отлавливать ошибки, нужно их обрабатывать.

Полируй архитектуру, внятно называй компоненты, документируй детали.

Документация — для пользователей.

Не паникуй.

Hello, Go

Куда же безHello, который на Go выглядит вот так:

Чтобы запустить этот код или попробовать любой другой, можно сходить вoнлайн-песочницу

. 

В следующих уроках расскажем, как поднять среду разработки на Go на локальной машине. Если же вам понадобится быстрый результат и будет неохота запускать окружение, сниппеты кода из уроков или свои заготовки — песочница к вашим услугам.

Полезные ссылки

Официальный сайт

Oнлайн-песочница

Robert Griesemer. Go for C programmers
