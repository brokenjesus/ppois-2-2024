# Модель автомобиля

Документация для программы имитирующей работу автомобиля

<h2>Класс StartCarError</h2>
Класс исключения, которое выбрасывается при невозможности запуска двигателя автомобиля. Унаследован от Exception

<h2>Класс CarDriveError</h2>
Класс исключения, которое выбрасывается при поломке автомобиля во время вождения. Унаследован от Exception

<h2>Класс SwitchAutomaticTransmissionError</h2>
Класс исключения, которое выбрасывается при попытке поменять передачу у автомобиля с автоматической коробкой передач. Унаследован от Exception

<h2>Класс CarNotInListError</h2>
Класс исключения, которое выбрасывается при отсутствии машины в списке автопарка водителя. Унаследован от ValueError

<h2>Класс InvalidGearError</h2>
Класс исключения, которое выбрасывается при попытке установить несуществующую передачу. Унаследован от ValueError

<h2>Класс InvalidAgeError</h2>
Класс исключения, которое выбрасывается при попытке сесть в машину, если водитель несовершенолетний. Унаследован от ValueError

<h2>Класс CurrentCarUnavailableError</h2>
Класс исключения, которое выбрасывается при отсутствии текущей машины. Унаследован от ValueError

<h2>Класс TransmissionType</h2>
Класс типа трансмиссии. Унаследован от Enum

<h3>Состояния</h3>
<ul>
  <li>automatic</li>
  <li>mechanical</li>
</ul>

<h2>Класс Season</h2>
Класс тормозов. Унаследован от Enum

<h3>Состояния</h3>
<ul>
  <li>winter</li>
  <li>summer</li>
</ul>

<h2>Класс Gears</h2>
Класс тормозов. Унаследован от Enum

<h3>Состояния</h3>
<ul>
  <li>N</li>
  <li>R</li>
  <li>G1</li>
  <li>G2</li>
  <li>G3</li>
  <li>G4</li>
</ul>

<h2>Класс AddDel</h2>
Интерфейс, включающий методы добавления(add) и удаления(rem). Используется для унаследования от него класса Driver и GasStation. 

<h2>Класс Human</h2>
Класс человека, используется для унаследования от него класса Driver. Имеет только геттеры и сеттеры.

<h3>Методы</h3>
<ul>
  <li>__init__(self, name: str, surname: str, age: int=18)</li>
  Создаёт экземпляр класса с именем(name), фамилией(surname) и возрастом(age) человека;
</ul>

<h2>Класс Detail</h2>
Класс детали, используется для унаследования от него классов подсистем автомобиля.

<h3>Методы</h3>
<ul>
  <li>__init__(self, vendor: str, creation_year: int=2024)</li>
  Создаёт экземпляр класса с названием производителя(vendor), годом создания(creation_year) и текущим состоянием(вычисляется относительно года создания) детали;
  <li>__str__(self)</li>
  Представляет объект класса в виде строки;
  <li>restore(self)</li>
  Устанавливает максимальное значение текущего состояния детали;
  <li>damage(self)</li>
  Уменьшает значение текущего состояния детали на 1;
</ul>

<h2>Класс Brakes</h2>
Класс тормозов. Унаследован от Detail.

<h2>Класс Wheels</h2>
Класс колёс. Унаследован от Detail.

<h3>Методы</h3>
<ul>
  <li>__init__(self, season: Season, vendor: str, creation_year: int=2024)</li>
  Создаёт экземпляр класса, используя конструктор наследника, и устанавливает сезонность(season) колёс;
  <li>__str__(self)</li>
  Представляет объект класса в виде строки, используя метод предка;
</ul>

<h2>Класс Transmission</h2>
Класс трансмиссии Унаследован от Detail. 

<h3>Методы</h3>
<ul>
  <li>__init__(self, ttype: TransmissionType, vendor: str, creation_year: int=2024)</li>
  Создаёт экземпляр класса, используя конструктор наследника, и устанавливает тип трансмиссии(ttype) и текущую передачу;
  <li>__str__</li>
  Представляет объект класса в виде строки, используя метод предка;
  <li>set_gear(new_gear: Gears)</li>
  Устанавливает новую текущую передачу(new_gear). Если такой передачи нет в списке выбрасывает ошибку InvalidGearError. В случае если пользователь попытается сменить передачу, когда трансмиссия автоматическая - выбрасывает ошибку SwitchAutomaticTransmissionError;
</ul>

<h2>Класс Engine</h2>
Класс трансмиссии Унаследован от Detail. 

<h3>Методы</h3>
<ul>
  <li>__init__(self, volume: int, vendor: str, creation_year: int=2024, fuel_level: int=0, oil: bool=False)</li>
  Создаёт экземпляр класса, используя конструктор наследника, и устанавливает объём бака(volume), текущий уровень топлива(fuel_level) и состояние масла(oil);
  <li>__str__</li>
  Представляет объект класса в виде строки, используя метод предка;
  <li>maximize_fuel_level</li>
  Устанавливает текущий уровень топлива равный объёму бака;
  <li>fuel_waste</li>
  Уменьшает текущий уровень топлива на 5% от объёма бака. В случае пустого бака, выводит информацию об этом;
</ul>

<h2>Класс Car</h2>
Класс представляющий модель автомобиля и реализующий взаимодействие между её компонентами;

