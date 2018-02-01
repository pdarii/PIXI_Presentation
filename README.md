PIXI.js

СЛАЙД 1

Pixi - це надзвичайно швидка 2D движок для рендеринга  спрайтів. 
Що це означає?

Це означає що вона допомогає нам відображати, анімувати та працювати з інтерактивною графікою, і нам досить легко робити ігри та додатки використовуючи JS та інші технології HTML5.

Вона досить

У неї досить нормально описана апішка та багато функцій, на зразок підтримки атласів структур та  вдосконалена система анімації спрайтів (інтерактивних зображень).

Вона також дозволяє робити ієрархії спрайтів( спрайтів в середині спрайтів ), а також вішати лістенери миші та тачу - напряму на спрайти. 

І, найважливіше, PIXI ніочго не нав*язує, можна використовувати рівно стільки функціонала цієї ліби, скільки треба, підганяти під свій стиль кодінга, і інтегрувати її разом з іншими фреймворками.

По суті апішка PIXI - це вишукані, добре відомі та перевірені часом API - які ще колись розроблялись в Macromedia/Adobe Flash.

Як написано на гітхабі - Олд скульні Flash девелопери, будуть почувати себе як вдома. 

Сила PIXI - в тому що вона загального призначення, це не ігровий движок, за рахунок цього ми маємо свободу робити на ньому що завгодно.


СЛАЙД 2

Установка PIXI

СЛАЙД 3

Базова сторінка з PIXI

<!doctype html>
<html>
<head>
  <meta charset="utf-8">
  <title>Hello Pixi</title>
</head>
  <script src="pixi.min.js"></script>
<body>
  <script type="text/javascript">
    let type = "WebGL"
    if(!PIXI.utils.isWebGLSupported()){
      type = "canvas"
    }

    PIXI.utils.sayHello(type)
  </script>
</body>
</html>


Тепер можна юзати PIXI

Спочатку створимо прямокутник - щоб реально бачити де ми можем виводити наші картинки. Pixi має Applicationobject який робить це для нас, він автоматично створює елемент HTML <canvas> і знає як відображати на ньому зображення. 
Нам потрібно створити спеціальний об*єкт - контейнер який називається stage. 

СЛАЙД 4

Stage - є root контейнером, який буде тримати всі речі - які PIXI буде відображати для нас.
Щоб створити Stage - треба написати настуний код:

СЛАЙД 5

Це найпростіший базовий код, який треба написати щоб почати юзати Pixi. Він створить канвас розміром 256 на 256 пікселей. Та додасть його в наш HTML документ.

//Create a Pixi Application
let app = new PIXI.Application({width: 256, height: 256});

//Add the canvas that Pixi automatically created for you to the HTML document
document.body.appendChild(app.view);

Покажи в едіторі.

Да, це чорний квадрат) 

PIXI вирішує використовувати Canvas Drawing API чи WebGL щоб рендерити графіку, звичайно це залежить що підтримує браузер. 


СЛАЙД 6

Конструктор Pixi приємає як аргумент
об*єкт з опціями на зразок розмірів, налаштувань згладжування і т.д.

Antialias згладжує края фонтів та графічних примітивів.
Transparent робить canvas background прозорим. resolution полегшує роботу з дісплеями різної роздільної здатності та густини пікселей. Для нашого проекту ми залишимо її 1.

СЛАЙД 7

Всі опції можна подивитись тут:
http://pixijs.download/release/docs/PIXI.Application.html


СЛАЙД 8

По дефаулту Pixi намагається завжди використовувати WebGL, це добре - тому що WebGL дуже швидкий, і на ньому можна робити дуже круті еффекти, але якщо треба саме Canvas - то можна передати параметр forceCanvas true.

СЛАЙД 9

Якщо треба змінити колір бекграунда канви після її створення - можна змінити параметр 
Обєкту app.renderer backgroundColor на HEX значення кольору.

СЛАЙД 10

Якщо потрібно знайти ширину або висоту Рендерера
Можна юзати
app.renderer.view.width та app.renderer.view.height.

СЛАЙД 11

Щоб змінити розмір канвасу - у рендерера є метод Resize, але щоб канва нормально ресайзилась і не було проблем з роздільною здатністю - потрібно рендереру задати 
autoResize true.

СЛАЙД 12

Якщо ми хочемо щоб Canvas заповнив весь екран - то можна задати розміри через CSS, та заресайзити рендерер до розміру вікна браузера:


СЛАЙД 13

Pixi sprites

Тепер у нас є Renderer, можем починати додавати в нього картинки. Все що ми хочем щоб було видиме в рендерері - має бути додано на спеціальний об*єкт Stage:

