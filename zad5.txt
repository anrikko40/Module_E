// Класс для любого типа электрооборудования
class ElectricalDevice {
  constructor(name) {
    this.name = name;
    this.plug = false;
    this.power = 0;
  }
  // Метод включения устройства   
  turnOnDevice() {
    this.plug = true;
    console.log(`The ${this.name} is on!`);
  }
  // Метод выключения устройства  
  turnOffDevice() {
    this.plug = false;
    console.log(`The ${this.name} is off!`);
  }
}

// Ноутбук может иметь разные режимы работы, влияющие на потребляемую мощность
class Laptop extends ElectricalDevice {
  constructor(name) {
    super(name);
    this.mode = "";
  }
  setMode(mode) {
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
  getPower() {
    if (this.plug) {
      console.log(`The power of the ${this.name} in ${this.mode} mode is ${this.power} watts.`)
    } else {
      console.log(`The ${this.name} does not consume power because it is turned off.`)
    }
  }
}

// Потребляемая мощность чайника зависит от его объема
class Teapot extends ElectricalDevice {
  constructor(name, volume) {
    super(name);
    this.power = 1000 * volume;
  }
  getPower() {
    if (this.plug) {
      console.log(`The power of the ${this.name} is ${this.power} watts.`)
    } else {
      console.log(`The ${this.name} does not consume power because it is turned off.`)
    }
  }
}

// Создание приборов, установка режимов работы и их включение/выключение
const laptop1 = new Laptop("Asus");

laptop1.setMode("turbo");

laptop1.turnOnDevice();

const laptop2 = new Laptop("HP");

laptop2.setMode("normal");

laptop2.turnOffDevice();

const teapot1 = new Teapot("Bork", 2.0);

teapot1.turnOnDevice();

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