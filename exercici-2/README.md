## Exercici 2: L'Escàner del Dominator (Pràctica autònoma)

**Context:** Formes part de la Unitat 1 de Seguretat Pública (*Psycho-Pass*). T'arriben dades incertes (una denúncia) des del gran Sistema Sibyl, i el gestor de paquets ho ha designat com a `any`. A conseqüència, el sistema del Dominator està executant mètodes basats en text (`toUpperCase()`) per a tot el que arriba. De vegades arriba un codi de xifres, i el sistema sencer fa *crash* per intentar passar un text majúscules a números que no ho suporten.

**Objectiu:** 
Tens l'ordre explícita de desfer l'`any`, utilitzar `unknown` pel target, i assegurar el tir amb comprovacions (`typeof`) abans no facis cap tractament.

**Codi base a arreglar:**
```ts
function scanTarget(data: any) {
  // Com que és 'any', TS confia cegament i assumeix que tot pot ser Text...
  let analysis = data.toUpperCase(); 
  console.log("Sibyl System says: " + analysis);
}

scanTarget("Latent Criminal detected in sector 4");

// Això provoca error gravíssim a Javascript (crash).
// TS no ho ha vist per culpa de l'any.
scanTarget(999); 
```

**Pistes per completar-ho:**
1. Canvia aquest `any` pel super segur `"unknown"`. Observa com l'editor ara subratlla `.toUpperCase()` en vermell negant-te l'accés.
2. Afegeix la lògica de seguretat `if (typeof data === "string") { ... }` envoltant la reacció.
3. Condiciona la resposta amb un `else` segur on imprimeixis: `"Error: Format de dades biològicament rebutjat"`.
