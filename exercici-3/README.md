## Exercici 3: La mutació incontrolable (Pràctica avançada)

**Context:** Has detectat un àlien paràsit (*Parasyte: The Maxim*). En les fases inicials, només era una cèl·lula amorfa de la qual ningú no en sabia l'estructura, i el desenvolupador inicial va optar per inicialitzar-lo com a objecte lliure `let migi: any = {}`.

El problema? Com que era un objecte dictat via `any`, l'alien es passa de la ratlla i genera mutacions invisibles, causant errors arquitectònics fatals: el creador ha intentat afegir una propietat anomenada `weapons` quan el diccionari mèdic exigeix que aquest camp s'identifiqui sempre amb la paraula `skills`. I un cop més... gràcies a l'`any` el compilador ha acceptat la invenció sense dir res!

**Codi base malaltís (purifica'l):**
```ts
// Aquest declarador és el niu del problema: permet que l'objecte muti per defecte.
let migi: any = {};

// Un array de mutacions en plena fugida.
migi.hostName = "Shinichi";
migi.strengthLevel = 9000;
migi.isAwake = true;

// ⚠️ ERROR OCULT FATAL: M'he equivocat de nom! Aquesta propietat no té sentit biològic 
// però la flexibilitat ho ha acceptat.
migi.weapons = ["blade form"]; 

// L'any passa a infectar fins i tot les funcions
function activateDefense(parasite: any) {
  if (parasite.isAwake) {
    console.log(parasite.hostName + " is protected covering the arm!");
  }
}

activateDefense(migi);
```

**Objectiu Màxim:**
1. Crea una poderosa `interface Parasite` on posaràs clàusules de ferro: S'ha de tenir exactament `hostName` (string), `strengthLevel` (number), `isAwake` (boolean) i el camp correcte **`skills`** (`string[]`).
2. Retoca l'objecte original abandonant l'`any`. Inicialitza la unitat amb totes les variables requerides dins d'uns corxetes respectuosos `{}` simultàniament, o bé juga amb opcionals a la teva interface.
3. Purrega la funció central `activateDefense` posant-hi la nova via encriptada d'informació, per saber que res de fora fallarà.
4. L'objectiu està assolit en el moment que el *linter* sencer et posi ralles vermelles si proves d'escriure un camp que et doni la gana.

No permetis cap `any` en aquesta habitació! Endavant amb l'examen!
