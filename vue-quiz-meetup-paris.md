# Quiz Vue.js Core - Meetup Paris
## 25 Questions du facile au très complexe

---

## NIVEAU FACILE (Questions 1-7)

### Question 1
**Combien de packages principaux compose Vue.js 3 core ?**
- A) 5
- B) 8
- C) 11 ✅
- D) 15

*Réponse: Il y a 11 packages: reactivity, runtime-core, runtime-dom, compiler-core, compiler-dom, compiler-sfc, compiler-ssr, server-renderer, shared, vue, et vue-compat*

---

### Question 2
**Quel mécanisme JavaScript Vue 3 utilise-t-il pour la réactivité ?**
- A) Object.defineProperty
- B) Proxy ✅
- C) Getters/Setters
- D) Observables

*Réponse: Vue 3 utilise les Proxy JavaScript (contrairement à Vue 2 qui utilisait Object.defineProperty)*

---

### Question 3
**Le package @vue/reactivity peut-il être utilisé indépendamment de Vue ?**
- A) Oui ✅
- B) Non
- C) Seulement avec Node.js
- D) Seulement côté client

*Réponse: Le système de réactivité est standalone et peut être utilisé sans Vue*

---

### Question 4
**Combien de types de handlers de proxy différents existe-t-il dans le système de réactivité ?**
- A) 2
- B) 4 ✅
- C) 6
- D) 8

*Réponse: 4 handlers: mutableHandlers, readonlyHandlers, shallowReactiveHandlers, shallowReadonlyHandlers*

---

### Question 5
**Quelle est la limite de récursion par défaut dans le scheduler pour détecter les boucles infinies ?**
- A) 50
- B) 100 ✅
- C) 200
- D) 1000

*Réponse: 100 itérations (packages/runtime-core/src/scheduler.ts)*

---

### Question 6
**Combien de phases a le processus de compilation de template ?**
- A) 2
- B) 3 ✅
- C) 4
- D) 5

*Réponse: 3 phases: Parse (template → AST), Transform (optimisation AST), Generate (AST → JavaScript)*

---

### Question 7
**Quel package gère la compatibilité avec Vue 2 ?**
- A) @vue/legacy
- B) @vue/compat ✅
- C) @vue/migration
- D) @vue/v2

*Réponse: Le package vue-compat fournit la couche de compatibilité Vue 2*

---

## NIVEAU MOYEN (Questions 8-17)

### Question 8
**Combien de WeakMaps différentes sont utilisées pour stocker les proxies réactifs ?**
- A) 1
- B) 2
- C) 4 ✅
- D) 8

*Réponse: 4 WeakMaps: reactiveMap, shallowReactiveMap, readonlyMap, shallowReadonlyMap*

---

### Question 9
**Quelle structure de données est utilisée pour le système de tracking des dépendances ?**
- A) Array
- B) Set
- C) Map
- D) Doubly-linked list ✅

*Réponse: Une liste doublement chaînée (doubly-linked list) avec des Links entre subscribers et dependencies*

---

### Question 10
**Quel est le nom du symbole utilisé pour tracker les itérations de tableaux ?**
- A) ARRAY_ITERATE_KEY ✅
- B) ITERATE_KEY
- C) ARRAY_KEY
- D) TRACK_ARRAY

*Réponse: ARRAY_ITERATE_KEY (packages/reactivity/src/arrayInstrumentations.ts)*

---

### Question 11
**Combien de méthodes de tableaux sont instrumentées pour la réactivité ?**
- A) 5
- B) 10
- C) 15
- D) 20+ ✅

*Réponse: Plus de 20 méthodes (includes, indexOf, push, pop, shift, unshift, splice, map, filter, etc.)*

---

### Question 12
**Quel PatchFlag a la valeur 1 ?**
- A) CLASS
- B) TEXT ✅
- C) STYLE
- D) PROPS

*Réponse: TEXT = 1, indique du contenu texte dynamique*

---

### Question 13
**Quelle valeur de PatchFlag indique qu'un nœud est en cache ?**
- A) 0
- B) 1
- C) -1 ✅
- D) -2

*Réponse: CACHED = -1 (les flags spéciaux sont négatifs)*

---

### Question 14
**Quel est le nom de la propriété ReactiveFlag pour vérifier si quelque chose est réactif ?**
- A) __v_reactive
- B) __v_isReactive ✅
- C) __isReactive
- D) __reactive

*Réponse: __v_isReactive (enum ReactiveFlags)*

---

### Question 15
**Comment nextTick est-il implémenté sous le capot ?**
- A) setTimeout
- B) requestAnimationFrame
- C) Promise.resolve().then() ✅
- D) setImmediate

*Réponse: Utilise une Promise résolue et currentFlushPromise*

---

### Question 16
**Quelle est la valeur du ShapeFlag pour ELEMENT ?**
- A) 0
- B) 1 ✅
- C) 2
- D) 4

*Réponse: ELEMENT = 1, c'est le premier flag*

---

### Question 17
**Combien de ConstantTypes différents existe-t-il pour le static hoisting ?**
- A) 3
- B) 4
- C) 5 ✅
- D) 6

*Réponse: 5 types: NOT_CONSTANT, CAN_SKIP_PATCH, CAN_HOIST, CAN_STRINGIFY, CAN_CACHE*

---

## NIVEAU DIFFICILE (Questions 18-22)

