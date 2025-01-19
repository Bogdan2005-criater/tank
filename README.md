
### **1. Часть кода: Анимация движущегося квадрата**
 ```javascript
let ctx = document.getElementById('myCanvas').getContext('2d');
let x = 50, dx = 2; // начальные координаты и скорость движения

function animate() {
    ctx.clearRect(0, 0, 500, 500); // очистка канваса
    ctx.fillStyle = 'red'; // задание цвета квадрата
    ctx.fillRect(x, 200, 50, 50); // рисуем квадрат
    x += dx; // обновляем координату x

    if (x <= 0 || x + 50 >= 500) dx = -dx; // изменение направления  
        requestAnimationFrame(animate); // следующий кадр анимации
    }
requestAnimationFrame(animate); // начальный вызов функции
  ```
### **2. Управление квадратом с помощью клавиш (стрелки)**
 ```javascript
const canvas = document.getElementById('myCanvas');
const ctx = canvas.getContext('2d');
let x = canvas.width / 2;
let y = canvas.height / 2;
const speed = 5;
let dx = 0;
let dy = 0;
// Функция для рисования квадрата
function drawSquare() {
    ctx.clearRect(0, 0, canvas.width, canvas.height); // Очистка канваса
    ctx.fillStyle = 'purple'; // Цвет квадрата
    ctx.fillRect(x, y, 50, 50); // Рисуем квадрат
    x += dx;
    y += dy;
}

 function keyDownHandler(event) {
    if (event.key === 'ArrowRight') {
        dx = speed;
    } else if (event.key === 'ArrowLeft') {
        dx = -speed;
    } else if (event.key === 'ArrowUp') {
        dy = -speed;
    } else if (event.key === 'ArrowDown') {
        dy = speed;
    }
}
// Обработка опускания клавиш
function keyUpHandler(event) {
    if (event.key === 'ArrowRight' || event.key === 'ArrowLeft') {
        dx = 0;
    } else if (event.key === 'ArrowUp' || event.key === 'ArrowDown') {
        dy = 0;
    }
}
// Слушатель на события клавиатуры
document.addEventListener('keydown', keyDownHandler);
document.addEventListener('keyup', keyUpHandler);

// Запуск анимации
function animate() {
    requestAnimationFrame(animate);
    drawSquare();
}

animate();
  ```
### **3. Следование квадрата за мышью**
 ```javascript
const canvas = document.getElementById('myCanvas');
const ctx = canvas.getContext('2d');

let square = {
    x: 0,
    y: 0,
    size: 20
};
canvas.addEventListener('mousemove', (event) => {
    const rect = canvas.getBoundingClientRect();
    square.x = event.clientX - rect.left - square.size / 2;
    square.y = event.clientY - rect.top - square.size / 2;
    draw();
});

function draw() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    ctx.fillStyle = 'blue';
    ctx.fillRect(square.x, square.y, square.size, square.size);
}
draw();
  ```
### **4. Проверка столкновений**
 ```javascript
// Проверка столкновений
function checkCollision() {
    if (x < enemyX + enemyWidth && x + 50 > enemyX && y < enemyY + enemyHeight && y + 50 > enemyY) {
        stopGame();
    }
}

// Остановка игры при столкновении
function stopGame() {
    dx = 0;
    dy = 0;
    enemyDx = 0;
}

  ```
Давайте подробно разберем предоставленный код, его функционал и задачи. Он представляет собой учебный материал, предназначенный для подготовки учащихся к созданию игры на основе Canvas API.

---

### **1. Часть кода: Анимация движущегося квадрата**
В самом начале кода представлена базовая анимация квадрата, который движется горизонтально в пределах канваса. Основные элементы:
- **`ctx.clearRect(0, 0, 500, 500)`** очищает область канваса для того, чтобы каждый кадр перерисовывался заново, иначе будет "след" от квадрата.
- **`ctx.fillStyle = 'red'`** задает цвет квадрата.
- **`ctx.fillRect(x, 200, 50, 50)`** рисует квадрат по координатам `x` и `200`, с шириной и высотой 50px.
- **`x += dx`** обновляет координаты квадрата на каждом кадре, двигая его горизонтально.
- **`if (x <= 0 || x + 50 >= 500)`** проверяет, достигает ли квадрат границы канваса, и изменяет направление (`dx = -dx`).

