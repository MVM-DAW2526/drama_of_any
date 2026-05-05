## Exercici 1: La purificació bàsica (Exercici Guiat)

**Context:** Ens trobem a la caserna general de l'Esquadró d'Exploració (*Attack on Titan*). Tenim una base de dades mèdica per als soldats, però el desenvolupador anterior, a causa de la pressa bèl·lica, va utilitzar `any` per tot arreu. 

Aquest és el codi trencat original:

```ts
// ❌ ATENCIÓ: Codi perillós
let woundedSoldiers: any = [];

function healSoldier(soldier: any) {
  soldier.hp = 100;
  soldier.isInjured = false;
  woundedSoldiers.push(soldier);
  console.log("Soldier " + soldier.name + " is fully healed!");
}

healSoldier({ name: "Levi", hp: 10, isInjured: true });

// Això farà fallida a l'execució ("undefined.name" no existeix), però TS no ens avisa abans!
healSoldier("Eren Yeager"); 
```

### Com ho resolem? (Passos)

1. **Analitzem l'entrada necessària:** Dins la funció, què s'espera realment de l'objecte? Veiem que fa l'ús de `soldier.hp`, `soldier.isInjured` i llegeix `soldier.name`.
2. **Creem el contracte (Interface):** Substituïm el caos per protecció.
   ```ts
   interface Soldier {
     name: string;
     hp: number;
     isInjured: boolean;
   }
   ```
3. **Reemplacem l'`any` pel gran nou tipus:**
   ```ts
   // ✅ Ara és un llistat confinat a la interfície
   let woundedSoldiers: Soldier[] = []; 

   function healSoldier(soldier: Soldier) { // Adéu 'any'!
     soldier.hp = 100;
     soldier.isInjured = false;
     woundedSoldiers.push(soldier);
     console.log("Soldier " + soldier.name + " is fully healed!");
   }

   healSoldier({ name: "Levi", hp: 10, isInjured: true }); // ✅ Correcte

   // healSoldier("Eren Yeager"); 
   // ❌ TypeScript ara t'evitarà un desastre aturant la compilació. Hem salvat vides!
   ```