<h3>Методы</h3>
<ul>
  <li>__init__(self, engine: Engine, wheels: Wheels, transmission: Transmission, brakes: Brakes, car_name: str, creation_year: int=2024)</li>
  Создаёт экземпляр класса с текущим двигателем(engine), колёсами(wheels), трансмиссией(transmission), тормозами(brakes), названием(car_name) и годом создания(creation_year) машины;
  <li>__str__</li>
  Представляет объект класса в виде строки;
  <li>increment_mileage</li>
  Увеличивает пробег на 1 единицу;
  <li>oil_waste</li>
  Убирает наличие масла из двигателя с 10% шансом;
  <li>repair</li>
  Полностью восстанавливает максимальное состояние всех деталей автомобиля;
</ul>

<h3>Свойства</h3>
<ul>
  <li>light_indicators(self) -> dict</li>
  Возвращает словарь световых индикаторов, показывающих уровень топлива, объём бака, состояния масла, двигателя, колёс, трансмиссии и тормозов, информацию о текущей передаче, работе двгателя и пробеге(вычисляется относительно года создания);
</ul>

<h2>Класс Driver</h2>
Класс водителя, реализующий взаимодействие с автоиобилем(управление и обслуживание). Унаследован от AddDel и Human.

<h3>Методы</h3>
<ul>
  <li>__init__(self, name: str, surname: str, age: int=18, vehicle_fleet: set[Car]=set()</li>
  Создаёт экземпляр класса, используя конструктор наследника(Human), с автопарком(vehicle_fleet) и текущим автомобилем(изначально None);
  <li>__str__(self)</li>
  Представляет объект класса в виде строки;
  <li>__hash__(self)</li>
  Создаёт хеш объекта класса на основании кортежа состоящего из имени, фамилии и возраста водителя;
  <li>__eq__(self, other)</li>
  Провереят равенство хешей self и other. Если other не является объектом класса Driver выбрасывает ошибку TypeError("right operand should be object of class Driver");
  <li>get_car_state(self) -> dict</li>
  Возвращает состояние текущей машины в виде словаря световых индикаторов. Если текущей машины нет, выбрасывает ошибку CurrentCarUnavailableError;
  <li>oil_change</li>
  Производит замену масла у текущей машины. Если текущей машины нет, выбрасывает ошибку CurrentCarUnavailableError;
  <li>add(car: Car)</li>
  Добавляет машину(car) в автопарк водителя. Если эта машина уже есть в автопарке, сообщает об этом;
  <li>choose(car: Car)</li>
  Позволяет выбрать машину(car) в качестве текущей. Если возраст водителя меньше 18 выбрасывает ошибку InvalidAgeError, в случае если выбранной машины нет в автопарке - выбрасывает ошибку CarNotInListError;
  <li>rem(car: Car)</li>
  Убирает машину(car) из автопарка. Если данной машины в автопарке нет, сообщает об этом;
  <li>start_engine</li>
  Запускает двигатель текущего автомобиля. Если текущей машины нет, выбрасывает ошибку CurrentCarUnavailableError, в случае если у машины нет топлива, сломаны двигатель или трансмиссия либо нет масла - выбрасывается ошибка StartCarError;
  <li>stop_engine(car: Car)</li>
  Глушит двигатель текущего автомобиля. Если текущей машины нет, выбрасывает ошибку CurrentCarUnavailableError;
  <li>drive_forward(car: Car)</li>
  Ведёт текущий автомобиль вперёд, попутно увеличивает пробег, уменьшает уровень топлива и изнашиавет детали автомобиля. Если текущей машины нет, выбрасывает ошибку CurrentCarUnavailableError, в случае если установленна задняя или нейтральная передача - выбрасывает ошибку InvalidGearError. Если же у машины нет топлива, сломаны двигатель, трансмиссия или колёса, двигатель не заведён либо нет масла - выбрасывает ошибку CarDriveError;
  <li>drive_back</li>
  Ведёт текущий автомобиль назад, попутно увеличивает пробег, уменьшает уровень топлива и изнашиавет детали автомобиля. Если текущей машины нет, выбрасывает ошибку CurrentCarUnavailableError, в случае если не установленна задняя передача - выбрасывает ошибку InvalidGearError. Если же у машины нет топлива, сломаны двигатель, трансмиссия или колёса, двигатель не заведён либо нет масла - выбрасывает ошибку CarDriveError;
  <li>drive_right(car: Car)</li>
  Ведёт текущий автомобиль направо, попутно увеличивает пробег, уменьшает уровень топлива и изнашиавет детали автомобиля. Если текущей машины нет, выбрасывает ошибку CurrentCarUnavailableError, в случае если установленна задняя или нейтральная передача - выбрасывает ошибку InvalidGearError. Если же у машины нет топлива, сломаны двигатель, трансмиссия, колёса или тормоза, двигатель не заведён либо нет масла - выбрасывает ошибку CarDriveError;
  <li>drive_left(car: Car)</li>
  Ведёт текущий автомобиль налево, попутно увеличивает пробег, уменьшает уровень топлива и изнашиавет детали автомобиля. Если текущей машины нет, выбрасывает ошибку CurrentCarUnavailableError, в случае если установленна задняя или нейтральная передача - выбрасывает ошибку InvalidGearError. Если же у машины нет топлива, сломаны двигатель, трансмиссия, колёса или тормоза, двигатель не заведён либо нет масла - выбрасывает ошибку CarDriveError;
</ul>

<h2>Класс GasStation</h2>
Класс заправочной станции. Унаследован от AddDel.

<h3>Методы</h3>
<ul>
  <li>add(cls, car: Car)</li>
  Добавляет машину(car) в очередь заправочной станции. Если эта машина уже есть в очереди, сообщает об этом
  <li>rem(cls, car: Car)</li>
  Убирает машину(car) из очереди. Если данной машины в очереди нет, сообщает об этом 
  <li>gen_refueling_car(cls) -> Generator</li>
  Генерирует заправленные машины из заправачной очереди
</ul>