### **2. Управление квадратом с помощью клавиш (стрелки)**
Здесь реализовано управление движением квадрата с помощью стрелок. Ключевые моменты:
- **Обработчики событий `keydown` и `keyup`**:
  - `keydown` изменяет скорость квадрата (`dx` или `dy`) в зависимости от нажатой клавиши.
  - `keyup` сбрасывает скорость в 0, чтобы квадрат останавливался, когда пользователь отпускает клавишу.
- **`x` и `y`** представляют текущие координаты квадрата, которые обновляются при каждом вызове функции `drawSquare`.
- Функция **`drawSquare`** очищает канвас, рисует квадрат в новых координатах и обновляет их.

---

### **3. Следование квадрата за мышью**
Следующий пример добавляет новый функционал — управление квадратом, который следует за курсором мыши:
- **`canvas.addEventListener('mousemove')`** отслеживает положение курсора на канвасе.
- **`event.clientX` и `event.clientY`** определяют координаты курсора относительно окна браузера. Чтобы получить координаты внутри канваса, используется вычитание смещения канваса (`rect.left` и `rect.top`).
- Новые координаты квадрата передаются в объект **`square`**, а затем перерисовываются функцией **`draw`**.

---

### **4. Проверка столкновений**
Добавлен базовый функционал для обработки столкновений:
- **`checkCollision`** проверяет, пересекаются ли прямоугольники танка игрока и врага.
  - Условия используют проверку координат: если координаты углов двух квадратов пересекаются, это считается столкновением.
  - При столкновении вызывается функция **`stopGame`**, которая останавливает движение игрока и врага.

---

## **Задание: Создание игры в танчики**

### **1. Управление персонажем**
Необходимо добавить управление танком игрока. Для этого уже есть заготовка, где реализовано управление через стрелки, но нужно добавить поддержку клавиш **WASD**:
- **`W`** для движения вверх (`dy = -speed`).
- **`A`** для движения влево (`dx = -speed`).
- **`S`** для движения вниз (`dy = speed`).
- **`D`** для движения вправо (`dx = speed`).

### **2. Враги**
Враги представляют собой квадраты, которые двигаются по заранее заданному маршруту. Нужно:
- Создать массив объектов для врагов, например:
  ```javascript
  let enemies = [
      { x: 100, y: 100, width: 50, height: 50, dx: 2, dy: 1 },
      { x: 300, y: 300, width: 50, height: 50, dx: -1, dy: 2 }
  ];
  ```
- Реализовать движение врагов:
  ```javascript
  function moveEnemies() {
      enemies.forEach(enemy => {
          enemy.x += enemy.dx;
          enemy.y += enemy.dy;
          // Проверка границ канваса
          if (enemy.x <= 0 || enemy.x + enemy.width >= canvas.width) {
              enemy.dx = -enemy.dx;
          }
          if (enemy.y <= 0 || enemy.y + enemy.height >= canvas.height) {
              enemy.dy = -enemy.dy;
          }
      });
  }
  ```

### **3. Обработка столкновений**
Проверка столкновений между игроком и каждым из врагов:
- Внутри основного цикла:
  ```javascript
  function checkCollisions() {
      enemies.forEach(enemy => {
          if (
              square.x < enemy.x + enemy.width &&
              square.x + square.size > enemy.x &&
              square.y < enemy.y + enemy.height &&
              square.y + square.size > enemy.y
          ) {
              stopGame();
          }
      });
  }
  ```

### **4. Финализация игры**
Функция **`stopGame`** может:
- Остановить анимацию, используя флаг:
  ```javascript
  let isGameRunning = true;
  
  function stopGame() {
      isGameRunning = false;
  }
  ```
- Вывести сообщение о проигрыше:
  ```javascript
  function stopGame() {
      alert('Игра окончена!');
      isGameRunning = false;
  }
  ```

### Итоговая структура игры
1. **Игровой цикл**:
   - Обновление положения игрока.
   - Движение врагов.
   - Проверка столкновений.
   - Перерисовка канваса.
2. **События клавиатуры** для управления танком игрока.
3. **Логика движения врагов**.

После реализации всего этого получится базовая игра в танчики, где игрок управляет своим танком, избегая столкновений с врагами.
