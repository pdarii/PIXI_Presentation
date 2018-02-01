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

Весь  tileset  192 на 192 pixels, кожна картинка 32 на 32 pixel. Зберігати та мати доступ до всієї ігрової графіки на тайлсеті - дуже ефективно для процесора та пам*яті, до тогож PIXI оптимізована для цього.
Ми можемо взяти саб імадж з тайлсету вказавши прямокутну область - з координатами та розміром картинки яка нам необхідно:

СЛАЙД 43

Texture atlas

Якщо працюєш над великою та складною грою - то потрібний швидкий та еффективний спосіб створювати спрайти з тайосетів. В цьому випадку - атлас текстур дуже виручає. 
Атлас текстур - це JSON файл - який містить позиції та розміри суб картинок з певного тайлсету. Якщо ми використовуємо атлас - то все що нам треба знати про картинку щоб її показати - це її ім*я. 
Можна сортувати тайлсет картинки в будь-якому порядку - і JSON файл буде слідкувати за їхніми розмірами та позиціями за нас. Це дуже зручно - так як розміри та позиції картинок не захардкожені в грі чи программі.
Якщо ми робим зміни в тайлсеті, наприклад додаєм картинки, ресайзимо їх чи видаляєм - просто треба перезібрати JSON файл і гра буде використовувати нові данні щоб відображати картинки корректно. В коді нічого міняти не доведеться

PIXI сумісна з стандартним  JSON texture atlas format який вміє пакувати популярна тулза Texture Packer, який є фрішним.

СЛАЙД 44

СЛАЙД 45

Завантаження texture atlas

Щоб завантажити texture atlas в Pixi, ми використовуєм стандартний лоадер. Якщо JSON був згенерований за допомогою Texture Packer,
він автоматично інтерпретує данні, і створить текстури з кожного тайлсету автоматично.

СЛАЙД 46

Тепер кожна картинка з тайлсету - це індивідуальна текстура в кеші PIXI. Можна отримати доступ до кожної текстури по тому ж імені - яке було з самого початку (“blob.png”, “dungeon.png”, “explorer.png”, і тд.)

Щоб створити спрайти з загружених текстур є 3 способи

СЛАЙД 47

1) TextureCache

СЛАЙД 48

2) Через інстанс лоадера

СЛАЙД 49

3) Через створення аліаса текстур


Тепер спробуємо створити підземелля використовуючи те що вже дізнались.

Покажи в едіторі.

TextureCache = PIXI.utils.TextureCache,
width: 512,
height: 512,


//Define variables that might be used in more 
//than one function
let dungeon, explorer, treasure, id;

function setup() {

  //There are 3 ways to make sprites from textures atlas frames

  //1. Access the `TextureCache` directly
  let dungeonTexture = TextureCache["dungeon.png"];
  dungeon = new Sprite(dungeonTexture);
  app.stage.addChild(dungeon);

  //2. Access the texture using throuhg the loader's `resources`:
  explorer = new Sprite(
    resources["images/treasureHunter.json"].textures["explorer.png"]
  );
  explorer.x = 68;

  //Center the explorer vertically
  explorer.y = app.stage.height / 2 - explorer.height / 2;
  app.stage.addChild(explorer);

  //3. Create an optional alias called `id` for all the texture atlas 
  //frame id textures.
  id = PIXI.loader.resources["images/treasureHunter.json"].textures; 
  
  //Make the treasure box using the alias
  treasure = new Sprite(id["treasure.png"]);
  app.stage.addChild(treasure);

  //Position the treasure next to the right edge of the canvas
  treasure.x = app.stage.width - treasure.width - 48;
  treasure.y = app.stage.height / 2 - treasure.height / 2;
  app.stage.addChild(treasure);
}


Проведи аналіз коду...

Тепер давайте додамо на стейдж монстрів та двері

Покажи в едіторі.


