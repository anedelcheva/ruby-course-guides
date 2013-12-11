В този документ ще събираме някои указания, които да ви насочат в избора на тема и в писането на вашите проекти към курса ["Програмиране с Ruby"](http://fmi.ruby.bg/).

### Игри и друг GUI intensive софтуер

Когато сте избрали да пишете неща, наподобяващи игри — или каквито и да е други проекти, изискващи сериозно GUI — постарайте се да "откачите" основния си код максимално много от рисуването/графиката/GUI-то. Целта ви е да имате много ясно разделение и абстракция между "ядрото" на вашия проект и графичния му интерфейс. Добре би било основната логика на проекта ви да се намира изцяло в "ядрото", под формата на класове, модули и прочее, като това ядро предоставя на своите позлватели някакво API. Тоест, стремите се да пишете въпросното ядро все едно пишете библиотека, която ще се преизползва в друг(и) софтуер(и). От там нататък, GUI-то се прави като wrapper на тази библиотека, ползва публичното й API и е един вид pluggable компонент към нея.

Можете да минете и само с кода от основното ядро, който имплементира функционалност без GUI, ако сте писали обилно тестове. Този проект е подходящ шанс за вас да пробвате подхода TDD. Допълнително, това ще ви помогне да покриете едно от изискванията, а именно да имате пълно покритие с unit тестове.

GUI-то е добре да е съвсем просто и може да минете без особено тестване там, освен, евентуално, някой друг инреграционен тест. Може да минете и с най-просто и дървено конзолно GUI, което е тънка обвивка около API-то на "ядрото". Ако сте запалени, може да направите повече от едно GUI. Последното е възможно да ви донесе бонус точки :)

### Rails проекти – забранени

Базирайки се на трагичния опит с ваши Rails проекти от минали години, сме принудени за ваше добро да ви забраним да правите такива проекти.

Причината за това е, че Rails сам по себе си е много сложен и за правилната му, канонична употреба, се изисква да положите усилия, които се равняват на още един едносеместриален курс. Ако не сте се занимавали с уеб програмиране преди това, нещата се усложняват допълнително. Rails е още една голяма и сложна абстракция, която трябва да научите прилично, за да става проектът ви за нещо, а това усложнява нещата неимоверно много.

Разбира се, имали сме няколко случая на сносни Rails проекти. Студентите, които са ги направили, са:

- имали предварителен опит с и силен интерес в областта на уеб програмирането
- се справяли добре с курса по Ruby и са овладели предварително достатъчно добре самия език
- прекарали в продължение на месеци множество часове – безсънни нощи и уикенди – в борба с Rails

Всичко останало е обречено на провал.

Ето ви един конкретен пример за възможна грешка (каквито изобилстваха в почти всички Rails проекти), произтичаща от сложността на Rails – ако сте ползвали `<form>`-тагове, за да направите форма, която не е пряко свързана с Rails модел, вместо да ползвате `form_tag` view helper-а (понеже вероятно не сте знаели, че има такова нещо). В Rails има много неща (както и в Ruby, между другото), така че се налага да проверявате за почти всичко, преди да тръгнете да си го пишете сами, какви готови решения се предлагат вече от фреймуърка и да прецените дали това решение е окей или не ви върши работа. Да, не е проблем да ползвате таг `<form>`, ако сте видели, че има `form_tag`, но, поради някаква причина, той не ви върши работа.

#### Уеб приложения на Sinatra – окей

За тези от вас, които са фенове на уеб програмирането и искат да направят такъв проект за курса си по Ruby, ви даваме алтернатива – може да ползвате нещо като Sinatra, или друг минималистичен уеб фреймуърк. Пак ще се налага да опознаете из основи това, на което стъпвате (например, Rack и Sinatra), но това е задача, която е в пъти по-малка и обозрима, от това да научите добре Rails.

### Създаване на Ruby библиотеки

