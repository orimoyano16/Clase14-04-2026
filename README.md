# Clase14-04-2026
## Moyano Oriana 
1- Implementar en local

2- Identificar las relaciones de jerarquía.

3- Implementar con todas las formas de asociación

4- Pegar el desarrollo en la hoja de calculo 

5- ¿Cuál es la diferencia en tiempo de ejecución de la asociación por Composición y la asociación por Agregación?


## Respuestas 
1- Console.log

“Aeroplano compuesto por: 3 hélice/sAlas Frontales: 2 Alas Posteriore: 3Tren de Aterrizaje compuesto por:  con Retractil fijo, 2 neumáticos, 3 amoriguadores Cubierta compuesta de:  Cubierta de Vuelo,  Cubierta de Tripulación,  Sistema de Emergencia, 4 Tanques de Combustible, 4 Puertas de Salida.”

2- Aeroplano
├── Helice
├── TrenDeAterrizaje
├── Alas
└── Cubierta

3-
1. Tipos de asociación a implementar
1. Asociación simple (usa a otra clase)
Una clase utiliza otra sin poseerla necesariamente
2. Agregación (HAS-A débil)
El objeto puede existir independientemente
3. Composición (HAS-A fuerte)
El objeto depende totalmente del contenedor
4. Dependencia (uso temporal)
Se usa como parámetro o dentro de un método

### ✔ COMPOSICIÓN 

Aeroplano está compuesto por partes esenciales

class Aeroplano {
    private helice: Helice;
    private trenAterrizaje: TrendeAterrizaje;
    private alas: Alas;
    private cubierta: Cubierta;

    constructor(
        phelice: Helice,
        pTrenAterrizaje: TrendeAterrizaje,
        pAlas: Alas,
        pCubierta: Cubierta
    ) {
        this.helice = phelice;
        this.trenAterrizaje = pTrenAterrizaje;
        this.alas = pAlas;
        this.cubierta = pCubierta;
    }
}

✔ Relación fuerte: si no hay partes, no hay aeroplano

### ✔ AGREGACIÓN 

Agregamos una clase externa, por ejemplo:

class Piloto {
    nombre: string;

    constructor(nombre: string) {
        this.nombre = nombre;
    }
}

Ahora el aeroplano usa pero no depende totalmente del piloto:
class Aeroplano {
    private piloto?: Piloto; // opcional

    public asignarPiloto(p: Piloto) {
        this.piloto = p;
    }
}

✔ El piloto puede existir sin el avión
✔ El avión puede existir sin piloto

### ✔ ASOCIACIÓN SIMPLE

Ejemplo: Turbina relacionada con Helice

class Helice {
    private numHelices: number;
    private turbina?: Turbina; // asociación simple

    constructor(n: number) {
        this.numHelices = n;
    }

    public asignarTurbina(t: Turbina) {
        this.turbina = t;
    }
}

✔ Relación entre clases
✔ No es dependencia fuerte

 ### ✔ DEPENDENCIA (temporal)

Ejemplo: método que usa otra clase solo como parámetro

class ControlVuelo {
    public verificar(a: Aeroplano): string {
        return "Chequeo completo del aeroplano";
    }
}

✔ No se guarda la referencia
✔ Solo se usa momentáneamente

Aeroplano
├── (Composición) Helice
│       └── (Asociación) Turbina
├── (Composición) TrenAterrizaje
├── (Composición) Alas
├── (Composición) Cubierta
└── (Agregación) Piloto

ControlVuelo ---> (Dependencia) Aeroplano

5-No existe una diferencia significativa en el tiempo de ejecución entre composición y agregación, ya que ambas se implementan como referencias a objetos. La diferencia radica en el ciclo de vida y la dependencia entre objetos, no en la eficiencia.





```mermaid
classDiagram

class Aeroplano {
  -helice: Helice
  -trenAterrizaje: TrendeAterrizaje
  -alas: Alas
  -cubierta: Cubierta
  -piloto: Piloto
  +ToString(): string
  +asignarPiloto(p: Piloto): void
}

class Helice {
  -numHelices: number
  -turbina: Turbina
  +ToString(): string
  +asignarTurbina(t: Turbina): void
}

class Turbina {
  -numTurbinas: number
  +ToString(): string
}

class TrendeAterrizaje {
  -numNeumaticos: number
  -numAmortiguadores: number
  -fijoRetractil: boolean
  +ToString(): string
}

class Alas {
  -numAlasFrente: number
  -numAlasCola: number
  +ToString(): string
}

class Cubierta {
  -cabinaTripulacion: boolean
  -cabinaVuelo: boolean
  -sistemaEmergencia: boolean
  -numTanquesCombustible: number
  -numPuertasSalidas: number
  +ToString(): string
}

class Piloto {
  -nombre: string
}

class ControlVuelo {
  +verificar(a: Aeroplano): string
}

Aeroplano *-- Helice
Aeroplano *-- TrendeAterrizaje
Aeroplano *-- Alas
Aeroplano *-- Cubierta

Aeroplano o-- Piloto

Helice --> Turbina

ControlVuelo ..> Aeroplano