СЛАЙД 14

app.stage

Stage це об*єкт  Pixi Container, загалом container це щось на зразок пустої коробки в якій ми будемо групувати разом та зберігати все що ми додамо в неї.

Stage - це рут контейнер для всіх видимих речей які ми додали. Що б ми не додали на stage - воно буде відрендерено на канвасі. Зараз наш Stage порожній, але зараз ми туди ще накидаєм добра.

ВАЖЛИВО - так як Stage це об*єкт Pixi Container - вона має ті самі проперті та методи як і інші Containerobject. Але хоч stage і має width і height - вони не відносяться до розміру вікна. Розмір Stage - лиш означає розмір місця зайнятого об*єктами - які ми на ній розмістимо.

Ок, що ми можем розмістити на Stage - наприклад спеціально об*єкти( картинки ) які називаються спрайтами. По суті спрайти це прості картинки які ми можем контролювати з нашого коду. 

Ми можемо контролювати їхню позицію, розмір та інші проперті, які нам стануть в пригоді при побудові графіки.

Навчитись робити та контролювати спрайти - це найважливіша річ при вивченні Pixi. Якщо ми знаєм як робити спрайти та додавати їх на Stage, то ми в маленькому кроці від старту розробки ігор.

СЛАЙД 15

Pixi має досить гнучкий клас Sprite, є 3 основні способи їх створити:
1. З картинки
2. З саб картинки з tileset.   Tileset це велика картинка в якій склеєні всі картинки які нам необхідні.
3. З Атласу текстур ( JSON файл який визначає розміри та позиції картинок на tileset)


СЛАЙД 16

Так як Pixi рендерить картинки на GPU за допомогою WebGL, картинки повинні бути в потрібному форматі щоб GPU міг з ними працювати. WebGL-ready картинка називається текстурою.

До того як спрайт відобразить картинку, нам потрібно конвертнути картинку в WebGL текстуру.

Щоб все працювало швидко та еффективно, Pixi використовує texture cache зберігати та мати ссилки на всі текстури які необхідні для наших спрайтів.

СЛАЙД 17

Імена текстур  збігаються з розташуванням файлу для зручності. Це означає що якщо ми загрузили картинку з "images/cat.png" то ми можем отримати до неї доступ:

PIXI.utils.TextureCache["images/cat.png"];

Щоб зробити новий спрайт з текстури можна використати наступний код:

СЛАЙД 18

let texture = PIXI.utils.TextureCache["images/anySpriteImage.png"];
let sprite = new PIXI.Sprite(texture);


Щоб загрузити картинку і  конвертнути її в текстуру ми використаємо загрузчик PIXI.

СЛАЙД 19

PIXI.loader
  .add("images/anyImage.png")
  .load(setup);

function setup() {
  //This code will run when the loader has finished loading the image
}


Розробники  PIXI рекомендують юзати лодер таким чином: - щоб ми створювали спрайти з ссилок в об*єкті лоадера. Ось приклад завантаження картинки та створення текстури:

СЛАЙД 20

PIXI.loader
  .add("images/anyImage.png")
  .load(setup);

function setup() {
  let sprite = new PIXI.Sprite(
    PIXI.loader.resources["images/anyImage.png"].texture
  );
}

СЛАЙД 21

Також можна грузити багато картинок за допомогою чейнінга.

Але краще просто передавати масив картинок.

СЛАЙД 22


СЛАЙД 23


Відображення спрайтів

Після того як ми завантажили картинку та створили з неї спрайт, нам потрібно додати цей спрайт на Stage, робиться це так:

СЛАЙД 24

Покажи в едіторі.


//Create a Pixi Application
let app = new PIXI.Application({ 
    width: 256, 
    height: 256,                       
    antialias: true, 
    transparent: false, 
    resolution: 1
  }
);

//Add the canvas that Pixi automatically created for you to the HTML document
document.body.appendChild(app.view);

//load an image and run the `setup` function when it's done
PIXI.loader
  .add("images/cat.png")
  .load(setup);

//This `setup` function will run when the image has loaded
function setup() {

  //Create the cat sprite
  let cat = new PIXI.Sprite(PIXI.loader.resources["images/cat.png"].texture);
  
  //Add the cat to the stage
  app.stage.addChild(cat);
}

СЛАЙД 25

СЛАЙД 26


Щоб ремувнути спрайт є метод 
app.stage.removeChild(anySprite)

Але зазвичай  щоб сховати спрайт простіше та більш ефективно буде викоистати 

anySprite.visible = false;

СЛАЙД 27

Використання аліасів

Щоб зробити код більш читаємим PIXI радить робити короткі аліаси з основних об*єктів і методів Та використовувати їх.