Да си направите собствена Руби библиотека е безплатно и не особено трудно. Като начало, запознайте се с няколко кратки ръководства, намиращи се на [guides.rubygems.org](http://guides.rubygems.org/):

1. [What is a gem?](http://guides.rubygems.org/what-is-a-gem/)
2. [Make your own gem](http://guides.rubygems.org/make-your-own-gem/)
3. [Patterns](http://guides.rubygems.org/patterns/)

[Описанието на gemspec-формата](http://guides.rubygems.org/specification-reference/) може също да ви е полезно, докато правите gem. Ще ви трябва безплатен акаунт на [rubygems.org](http://rubygems.org).

### Архитектура на вашето приложение и мислени ограничения

Ограниченията са причина хората да проявяват изобретателност.

Поставете си следното ограничение - представете си, че правите проекта си в Ruby gem. Представете си, че го правите така, че клиентът му ще бъде друг Ruby код и че не трябва да мислите за потребителски интерфейс, графичен интерфейс, уеб интерфейс... Помислете как може да моделирате вашата _бизнес логика_ и да разделите кода си на модули и файлове по начин, подходящ за вашата предметна област, без да се съобразявате със структура, наложена от Rails, Sinatra, Ruby Tk или каквото и да е друго. Не се притеснявайте да правите повечко файлове и папки, стига това да се вписва добре в модела ви.

Накрая може да ползвате вашия gem в Rails, или Sinatra, или Ruby Tk, или нещо друго, написвайки малко код и малко интеграционни тестове, за да проверите, че **интеграцията** ви със съответния GUI фреймуърк работи. И трябва въпросното GUI да е тънък слой върху вашата библиотека, а не вашата библиотека да е тънък слой върху Rails, да кажем.

Ако дойдете при нас само с Ruby gem и добри unit тестове, може да получите пълен брой точки. Ценим unit тестовете най-много за тези проекти и може да минете и без интеграционни такива, ако нямате интеграция с външи компоненти.

Гледайте това [видео от презентация на "чичо Боб Мартин" по повод архитектурата на приложения и Rails](http://youtu.be/WpkDN78P884). То се отнася и до проекти, които не са уеб или Rails. По-конкретен пример за това как бихте могли да реализирате на практика идеите, за които Боб Мартин говори в презентацията си, може да намерите в статията на Виктор Савкин ["Building Rich Domain Models In Rais. Separating Persistance."](http://victorsavkin.com/post/41016739721/building-rich-domain-models-in-rails-separating) Архитектурата, предложена и реализирана по-горе, е до известна степен крайна и доколко е подходяща за даден проект е обект на дискусия. От друга страна, тя е много изчистена и за целите на курсовия проект е много добро упражнение.

### Version control

Изискването да се ползва система за контрол на версиите не сме го споменавали изрично, но смятаме, че се подразбира и че всички сте наясно. Задължително е. Силно препоръчваме да ползвате Git и GitHub. Няма проблем кодът на проекта да ви е публичен. Ако все пак държите да ползвате друга version control система, пак ще приемем това изискване за покрито. Важното е да има някакъв version control.

### Размер и сложност на проекта

Ако една задача в курса ви носи 6 точки, едно предизвикателство една точка, а един проект — 60, може да направите грубата сметка колко сложен трябва да е проектът. Осланяме се на вашата честност и ви оставяме сами да прецените това.

Като цяло, проектът не трябва да е нещо, което да може да се напише за едно или две денонощия. Може да се наложи да си измислите и да вкарате още функционалност, за да покриете това изискване за сложност. Преценката за това какво е "достатъчна сложност" засега остава във вашето поле. Изисквания за функционалност могат да се измислят винаги, така че може да се приеме, че сложността на дадена идея никога не е ограничена отгоре. Тоест, каквато и да е идеята ви, може да добавяте и да добавяте функционалност, докато не се получи нещо с "достатъчна сложност".

В крайна сметка, ако не се опитвате _просто да напишете нещо_, което да ви "прекара" през курса, а пишете проекта с цел да пробвате и научите нови неща и подходите сериозно, няма да имате проблем.

Започнете навреме.