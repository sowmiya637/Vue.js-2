
#  Phase 2: Vue 3 Essentials (The Core)

##  Overview
This phase introduces the **core concepts of Vue 3**, focusing entirely on the **Composition API** using  
`<script setup>` — the **modern and recommended way** to write Vue components.

Vue follows a **declarative, reactive programming model**, meaning:
> You describe *what* the UI should look like based on state, and Vue handles *how* to update it.

---

#  The Vue Way of Thinking

- UI is a **function of state**
- When state changes → UI updates automatically
- No manual DOM manipulation
- Logic is grouped by **feature**, not lifecycle

---

#  Component Structure (Vue 3)

```vue
<template>
  <!-- HTML -->
</template>

<script setup>
  // JavaScript logic
</script>

<style scoped>
  /* CSS */
</style>
````

* `<template>` → UI
* `<script setup>` → state + logic
* `<style scoped>` → component-specific styles

---

#  1. Declarative Rendering

## What is Declarative Rendering?

Instead of manually updating the DOM, Vue lets you **declare** how data should appear.

### Mustache Syntax `{{ }}`

Used to display data inside the template.

```vue
<script setup>
import { ref } from 'vue'

const name = ref("Sowmiya")
</script>

<template>
  <h1>Hello {{ name }}</h1>
</template>
```

 When `name` changes, the UI updates automatically.

---

# 🧭 2. Directives

Directives are **special attributes** that tell Vue how to interact with the DOM.

---

## 2.1 `v-bind` (`:`) — Dynamic Attributes

Binds a variable to an HTML attribute.

```vue
<script setup>
const imageUrl = "logo.png"
</script>

<template>
  <img :src="imageUrl" />
</template>
```

✔️ Short form: `:src`

---

## 2.2 `v-on` (`@`) — Event Handling

Handles user interactions.

```vue
<script setup>
import { ref } from 'vue'

const count = ref(0)

const increment = () => {
  count.value++
}
</script>

<template>
  <button @click="increment">Count: {{ count }}</button>
</template>
```

✔️ Short form: `@click`

---

## 2.3 `v-model` — Two-Way Data Binding

Synchronizes input fields with state.

```vue
<script setup>
import { ref } from 'vue'
const username = ref("")
</script>

<template>
  <input v-model="username" />
  <p>Entered: {{ username }}</p>
</template>
```

✔️ Automatically handles input + update.

---

## 2.4 Conditional & List Rendering

### `v-if` vs `v-show`

```vue
<p v-if="isLoggedIn">Welcome!</p>
<p v-show="isLoggedIn">Welcome!</p>
```

| Directive | Behavior            |
| --------- | ------------------- |
| `v-if`    | Adds/removes DOM    |
| `v-show`  | Toggles CSS display |

---

### `v-for` — List Rendering

```vue
<script setup>
const courses = ["Vue", "Node", "MongoDB"]
</script>

<template>
  <ul>
    <li v-for="course in courses" :key="course">
      {{ course }}
    </li>
  </ul>
</template>
```

---

# 🔁 3. Reactivity API

## 3.1 `ref()` — For Primitive Values

```js
import { ref } from 'vue'

const count = ref(0)
count.value++
```

🔑 Access or modify using `.value`

---

## 3.2 `reactive()` — For Objects

```js
import { reactive } from 'vue'

const user = reactive({
  name: "Sowmiya",
  age: 21
})

user.age++
```

✔️ No `.value` needed
✔️ Deeply reactive

---

## When to Use What?

| Type         | Use          |
| ------------ | ------------ |
| Primitive    | `ref()`      |
| Object/Array | `reactive()` |

---

# 🧮 4. Computed Properties

## What are Computed Properties?

Computed properties **derive new data** from existing state and cache the result.

```vue
<script setup>
import { ref, computed } from 'vue'

const price = ref(100)
const quantity = ref(2)

const total = computed(() => price.value * quantity.value)
</script>

<template>
  <p>Total: {{ total }}</p>
</template>
```

✔️ Auto-updates
✔️ Efficient (cached)
✔️ No manual recalculation

---

# 👀 5. Watchers

## What are Watchers?

Watchers run **side effects** when reactive data changes.

Use when:

* Calling APIs
* Logging changes
* Syncing with localStorage

---

## Watching a Single Value

```vue
<script setup>
import { ref, watch } from 'vue'

const search = ref("")

watch(search, (newValue) => {
  console.log("Search changed:", newValue)
})
</script>
```

---

## Watching Multiple Values

```js
watch([price, quantity], () => {
  console.log("Price or quantity changed")
})
```

---

# 🔗 Computed vs Watch

| Computed        | Watch           |
| --------------- | --------------- |
| Returns a value | Performs action |
| Derived state   | Side effects    |
| Cached          | Not cached      |

---

# 🧠 How Everything Connects

| Concept            | Purpose       |
| ------------------ | ------------- |
| Mustache           | Display data  |
| Directives         | DOM behavior  |
| `ref` / `reactive` | State         |
| Computed           | Derived state |
| Watch              | Side effects  |

