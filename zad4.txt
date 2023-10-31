// Родительская функция для любого типа электрооборудования
function ElectricalDevice(name) {
  this.name = name,
  this.plug = false,
  this.power = 0
}

// Функция включения устройства
ElectricalDevice.prototype.turnOnDevice = function() {
  this.plug = true;
  console.log(`The ${this.name} is on!`)
}

// Функция выключения устройства
ElectricalDevice.prototype.turnOffDevice = function() {
  this.plug = false;
  console.log(`The ${this.name} is off!`)
}

// Ноутбук может иметь разные режимы работы, влияющие на потребляемую мощность
function Laptop(name) {
  this.name = name,
  this.mode = ""
}

Laptop.prototype = new ElectricalDevice()

Laptop.prototype.setMode = function(mode) {
  switch (mode) {
    case "normal":
      this.mode = "normal";
      this.power = 60;
      console.log(`The normal mode is set for ${this.name}`);
      break;
    case "saver":
      this.mode = "saver";
      this.power = 15;
      console.log(`The energy-saving mode is set for ${this.name}`);
      break;
    case "turbo":
      this.mode = "turbo";
      this.power = 80;
      console.log(`The turbo mode is set for ${this.name}`);
      break;
    default:
      this.power = 0;
      console.log(`Unknown mode for ${this.name} is set.`);
  }
}

Laptop.prototype.getPower = function() {
  if (this.plug) {
    console.log(`The power of the ${this.name} in ${this.mode} mode is ${this.power} watts.`)
  } else {
    console.log(`The ${this.name} does not consume power because it is turned off.`)
  }
}

// Потребляемая мощность чайника зависит от его объема
function Teapot(name, volume) {
  this.name = name,
  this.power = 1000 * volume
}

Teapot.prototype = new ElectricalDevice()

Teapot.prototype.getPower = function() {
  if (this.plug) {
    console.log(`The power of the ${this.name} is ${this.power} watts.`)
  } else {
    console.log(`The ${this.name} does not consume power because it is turned off.`)
  }
}

// Создание приборов, установка режимов работы и их включение/выключение
const laptop1 = new Laptop("Asus");

laptop1.setMode("superturbo");

laptop1.setMode("saver");

laptop1.getPower();

laptop1.turnOnDevice();

const laptop2 = new Laptop("HP");

laptop2.setMode("normal");

laptop2.turnOnDevice();

const teapot1 = new Teapot("Bork", 1.5);

const energyConsumers = [laptop1, laptop2, teapot1];

let totalPower = 0;

// Расчет суммарной мощности в зависимости от включенных устройств
for (let device of energyConsumers) {
  device.getPower();
  if (device.plug) {
    totalPower += device.power;
  }
}

console.log(`The total power of the ${energyConsumers.length} devices is ${totalPower}.`)