//Make the exit door
  door = new Sprite(id["door.png"]); 
  door.position.set(32, 0);
  app.stage.addChild(door);

  //Make the blobs
  let numberOfBlobs = 6,
      spacing = 48,
      xOffset = 150;

  //Make as many blobs as there are `numberOfBlobs`
  for (let i = 0; i < numberOfBlobs; i++) {

    //Make a blob
    let blob = new Sprite(id["blob.png"]);

    //Space each blob horizontally according to the `spacing` value.
    //`xOffset` determines the point from the left of the screen
    //at which the first blob should be added.
    let x = spacing * i + xOffset;

    //Give the blob a random y position
    //(`randomInt` is a custom function - see below)
    let y = randomInt(0, app.stage.height - blob.height);

    //Set the blob's position
    blob.x = x;
    blob.y = y;

    //Add the blob sprite to the stage
    app.stage.addChild(blob);



//The `randomInt` helper function
function randomInt(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}





Тепер навчимо їх рухатись

Ми вмієм малювати спрайти, - тепер щоб їх рухати - нам потрібно створити цикл використовуючи ticker PIXI - це називається game loop.
Будь який код всередині game loop буде оновлювати 60 раз в секунду. Напишемо код - який буде рухати спрайт праворуч зі швидкість 1px у фрейм.


Покажи в едіторі.


function setup() {
  //Start the game loop by adding the `gameLoop` function to
  //Pixi's `ticker` and providing it with a `delta` argument.
  app.ticker.add(delta => gameLoop(delta));
}

function gameLoop(delta){
  //Move the explorer 1 pixel 
    explorer.x += 1;
}

СЛАЙД 50


Будь яка функція - яку ми додамо до Pixi's ticker буде викликана 60 раз в секунду, також ми передали функції delta - для чого?

Значення delta - відповідає за значення fractional lag між frames ми можемо додавати його до позиції щоб зробити анімацію незалежною від фреймрейту.

Покажи в едіторі.

explorer.x += 1 + delta;

Чи ми це додамо - чи ні, це здебільшого естетичний вибір, еффект буде видно тільки якщо анімація буде не справлятись з фреймретом 60фпс

Щоб створити game loop не обов*язково використовувати тікер, можна обійтись звичайним requestAnimationFrame


СЛАЙД 51


Покажи в едіторі.

function gameLoop() {

  //Call this `gameLoop` function on the next screen refresh
  //(which happens 60 times per second)
  requestAnimationFrame(gameLoop);

  //Move the cat
  explorer.x += 1;
}

//Start the loop
gameLoop();


СЛАЙД 52


Використання швидкості

Щоб у нас було більше гнучкості - добра ідея контролювати швидкість руху спрайту, для цього є два параметри vx та vy.
По горизонталі та по вертикалі. Замість того щоб міняти в спрайті x та y напряму, спочатку краще змінити швидкість. Це нам дає більше керування.

задамо 
нашому персонажу стартові параметри швидкості, при них він буде стояти

explorer.vx = 0;
explorer.vy = 0;

та оновимо gameloop

function gameLoop(delta){

    //Update the explorer's velocity
    explorer.vx = 1;
    explorer.vy = 1;

    //Apply the velocity values to the explorer's 
    //position to make it move
    explorer.x += explorer.vx;
    explorer.y += explorer.vy;

}

СЛАЙД 53

Стани гри

Незалежно від стиля програмування, щоб допомогти нашому коду - PIXI рекомендує наступну структуру для ігрового цикла

//Set the game state
state = play;
 
//Start the game loop 
app.ticker.add(delta => gameLoop(delta));

function gameLoop(delta){

  //Update the current game state:
  state(delta);
}

function play(delta) {

  //Move the explorer 1 pixel to the right each frame
  explorer.vx = 1
  explorer.x += explorer.vx;
}

Тут ми бачимо що  функція gameLoop викликає функцію state 60 разів на секунду і код в play теж виконається 60 разів на секунду.


СЛАЙД 54

Керування з клавіатури

function keyboard(keyCode) {
  let key = {};
  key.code = keyCode;
  key.isDown = false;
  key.isUp = true;
  key.press = undefined;
  key.release = undefined;
  //The `downHandler`
  key.downHandler = event => {
    if (event.keyCode === key.code) {
      if (key.isUp && key.press) key.press();
      key.isDown = true;
      key.isUp = false;
    }
    event.preventDefault();
  };

  //The `upHandler`
  key.upHandler = event => {
    if (event.keyCode === key.code) {
      if (key.isDown && key.release) key.release();
      key.isDown = false;
      key.isUp = true;
    }
    event.preventDefault();
  };

  //Attach event listeners
  window.addEventListener(
    "keydown", key.downHandler.bind(key), false
  );
  window.addEventListener(
    "keyup", key.upHandler.bind(key), false
  );
  return key;
}

let keyObject = keyboard(asciiKeyCodeNumber);

keyObject.press = () => {
  //key object pressed
};
keyObject.release = () => {
  //key object released
};


Покажи в едіторі.


          //Capture the keyboard arrow keys
            let left = keyboard(37),
                up = keyboard(38),
                right = keyboard(39),
                down = keyboard(40);
            //Left arrow key `press` method
            left.press = function () {
                //Change the explorer's velocity when the key is pressed
                explorer.vx = -5;
                explorer.vy = 0;
            };
            //Left arrow key `release` method
            left.release = function () {
                //If the left arrow has been released, and the right arrow isn't down,
                //and the explorer isn't moving vertically:
                //Stop the explorer
                if (!right.isDown && explorer.vy === 0) {
                    explorer.vx = 0;
                }
            };
            //Up
            up.press = function () {
                explorer.vy = -5;
                explorer.vx = 0;
            };
            up.release = function () {
                if (!down.isDown && explorer.vx === 0) {
                    explorer.vy = 0;
                }
            };
            //Right
            right.press = function () {
                explorer.vx = 5;
                explorer.vy = 0;
            };
            right.release = function () {
                if (!left.isDown && explorer.vy === 0) {
                    explorer.vx = 0;
                }
            };
            //Down
            down.press = function () {
                explorer.vy = 5;
                explorer.vx = 0;
            };
            down.release = function () {
                if (!up.isDown && explorer.vx === 0) {
                    explorer.vy = 0;
                }
            };




function gameLoop() {
    //use the explorer's velocity to make it move
    explorer.x += explorer.vx;
    explorer.y += explorer.vy;
  }


СЛАЙД 55

Групування Спрайтів

СЛАЙД 56

Групі можна задавати позицію
animals.position.set(64, 64);

У Групи можна отримати її розмір
console.log(animals.width);

Групі можна задати розмір
animals.width = 200;

У картинок в групі є локальна та глобальна позиція.

СЛАЙД 57

У PIXI звичайно є примітиви

СЛАЙД 58

Текст

message.text = "Text changed!";
message.style = {fill: "black", font: "16px PetMe64"};
message.style = {wordWrap: true, wordWrapWidth: 100, align: center};































































