### Question 18
**Pourquoi push/pop/shift/unshift/splice pausent-ils le tracking pendant leur exécution ?**
- A) Pour améliorer les performances
- B) Pour éviter les boucles infinies ✅
- C) Pour éviter les fuites mémoire
- D) C'est un bug legacy

*Réponse: Pour éviter les boucles infinies (issue #2137), ces méthodes modifient length qui déclencherait des effets*

---

### Question 19
**Combien d'EffectFlags différents existent dans le système de réactivité ?**
- A) 6
- B) 7
- C) 8 ✅
- D) 9

*Réponse: 8 flags: ACTIVE, RUNNING, TRACKING, NOTIFIED, DIRTY, ALLOW_RECURSE, PAUSED, EVALUATED*

---

### Question 20
**Pourquoi includes/indexOf/lastIndexOf cherchent-ils deux fois dans les tableaux réactifs ?**
- A) Pour améliorer les performances
- B) Pour gérer les problèmes d'identité entre valeurs reactive et raw ✅
- C) C'est un bug
- D) Pour supporter IE11

*Réponse: Si la recherche avec la valeur reactive échoue, on réessaie avec toRaw() pour gérer les problèmes d'identité*

---

### Question 21
**Comment fonctionne le fast-path d'optimisation avec globalVersion ?**
- A) Compare les versions pour skip les computations inutiles ✅
- B) Stocke l'historique des changements
- C) Optimise le garbage collection
- D) Cache les résultats

*Réponse: globalVersion s'incrémente à chaque changement réactif, permet de déterminer rapidement si une recomputation est nécessaire*

---

### Question 22
**Quel est le rôle du concept de "Block Tree" ?**
- A) Organiser le code
- B) Diviser le template en blocs avec structure stable pour optimiser le diff ✅
- C) Gérer le lazy loading
- D) Améliorer le SEO

*Réponse: Les blocks (créés par v-if/v-for) ont une structure stable en interne, permettant de skip la plupart des enfants lors du diff*

---

## NIVEAU TRÈS DIFFICILE (Questions 23-25)

### Question 23
**Comment la fonction isOn détecte-t-elle rapidement qu'une key est un event handler ?**
- A) Regex
- B) startsWith('on')
- C) Vérification des charCodes pour 'on' suivi d'une majuscule ✅
- D) Map lookup

*Réponse: Vérifie charCodeAt(0) === 111 ('o') && charCodeAt(1) === 110 ('n') && charCodeAt(2) > 122 || < 97 (majuscule)*

---

### Question 24
**Pourquoi RefImpl stocke-t-il à la fois _value et _rawValue ?**
- A) Pour la compatibilité Vue 2
- B) Pour stocker séparément la version reactive et raw des objets ✅
- C) Pour le debugging
- D) Pour le garbage collection

*Réponse: _rawValue stocke la valeur raw, _value stocke la version reactive (via toReactive) - permet de comparer et éviter les conversions inutiles*

---

### Question 25
**Dans le scheduler, comment les jobs sont-ils ordonnés dans la queue ?**
- A) FIFO simple
- B) LIFO
- C) Par priorité fixe
- D) Par ID avec insertion par binary search ✅

*Réponse: Jobs triés par ID via binary search, garantit que les parents s'updatent avant les enfants (IDs plus bas), les pre-watchers avant les composants avec même ID*

---

## BONUS: Questions supplémentaires si besoin

### Question Bonus 1
**Quelle optimisation cacheStringFunction apporte-t-elle aux utilitaires comme camelize ?**
- A) Compression
- B) Mémoization avec cache Object.create(null) ✅
- C) Lazy evaluation
- D) Tree shaking

*Réponse: Crée un cache pour éviter de recalculer les transformations de strings déjà vues*

---

### Question Bonus 2
**Comment isIntegerKey détermine-t-il si une clé est un entier ?**
- A) typeof === 'number'
- B) Number.isInteger()
- C) Vérifie que parseInt(key) === key et !== 'NaN' et pas de '-' ✅
- D) Regex /^\d+$/

*Réponse: isString && key !== 'NaN' && key[0] !== '-' && '' + parseInt(key, 10) === key*

---

### Question Bonus 3
**Combien de node transforms sont appliqués dans le pipeline de compilation ?**
- A) 5
- B) 7
- C) 9 ✅
- D) 11

*Réponse: 9 transforms principaux: transformVBindShorthand, transformOnce, transformIf, transformMemo, transformFor, transformExpression, transformSlotOutlet, transformElement, transformText*

---

## Notes pour l'animateur

**Timing recommandé par question:**
- Questions faciles (1-7): 15-20 secondes
- Questions moyennes (8-17): 25-30 secondes
- Questions difficiles (18-22): 35-40 secondes
- Questions très difficiles (23-25): 45-60 secondes

**Points suggérés:**
- Facile: 500 points
- Moyen: 750 points
- Difficile: 1000 points
- Très difficile: 1500 points

**Tips:**
- Mélangez les difficultés pour garder l'engagement
- Commencez avec 2-3 questions faciles pour "échauffer"
- Intercalez des questions difficiles entre des moyennes
- Finissez avec une question très difficile pour le suspense !

**Références de code à montrer (optionnel):**
- Question 18: `packages/reactivity/src/arrayInstrumentations.ts`
- Question 20: Même fichier, la fonction `searchProxy`
- Question 23: `packages/shared/src/general.ts` fonction `isOn`
- Question 25: `packages/runtime-core/src/scheduler.ts` fonction `findInsertionIndex`

Bon meetup ! 🎉