Це не тільки дозволить нам писати більш читаємий код, але є ще бонус, PIXI досить часто може оновлювати API, і нам не доведеться кожеш раз щось міняти в багатьох місцях. 

СЛАЙД 27

Отже перепишемо наш код з аліасами: 

Покажи в едіторі.

//Aliases
let Application = PIXI.Application,
    loader = PIXI.loader,
    resources = PIXI.loader.resources,
    Sprite = PIXI.Sprite;

//Create a Pixi Application
let app = new Application({ 
    width: 256, 
    height: 256,                       
    antialias: true, 
    transparent: false, 
    resolution: 1
  }
);

//Add the canvas that Pixi automatically created for you to the HTML document
document.body.appendChild(app.view);

//load an image and run the `setup` function when it's done
loader
  .add("images/cat.png")
  .load(setup);

//This `setup` function will run when the image has loaded
function setup() {

  //Create the cat sprite
  let cat = new Sprite(resources["images/cat.png"].texture);
  
  //Add the cat to the stage
  app.stage.addChild(cat);
}


СЛАЙД 28

СЛАЙД 29

Трохи більше про загрузку.

Формат який ми розглядали - це стандратний формат загрузки картинок, але є ще декілька.

Можна зробити спрайт з звичайного JavaScript Image object або Canvas

Для оптимізації та еффективності завжди краще робити спрайти з текстур які вже були загружені в кеш текстур Pixi’s, але якщо з певних причин - нам необхідно використати JavaScript Image object - ми можемо зробити це:

СЛАЙД 30

Якщо необхідно змінити текстуру спрайту який вже показується - це теж можливо.

СЛАЙД 31

Це можна використовувати щоб інтерактивно міняти спрайти - якщо щось важливе відбувається в грі.

СЛАЙД 32

Також можна приасайнити унікальне ім*я для кожної картинки що ми завантажуємо.
( Розробники радять не юзати цю фічу. Тому що можна забути чи переплутати ім*я, а шлях є шлях)

СЛАЙД 33

Моніторинг процесу завантаження

Загрузчик PIXI має спеціальний івент, який викликає певні функції кожен раз коли файл завантажується.

Виглядає це ось так:

СЛАЙД 34


PIXI.loader
  .add([
    "images/one.png",
    "images/two.png",
    "images/three.png"
  ])
  .on("progress", loadProgressHandler)
  .load(setup);

function loadProgressHandler() {
  console.log("loading"); 
}

function setup() {
  console.log("setup");
}


Це звичайно круто, але можна навіть краще.


СЛАЙД 35

Насправді у лодера є багато фіч, але всі я не встигну перечислити.


СЛАЙД 36

Позиціювання спрайтів

cat.x = 96;
cat.y = 96;


function setup() {

  //Create the `cat` sprite
  let cat = new Sprite(resources["images/cat.png"].texture);

  //Change the sprite's position
  cat.x = 96;
  cat.y = 96;

  //Add the cat to the stage so you can see it
  app.stage.addChild(cat);
}

Покажи в едіторі.



СЛАЙД 37

Також можна задати позицію через сеттер

СЛАЙД 38

Розмір та скейл

Покажи в едіторі.


function setup() {

  //Create the `cat` sprite
  let cat = new Sprite(resources["images/cat.png"].texture);

  //Change the sprite's position
  cat.x = 96;
  cat.y = 96;

  //Change the sprite's size
  cat.width = 80;
  cat.height = 120;

  //Add the cat to the stage so you can see it
  app.stage.addChild(cat);
}

СЛАЙД 39

Скейл це числа від 0 до 1, які відповідають за відсоток від розміру спрайту. 1 - значить 100%,
0.5 - 50%.


СЛАЙД 40

Поворот

Поворот спрайту можна задати через атрибут rotation, він в радіанах.

По замовчуванню точка навколо якої повертається спрайт - це точка ху

Але її можна змінити:

СЛАЙД 41

anchor.x та anchor.y відображають у відсотках розмір спрайту, від 0 до 1 (0% to 100%). Якщо ми задамо 0.5, спрайт буде крутитись навколо центральної точки.


СЛАЙД 42

Спрайт з tileset 

Весь  tileset  192 на 192 pixels

The entire tileset is 192 by 192 pixels. Each image is in its own 32 by 32 pixel grid cell. Storing and accessing all your game graphics on a tileset is a very processor and memory efficient way to work with graphics, and Pixi is optimized for this.
You can capture a sub-image from a tileset by defining a rectangular area that's the same size and position as the sub-image you want to extract. Here's an example of the rocket sub-image that’s been extracted from the tileset.

































































































































