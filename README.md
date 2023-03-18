# Vue.js官方示例代码学习文档



## 基础

### 你好世界

跟Vue说 'Hello world!'：

```vue
<script setup>
import { ref } from 'vue'

// “ref”是用来存储值的响应式数据源。
// 理论上我们在展示该字符串的时候不需要将其包装在 ref() 中，
// 但是在下一个示例中更改这个值的时候，我们就需要它了。
const message = ref('Hello World!')
</script>

<template>
  <h1>{{ message }}</h1>
</template>
```

这是一个使用Vue 3的组件，它展示了一个简单的“Hello World！”消息。

```html
<script setup>
import { ref } from 'vue'
    
const message = ref('Hello World!')
</script>
```

这段代码使用了Vue 3的脚本块，使用了新的`<script setup>`语法。它定义了一个名为`message`的响应式数据源，该数据源使用`ref()`函数来包装一个初始值为“Hello World！”的字符串。

`ref()`函数是Vue 3中用于创建响应式数据源的函数，它返回一个包含一个值的对象，该值可以被Vue追踪，并在其发生变化时自动更新关联的组件。

> `ref`函数是Vue 3中响应式编程的重要组成部分。与Vue 2中的数据绑定方式不同，Vue 3使用了**Proxy对象**和**Reflect API**来实现响应式数据的追踪和更新。`ref`函数是Vue 3中用于创建响应式数据源的基础工具函数，它可以用于创建简单的数据源，如字符串、数字、布尔值等，还可以用于创建对象、数组等复杂的数据源。

```html
<template>
  <h1>{{ message }}</h1>
</template>
```

这是Vue 3中的模板，它定义了如何展示组件。它包含了一个`<h1>`标签，其中的`{{ message }}`指令用于将`message`的值插入到文本中。

在这个简单的例子中，当组件渲染时，它会展示“Hello World！”消息。由于`message`是响应式数据源，当其发生变化时，组件会自动更新来反映新的值。

### 处理用户输入

这个示例展示了如何通过 v-on指令处理用户输入：

```vue
<script setup>
import { ref } from 'vue'

const message = ref('Hello World!')

function reverseMessage() {
  // 通过其 .value 属性
  // 访问/修改一个 ref 的值。
  message.value = message.value.split('').reverse().join('')
}

function notify() {
  alert('navigation was prevented.')
}
</script>

<template>
  <!--
    注意我们不需要在模板中写 .value，
    因为在模板中 ref 会自动“解包”。
  -->
  <h1>{{ message }}</h1>

  <!--
    绑定到一个方法/函数。
    这个 @click 语法是 v-on:click 的简写。
  -->
  <button @click="reverseMessage">Reverse Message</button>

  <!-- 也可以写成一个内联表达式语句 -->
  <button @click="message += '!'">Append "!"</button>

  <!--
    Vue 也为一些像 e.preventDefault() 和 e.stopPropagation()
    这样的常见任务提供了修饰符。
  -->
  <a href="https://vuejs.org" @click.prevent="notify">
    A link with e.preventDefault()
  </a>
</template>

<style>
button, a {
  display: block;
  margin-bottom: 1em;
}
</style>
```

这段代码使用Vue 3的`<script setup>`语法和`<template>`语法来实现一个简单的用户输入处理功能。

```vue
<script setup>
import { ref } from 'vue'

const message = ref('Hello World!')

function reverseMessage() {
  message.value = message.value.split('').reverse().join('')
}

function notify() {
  alert('navigation was prevented.')
}
</script>
```

这一部分代码使用ES模块的语法来声明变量和函数，并将它们导出到模板中使用。在这个块中，我们使用了Vue 3的`ref`函数来创建一个响应式数据源`message`，并定义了两个方法`reverseMessage`和`notify`。

1. `reverseMessage`方法用于翻转`message`变量的值：

- `message`是一个响应式数据源，它使用`ref`函数创建。在Vue 3中，要访问`ref`数据源的值，需要使用`.value`属性。因此，`message.value`表示`message`数据源的值。

- `.split('')`将`message.value`值转换为字符数组，每个字符都是数组的一个元素。`.reverse()`将该数组反转，`.join('')`将反转后的字符数组转换为字符串。最后，将反转后的字符串赋值给`message.value`，这样`message`的值就被翻转了。

> Q： `const ` 关键字通常被用来声明不可重新赋值的常量，为什么这里动态变化的响应式数据源可以使用`const`关键字声明？
>
> A：在 Vue 3中，使用`ref`函数创建的响应式数据源虽然可以通过变量名进行访问，**但实际上该变量名只是一个引用，指向了响应式数据源的值。**因此，在使用`ref`函数创建响应式数据源后，我们通常将其赋值给一个`const`常量，以确保该变量不能被重新赋值。
>
> 例如，下面的代码演示了如何使用`const`关键字和`ref`函数创建一个响应式数据源：
>
> ```javascript
> const message = ref('Hello World!');
> ```
>
> 在这个例子中，`message`是一个常量，它的值为一个响应式数据源，初始值为“Hello World！”字符串。由于使用了`const`关键字，`message`不能被重新赋值，否则会抛出一个`TypeError`错误。但是，实际上`message`引用的是一个响应式数据源的值，并非响应式数据源本身，因此我们可以通过修改响应式数据源的值来实现对`message`变量的更新。
>
> 例如，下面的代码演示了如何通过修改响应式数据源的值来更新`message`变量：
>
> ```javascript
> message.value = 'Hello Vue!';
> ```
>
> 在这个例子中，我们通过修改响应式数据源的值来更新`message`变量，将其值修改为“Hello Vue！”字符串。由于`message`变量是常量，我们无法对其重新赋值，但是可以通过修改响应式数据源的值来更新`message`变量的值。
>
> 总之，**变量名只是引用，我们修改的是由ref包裹的响应式数据源。**

2.`notify`方法用于在用户单击链接时显示一个警告框。

```vue
<template>
  <h1>{{ message }}</h1>
  <button @click="reverseMessage">Reverse Message</button>
  <button @click="message += '!'">Append "!"</button>
  <a href="https://vuejs.org" @click.prevent="notify">
    A link with e.preventDefault()
  </a>
</template>
```

这一部分代码使用Vue 3的模板语法来定义应用程序的用户界面。在这部分代码中，我们使用了Vue 3的插值语法`{{ }}`来将`ref`数据源自动解包的`message`变量的值显示在页面上。

> Q：为什么我不需要在模板上使用message.value来提供message的值？
>
> A：在Vue 3中，使用`ref`函数创建的响应式数据源可以通过`.value`属性来访问其值。例如，如果使用`ref`函数创建一个名为`message`的响应式数据源，那么要访问它的值，可以使用`message.value`。但是，在模板语法中，Vue 3会自动对`ref`数据源进行解包，即自动访问`.value`属性并将其值提供给模板。因此，在模板中，可以直接使用`{{ message }}`来显示`message`的值，而不需要使用`.value`属性。
>
> **解包（Unpacking）在编程中通常指从一个容器类型（如数组、元组、对象、响应式数据源等）中提取其中的值，并将其赋值给一个或多个变量或属性。**在JavaScript中，解包通常使用解构语法来完成。例如，可以使用数组解构语法`[a, b, c] = [1, 2, 3]`将数组`[1, 2, 3]`中的值解构并分别赋值给变量`a`、`b`、`c`。
>
> 在Vue 3中，`ref`函数创建的响应式数据源也需要使用解包来访问其值。在JavaScript中，要访问`ref`数据源的值，需要使用`.value`属性。但是，在Vue 3的模板语法中，Vue 3会自动对`ref`数据源进行解包，并将其值提供给模板。这样，在模板中就可以直接使用`{{ message }}`来显示`message`的值，而不需要使用`.value`属性。
>

最后，代码使用了Vue 3的事件绑定语法`@click`来绑定`reverseMessage`和`notify`方法到两个按钮和一个链接上。按钮用于触发`reverseMessage`方法，链接用于触发`notify`方法。

### Attribute绑定

在Web开发中，Attribute（属性）是指HTML元素上的属性，例如`class`、`id`、`title`等。这些属性可以用于控制元素的样式、行为和表现形式。**Attribute绑定是指将Vue实例中的数据与HTML元素的属性绑定在一起，使得数据的变化可以自动更新到HTML元素上。**在Vue中，可以使用v-bind指令来进行Attribute绑定。例如：

```html
<img v-bind:src="imageSrc">
```

这段代码中，`v-bind:src`指令将Vue实例中的`imageSrc`数据绑定到`<img>`元素的`src`属性上。当`imageSrc`的值发生变化时，该`<img>`元素的`src`属性也会自动更新。Attribute绑定可以用于控制HTML元素的样式、行为和表现形式。例如，可以将Vue实例中的数据绑定到`class`、`style`、`title`等属性上，从而动态改变元素的样式、提示信息等。此外，还可以将Vue实例中的方法绑定到事件属性上，从而实现交互功能，例如点击、鼠标悬停等。

现在我们将元素的 attribute / property 响应式地绑定到状态上：

```vue
<script setup>
import { ref } from 'vue'

const message = ref('Hello World!')
const isRed = ref(true)
const color = ref('green')

function toggleRed() {
  isRed.value = !isRed.value
}

function toggleColor() {
  color.value = color.value === 'green' ? 'blue' : 'green'
}
</script>

<template>
  <p>
    <span :title="message">
      Hover your mouse over me for a few seconds to see my dynamically bound title!
    </span>
  </p>

  <!--
  除了普通字符串之外，
  class 绑定还特别支持了对象和数组
  -->
  <p :class="{ red: isRed }" @click="toggleRed">
    This should be red... but click me to toggle it.
  </p>

  <!-- 样式绑定也支持对象和数组 -->
  <p :style="{ color }" @click="toggleColor">
    This should be green, and should toggle between green and blue on click.
  </p>
</template>

<style>
.red {
  color: red;
}
</style>
```

这段代码实现了一些简单的交互效果。

```vue
<script setup>
import { ref } from 'vue'

const message = ref('Hello World!')
const isRed = ref(true)
const color = ref('green')

function toggleRed() {
  isRed.value = !isRed.value
}

function toggleColor() {
  color.value = color.value === 'green' ? 'blue' : 'green'
}
</script>
```

这部分代码使用`ref`函数创建了三个响应式数据源：`message`、`isRed`和`color`。`function toggleRed()`定义了一个函数，用于切换`isRed`的值。该函数将`isRed`的值取反，从而实现了切换红色状态的功能。`function toggleColor()`定义了另一个函数，用于切换`color`的值。该函数根据`color`的当前值来切换`color`的值，从而实现在绿色和蓝色之间切换的功能。

> ```javascript
> color.value = color.value === 'green' ? 'blue' : 'green'
> ```
>
> 这句代码使用了JavaScript中的三元表达式（ternary operator），它的语法形式为：
>
> ```
> condition ? exprIfTrue : exprIfFalse
> ```
>
> 它的作用是根据`condition`表达式的值来决定返回`exprIfTrue`还是`exprIfFalse`。
>
> 在这个代码中，`color.value === 'green'`是一个条件表达式，它的值为`true`或`false`。如果`color.value`的值等于`'green'`，则条件表达式的值为`true`，否则为`false`。如果条件表达式的值为`true`，则三元表达式将返回`'blue'`，否则将返回`'green'`。因此，这句代码的作用是：如果`color.value`的值为`'green'`，则将其改为`'blue'`，否则将其改为`'green'`。这样就实现了在绿色和蓝色之间切换的功能。
>

```html
<template>
  <p>
    <span :title="message">
      Hover your mouse over me for a few seconds to see my dynamically bound title!
    </span>
  </p>

  <p :class="{ red: isRed }" @click="toggleRed">
    This should be red... but click me to toggle it.
  </p>

  <p :style="{ color }" @click="toggleColor">
    This should be green, and should toggle between green and blue on click.
  </p>
</template>
```

这部分代码定义了模板，使用了三个绑定：

- `:title="message"`将`<span>`元素的`title`属性绑定到`message`响应式数据源的值上。当鼠标悬停在该元素上时，将显示`message`的值。
- `:class="{ red: isRed }"`将`<p>`元素的`class`属性绑定到一个包含`red`属性的对象上，该对象的`red`属性的值等于`isRed`响应式数据源的值。当`isRed`为`true`时，该元素的`class`属性将包含`red`属性，从而显示为红色。
- `:style="{ color }"`将`<p>`元素的`style`属性绑定到一个包含`color`属性的对象上，该对象的`color`属性的值等于`color`响应式数据源的值。当`color`为`green`时，该元素的颜色将为绿色，当`color`为`blue`时，该元素的颜色将为蓝色。

### 条件与循环

我们可以通过 v-if 和 v-for 指令条件性地或循环地渲染内容：

```vue
<script setup>
import { ref } from 'vue'

const show = ref(true)
const list = ref([1, 2, 3])
</script>

<template>
  <button @click="show = !show">Toggle List</button>
  <button @click="list.push(list.length + 1)">Push Number</button>
  <button @click="list.pop()">Pop Number</button>
  <button @click="list.reverse()">Reverse List</button>

  <ul v-if="show && list.length">
    <li v-for="item of list">{{ item }}</li>
  </ul>
  <p v-else-if="list.length">List is not empty, but hidden.</p>
  <p v-else>List is empty.</p>
</template>
```

> 你可能会遇到该报错：Elements in iteration expect to have 'v-bind:key' directives.
>
> 这个警告信息是Vue的一个常见警告，它的含义是：
>
> 在使用`v-for`指令循环渲染元素时，每个元素都应该有一个唯一的`key`属性，用于帮助Vue更好地跟踪元素的变化。
>
> 这个警告信息通常出现在没有为`v-for`指令提供`key`属性时，例如：
>
> ```html
> <ul>
>   <li v-for="item in items">{{ item }}</li>
> </ul>
> ```
>
> 在这个例子中，`v-for`指令用于循环渲染`items`数组中的每个元素，但是没有为`<li>`元素提供唯一的`key`属性。这样做会导致Vue无法准确地追踪元素的变化，从而可能导致一些意想不到的问题。
>
> 为了解决这个问题，可以为`<li>`元素添加一个`key`属性，例如：
>
> ```html
> <ul>
>   <li v-for="item in items" :key="item.id">{{ item }}</li>
> </ul>
> ```
>
> 在这个例子中，我们使用`item.id`作为每个元素的`key`属性，这样可以确保每个元素都有一个唯一的`key`值，从而帮助Vue更好地跟踪元素的变化。需要注意的是，`key`属性的值应该是一个唯一的字符串，最好是每个元素独有的标识符。如果没有合适的标识符，可以使用元素在数组中的索引作为`key`属性的值，但这样可能会导致一些性能问题和不必要的渲染。
>

这段代码是一个Vue 3组件的模板代码和脚本代码，实现了一个简单的列表示例，包含了以下几个功能：

- 点击“toggle List”按钮可以切换列表的显示和隐藏；
- 点击“Push Number”按钮可以向列表中添加一个数字；
- 点击“Pop Number”按钮可以从列表中删除最后一个数字；
- 点击“Reverse List”按钮可以将列表中的元素顺序反转。

```javascript
<script setup>
  import {ref} from 'vue'

  const show = ref(true)
  const list = ref([1,2,3])
</script>
```

这段代码定义了两个响应式数据：`show`和`list`。`ref`函数用于创建一个响应式数据，它可以让Vue跟踪数据的变化，并在数据变化时自动更新相关的视图。在这个例子中，`show`和`list`都是使用`ref`函数创建的响应式数据。

```html
<template>
  <div>
    <button @click="show = !show">toggle List</button>
    <button @click="list.push(list.length + 1)">Push Number</button>
    <button @click="list.pop()">Pop Number</button>
    <button @click="list.reverse">Reverse List</button>
    <ul v-if="show && list.length">
      <li v-for="item of list " :key="item.id">{{  item  }}</li>
    </ul>
    <p v-else-if="list.length">List is not empty, but hidden.</p>
    <p v-else>List is empty.</p>
  </div>
  <hr/>
</template>
```

这是Vue 3组件的模板代码，包含了一个包裹在`<div>`元素中的按钮和列表元素。按钮用于控制列表的显示和隐藏，同时还提供了一些操作列表的按钮，例如添加、删除和反转列表等。

在列表元素中，使用`v-for`指令循环渲染列表中的每个元素，同时为每个元素添加了一个唯一的`key`属性，用于帮助Vue更好地跟踪元素的变化。列表的显示和隐藏通过`v-if`指令来控制，可以根据`show`数据的值来判断是否显示。

### 表单绑定

我们可以使用 v-model 指令在状态和表单输入之间创建双向绑定：

```vue
<script setup>
import { ref } from 'vue'

const text = ref('Edit me')
const checked = ref(true)
const checkedNames = ref(['Jack'])
const picked = ref('One')
const selected = ref('A')
const multiSelected = ref(['A'])
</script>

<template>
  <h2>Text Input</h2>
  <input v-model="text"> {{ text }}

  <h2>Checkbox</h2>
  <input type="checkbox" id="checkbox" v-model="checked">
  <label for="checkbox">Checked: {{ checked }}</label>

  <!--
    多个复选框可以绑定到
    相同的 v-model 数组
  -->
  <h2>Multi Checkbox</h2>
  <input type="checkbox" id="jack" value="Jack" v-model="checkedNames">
  <label for="jack">Jack</label>
  <input type="checkbox" id="john" value="John" v-model="checkedNames">
  <label for="john">John</label>
  <input type="checkbox" id="mike" value="Mike" v-model="checkedNames">
  <label for="mike">Mike</label>
  <p>Checked names: <pre>{{ checkedNames }}</pre></p>

  <h2>Radio</h2>
  <input type="radio" id="one" value="One" v-model="picked">
  <label for="one">One</label>
  <br>
  <input type="radio" id="two" value="Two" v-model="picked">
  <label for="two">Two</label>
  <br>
  <span>Picked: {{ picked }}</span>

  <h2>Select</h2>
  <select v-model="selected">
    <option disabled value="">Please select one</option>
    <option>A</option>
    <option>B</option>
    <option>C</option>
  </select>
  <span>Selected: {{ selected }}</span>

  <h2>Multi Select</h2>
  <select v-model="multiSelected" multiple style="width:100px">
    <option>A</option>
    <option>B</option>
    <option>C</option>
  </select>
  <span>Selected: {{ multiSelected }}</span>
</template>
```

这段代码使用Vue 3的`<script setup>`语法和模板语法，实现了多种表单元素的绑定和展示。

```html
<script setup>
import { ref } from 'vue'

const text = ref('Edit me')
const checked = ref(true)
const checkedNames = ref(['Jack'])
const picked = ref('One')
const selected = ref('A')
const multiSelected = ref(['A'])
</script>
```

这是使用`<script setup>`语法定义的一个Vue组件的脚本部分。在该部分中，首先使用`import`语句导入了Vue 3中的`ref`函数，用于创建响应式数据。然后使用`const`关键字定义了多个响应式数据，分别用于绑定不同类型的表单元素。

```html
<template>
  <h2>Text Input</h2>
  <input v-model="text"> {{ text }}

  <h2>Checkbox</h2>
  <input type="checkbox" id="checkbox" v-model="checked">
  <label for="checkbox">Checked: {{ checked }}</label>
    
  <h2>Multi Checkbox</h2>
  <input type="checkbox" id="jack" value="Jack" v-model="checkedNames">
  <label for="jack">Jack</label>
  <input type="checkbox" id="john" value="John" v-model="checkedNames">
  <label for="john">John</label>
  <input type="checkbox" id="mike" value="Mike" v-model="checkedNames">
  <label for="mike">Mike</label>
  <p>Checked names: <pre>{{ checkedNames }}</pre></p>

  <h2>Radio</h2>
  <input type="radio" id="one" value="One" v-model="picked">
  <label for="one">One</label>
  <br>
  <input type="radio" id="two" value="Two" v-model="picked">
  <label for="two">Two</label>
  <br>
  <span>Picked: {{ picked }}</span>

  <h2>Select</h2>
  <select v-model="selected">
    <option disabled value="">Please select one</option>
    <option>A</option>
    <option>B</option>
    <option>C</option>
  </select>
  <span>Selected: {{ selected }}</span>

  <h2>Multi Select</h2>
  <select v-model="multiSelected" multiple style="width:100px">
    <option>A</option>
    <option>B</option>
    <option>C</option>
  </select>
  <span>Selected: {{ multiSelected }}</span>
</template>
```

这是使用模板语法定义的Vue组件的模板部分。在该部分中，使用了多种表单元素，分别展示了不同类型表单元素的绑定和展示。其中：

- `<input v-model="text"> {{ text }}`：这是一个文本输入框，使用了`v-model`指令将输入框的值绑定到`text`变量上，并在后面展示该变量的值。
- `<input type="checkbox" id="checkbox" v-model="checked">`：这是一个复选框，使用了`v-model`指令将复选框的状态绑定到`checked`变量上，并在后面展示该变量的值。
- `<input type="checkbox" id="jack" value="Jack" v-model="checkedNames">`：这是一个多选复选框，使用了`v-model`指令将复选框的状态绑定到`checkedNames`数组上，并在下方展示该数组的值。
- `<input type="radio" id="one" value="One" v-model="picked">`：这是一组单选按钮，使用了`v-model`指令将单选按钮的值绑定到`picked`变量上，并在后面展示该变量的值。
- `<select v-model="selected">...</select>`：这是一个下拉列表框，使用了`v-model`指令将选中的选项的值绑定到`selected`变量上，并在后面展示该变量的值。
- `<select v-model="multiSelected" multiple style="width:100px">...</select>`：这是一个多选下拉列表框，使用了`v-model`指令将选中的选项的值绑定到`multiSelected`数组上，并在后面展示该数组的值。

### 简单组件

这里展示了最简单的组件，它接收一个prop并渲染出来：

```vue
<script setup>
import { ref } from 'vue'
import TodoItem from './TodoItem.vue'

const groceryList = ref([
  { id: 0, text: 'Vegetables' },
  { id: 1, text: 'Cheese' },
  { id: 2, text: 'Whatever else humans are supposed to eat' }
])
</script>

<template>
  <ol>
    <!--
      我们给每个 todo 项提供它所表示的 todo 对象，
      以便能够动态展示内容。
      同时还需要给每个组件提供一个“key”，
      这在指南的 v-for 部分有详细解释。
    -->
    <TodoItem
      v-for="item in groceryList"
      :todo="item"
      :key="item.id"
    ></TodoItem>
  </ol>
</template>
```

<div align="center">App.vue</div>

```vue
<script setup>
const props = defineProps({
  todo: Object
})
</script>

<template>
  <li>{{ todo.text }}</li>
</template>
```

<div align="center">TodoItem.vue</div>

事实上，照搬官方提供的TodoItem.vue并不能直接运行，因为`defineProps`需要引入，同时，在`<script setup>`中也无需手动配置props。

使用`defineProps`要安装 `@vue/runtime-core` 模块，可以使用 npm  命令。

使用 npm 命令安装：

```
npm install @vue/runtime-core
```

```vue
<template>
    <li>{{ todo.text }}</li>
</template>

<script setup>
import { defineProps } from '@vue/runtime-core';
    defineProps({
        todo:Object
    })

</script>
```

<div align="center">TodoItem.vue</div>

这样，TodoItem的内容就成功地在App上渲染出来。

## 实战

### Markdown编辑器

一个简单的markdown编辑器。

```vue
<script setup>
import { marked } from 'marked'
import { debounce } from 'lodash-es'
import { ref, computed } from 'vue'

const input = ref('# hello')

const output = computed(() => marked(input.value))

const update = debounce((e) => {
  input.value = e.target.value
}, 100)
</script>

<template>
  <div class="editor">
    <textarea class="input" :value="input" @input="update"></textarea>
    <div class="output" v-html="output"></div>
  </div>
</template>

<style>
body {
  margin: 0;
}

.editor {
  height: 100vh;
  display: flex;
}

.input,
.output {
  overflow: auto;
  width: 50%;
  height: 100%;
  box-sizing: border-box;
  padding: 0 20px;
}

.input {
  border: none;
  border-right: 1px solid #ccc;
  resize: none;
  outline: none;
  background-color: #f6f6f6;
  font-size: 14px;
  font-family: 'Monaco', courier, monospace;
  padding: 20px;
}

code {
  color: #f66;
}
</style>
```

> 如果你想在 Vue 3 的项目中使用 `marked` 和 `lodash-es` 这两个依赖项，可以使用 npm 命令来下载相应的包。
>
> 使用 npm 命令下载：
>
> ```
> npm install marked lodash-es
> ```
>
> 该命令将会在你的项目中安装 `marked` 和 `lodash-es` 包，并将它们添加到你的 `package.json` 文件中的 `dependencies` 中。安装完成后，你可以在项目的脚本部分中使用 `import` 语句来导入这些依赖项：
>
> ```js
> import { marked } from 'marked'
> import { debounce } from 'lodash-es'
> ```
>
> 需要注意的是，`marked` 和 `lodash-es` 都是第三方的 JavaScript 库，不属于 Vue 3 的核心模块，因此需要单独下载和安装。另外，如果你在浏览器端使用这些库，需要将它们添加到 `index.html` 文件中的 `<script>` 标签中，或者使用打包工具（如 webpack 或者 vite）来打包和引入这些库。

这段代码是一个 Vue 3 的单文件组件，包含了一个编辑器组件，可以实时预览 Markdown 文本的渲染效果。

```vue
<script setup>
import { marked } from 'marked'
import { debounce } from 'lodash-es'
import { ref, computed } from 'vue'

const input = ref('# hello')

const output = computed(() => marked(input.value))

const update = debounce((e) => {
  input.value = e.target.value
}, 100)
</script>
```

这部分代码是组件的脚本部分，使用了 Vue 3 的 `<script setup>` 语法。在这里，我们使用 `import` 语句导入了 `marked` 和 `lodash-es` 库的 `marked` 函数和 `debounce` 函数，以及 Vue 3 的 `ref` 和 `computed` 函数。

接着，我们使用 `ref` 函数创建了一个响应式的变量 `input`，用于存储 Markdown 文本的输入。使用 `computed` 函数创建了一个计算属性 `output`，用于将 `input` 中的 Markdown 文本转换为 HTML 字符串并展示到页面上。

> ```javascript
> const output = computed(() => marked(input.value))
> ```
>
> 在这里，计算属性 `output` 的值是通过调用 `marked` 函数将 `input.value` 中的 Markdown 文本转换为 HTML 字符串得到的。具体来说，**箭头函数** `() => marked(input.value)` 表示一个计算属性的 getter 函数，当 `input.value` 发生变化时，该函数会被重新调用，计算出新的 `output` 值并返回。
>
> 箭头函数是 ES6 引入的一种新的函数定义语法，它可以用更简洁的语法来定义函数。箭头函数的基本语法如下：
>
> ```
> (param1, param2, …, paramN) => { statements }
> ```
>
> 其中，**括号中的参数表示函数的参数列表，箭头 `=>` 后面的花括号中的语句表示函数体。如果函数体只有一条语句，可以省略花括号和 `return` 关键字**，例如：
>
> ```
> (param1, param2, …, paramN) => expression
> ```
>
> 这样的语法可以让我们写出更简洁、更易读的代码。
>
> 在 Vue 3 中，箭头函数常常用于定义计算属性、监听器、方法等。例如，在上面的代码中，我们使用箭头函数定义了计算属性 `output` 的 **getter 函数**：
>
> ```
> const output = computed(() => marked(input.value))
> ```
>
> 在 Vue 3 中，计算属性是一种特殊的响应式数据，它的值不是直接存储在变量中，而是根据其他响应式数据的变化而动态计算得到的。**计算属性的值是由 getter 函数计算得到的，当计算属性所依赖的响应式数据发生变化时，getter 函数会被重新计算，并返回新的计算属性值。**因此，在定义计算属性时，我们需要提供一个 getter 函数来计算属性值。
>
> 在上面的代码中，我们使用 `computed` 函数创建了一个计算属性 `output`，并将一个箭头函数 `() => marked(input.value)` 作为 getter 函数传递给了 `computed` 函数。这个 getter 函数接受 `input.value` 作为参数，使用 `marked` 函数将其转换为 HTML 字符串并返回，计算得到了计算属性 `output` 的值。
>

最后，我们使用 `debounce` 函数创建了一个函数 `update`，用于在用户输入时更新 `input` 的值，并将其绑定到 `textarea` 的 `@input` 事件上。

需要注意的是，`ref` 和 `computed` 函数是 Vue 3 的响应式 API，用于创建响应式的数据和计算属性。`debounce` 函数是 lodash-es 库中的一个函数，用于延迟函数的执行，避免频繁触发事件而导致性能问题。

```html
<template>
  <div class="editor">
    <textarea class="input" :value="input" @input="update"></textarea>
    <div class="output" v-html="output"></div>
  </div>
</template>
```

这部分代码是组件的模板部分，使用了 Vue 3 的模板语法。在这里，我们使用了 `v-bind` 指令将 `input` 的值绑定到 `textarea` 的 `value` 属性上，使用 `@input` 指令将 `update` 函数绑定到 `textarea` 的 `input` 事件上。同时，我们使用 `v-html` 指令将 `output` 的值渲染为 HTML 内容，并展示到页面的另一个 `div` 元素中。

### 获取数据

这个示例会通过 GitHub 的 API 获取最新的 Vue.js 提交信息并将其展示为列表，你可以在两个分支之间切换：

```vue
<script setup>
import { ref, watchEffect } from 'vue'

const API_URL = `https://api.github.com/repos/vuejs/core/commits?per_page=3&sha=`
const branches = ['main', 'v2-compat']

const currentBranch = ref(branches[0])
const commits = ref(null)

watchEffect(async () => {
  // 该 effect 会立即运行，
  // 并且在 currentBranch.value 改变时重新运行
  const url = `${API_URL}${currentBranch.value}`
  commits.value = await (await fetch(url)).json()
})

function truncate(v) {
  const newline = v.indexOf('\n')
  return newline > 0 ? v.slice(0, newline) : v
}

function formatDate(v) {
  return v.replace(/T|Z/g, ' ')
}
</script>

<template>
  <h1>Latest Vue Core Commits</h1>
  <template v-for="branch in branches">
    <input type="radio"
      :id="branch"
      :value="branch"
      name="branch"
      v-model="currentBranch">
    <label :for="branch">{{ branch }}</label>
  </template>
  <p>vuejs/vue@{{ currentBranch }}</p>
  <ul>
    <li v-for="{ html_url, sha, author, commit } in commits">
      <a :href="html_url" target="_blank" class="commit">{{ sha.slice(0, 7) }}</a>
      - <span class="message">{{ truncate(commit.message) }}</span><br>
      by <span class="author">
        <a :href="author.html_url" target="_blank">{{ commit.author.name }}</a>
      </span>
      at <span class="date">{{ formatDate(commit.author.date) }}</span>
    </li>
  </ul>
</template>

<style>
a {
  text-decoration: none;
  color: #42b883;
}
li {
  line-height: 1.5em;
  margin-bottom: 20px;
}
.author,
.date {
  font-weight: bold;
}
</style>
```

**注意，官方提供的代码并不够完善，它可能会出现该报错：<span style="color:darkred">Elements in iteration expect to have 'v-bind:key' directives.</span>**

这个警告是 Vue 给出的一种提示，用于帮助开发者正确地使用 `v-for` 指令。在使用 `v-for` 指令循环渲染元素时，每个元素都需要有一个唯一的 `key` 属性，以便 Vue 可以跟踪每个元素的状态。如果没有提供 `key` 属性，Vue 会给出上述警告，提醒开发者需要添加 `v-bind:key` 指令。

为了解决这个警告，我们需要在循环渲染元素时为每个元素添加一个唯一的 `key` 属性，上述部分代码可修改成：

```vue
<template v-for="branch in branches" :key="branch">
        <input type="radio" :id="branch" :value="branch" name="branch" v-model="currentBranch">
        <label :for="branch">{{ branch }}</label>
    </template>
```

以及这一段：

```vue
<li v-for="{ html_url, sha, author, commit } in commits">
      <a :href="html_url" target="_blank" class="commit">{{ sha.slice(0, 7) }}</a>
      - <span class="message">{{ truncate(commit.message) }}</span><br>
      by <span class="author">
        <a :href="author.html_url" target="_blank">{{ commit.author.name }}</a>
      </span>
      at <span class="date">{{ formatDate(commit.author.date) }}</span>
    </li>
```

上述代码从 `commits` 数组中的每个元素中提取了 `html_url`、`sha`、`author` 和 `commit` 四个属性，并分别赋值给了相应的变量。这种语法在某些情况下可能会导致解构失败，从而出现错误。为了避免这种情况，可以将解构语法改为使用括号包裹对象：

```vue
<li v-for="commit in commits" :key="commit.sha">
  <a :href="commit.html_url" target="_blank" class="commit">{{ commit.sha.slice(0,7) }}</a>
  -<span class="message">{{ truncate(commit.commit.message) }}</span><br>
  by<span class="author">
      <a :href="commit.author.html_url" target="_blank">{{ commit.commit.author.name }}</a>
  </span>
  at <span class="date">{{ formatDate(commit.commit.author.date) }}</span>
</li>
```

在上面的代码中，我们移除了对象解构语法，直接使用 `commit` 变量来访问每个元素的属性。同时，我们为 `li` 元素添加了一个 `key` 属性，以确保每个元素都有一个唯一的标识符。此外，我们还将 `html_url`、`author` 和 `commit` 对象中的属性访问方式进行了相应的修改，以适应新的语法。

需要注意的是，如果 `commits` 数组中的元素中没有某个属性，访问该属性时可能会出现错误。在这种情况下，可以使用可选链操作符（`?.`）来避免错误，例如：

```vue
<a :href="commit.author?.html_url" target="_blank">{{ commit.commit.author.name }}</a>
```

这样做可以在 `commit.author` 对象不存在时避免出现错误。

现在我们再来分析整个代码。这是一个 Vue 3 单文件组件，主要实现了以下功能：

- 显示最新的 Vue.js 核心库的提交记录；
- 支持切换不同分支的提交记录；
- 显示每个提交记录的 SHA、提交信息、作者和提交时间。

```vue
<template>
    <h1>Latest Vue Core Commits</h1>
    <template v-for="branch in branches" :key="branch">
        <input type="radio" :id="branch" :value="branch" name="branch" v-model="currentBranch">
        <label :for="branch">{{ branch }}</label>
    </template>
    <p>vuejs/vue@{{ currentBranch }}</p>
    <ul>
        <li v-for="commit in commits" :key="commit.sha">
            <a :href="commit.html_url" target="_blank" class="commit">{{ commit.sha.slice(0,7) }}</a>
            -<span class="message">{{ truncate(commit.commit.message) }}</span><br>
            by<span class="author">
            <a :href="commit.author.html_url" target="_blank">{{ commit.commit.author.name }}</a>
            </span>
            at <span class="date">{{ formatDate(commit.commit.author.date) }}</span>
        </li>
    </ul>
</template>
```

这里定义了组件的模板，包括一个标题、一个分支选择器、一个显示当前分支和一个提交记录列表。分支选择器中的每个选项都使用了 `v-for` 指令来遍历 `branches` 数组，并使用 `:key` 属性来为每个选项指定唯一的键值。提交记录列表中的每个记录都使用了 `v-for` 指令来遍历 `commits` 数组，并使用 `:key` 属性来为每个记录指定唯一的键值。

```vue
<script setup>
import {ref,watchEffect} from 'vue'

const API_URL = 'https://api.github.com/repos/vuejs/core/commits?per_page=3&sha='
const branches = ['main','v2-compat']

const currentBranch=ref(branches[0])
const commits = ref(null)

watchEffect(async()=>{
    const url = `${API_URL}${currentBranch.value}`
    commits.value = await(await fetch(url)).json()
})

function truncate(v){
    const newline = v.indexOf('\n')
    return newline > 0 ? v.slice(0,newline): v
}

function formatDate(v) {
  return v.replace(/T|Z/g, ' ')
}
</script>
```

在这里，我们首先导入了 `ref` 和 `watchEffect` 函数，用于定义响应式数据和监听数据变化，然后定义了 `API_URL` 常量和 `branches` 数组，分别表示 GitHub API 的 URL 和支持的分支列表。接着，我们使用 `ref` 函数定义了 `currentBranch` 和 `commits` 两个响应式变量，分别表示当前选择的分支和获取到的提交记录。在 `watchEffect` 函数中，我们使用 `async/await` 来获取指定分支的提交记录，并将获取到的数据赋值给 `commits` 变量。最后，我们定义了两个辅助函数 `truncate` 和 `formatDate`，分别用于截取提交信息的前几行和格式化日期。

整体来说，我们使用了 `v-for` 指令、`v-model` 指令、事件处理函数和计算属性等 Vue 相关的特性。其中，分支选择器中的每个选项都使用了 `v-model` 指令来绑定到 `currentBranch` 变量，以便在用户选择不同分支时能够自动更新提交记录。提交记录列表中的每个记录都使用了计算属性 `truncate(commit.commit.message)` 和 `formatDate(commit.commit.author.date)` 来格式化提交信息和日期。同时，每个记录的 SHA 和作者都使用了 `href` 属性来生成链接，以便用户能够跳转到 GitHub 上查看更多详情。

**获取数据并不一定要使用浏览器原生的`fetch`函数，使用Axios库是更为简便的选择。**

### 带有排序和过滤的网格

该示例创建了一个可复用的网格组件，并结合外部数据使用它：

```vue
<template>
    <table v-if="filteredData.length">
    <thead>
        <tr>
            <th v-for="key in columns" :key="key" @click="sortBy(key)" :class="{active : sortKey == key}">
            {{ capitalize(key) }}
            <span class="arrow" :class="sortOrders[key] > 0 ? 'asc' : 'dsc'"></span>
            </th>
        </tr>
    </thead>
    <tbody>
        <tr v-for="entry in filteredData" :key="entry">
            <td v-for="key in columns" :key="key">
                {{entry[key]}}
            </td>
        </tr>
    </tbody>
    </table>
    <p v-else>No matches found.</p>
</template>

<script setup>
import { ref, computed, defineProps } from 'vue'

const props = defineProps({
  data: Array,
  columns: Array,
  filterKey: String
})

const sortKey = ref('')
const sortOrders = ref(
  props.columns.reduce((o, key) => ((o[key] = 1), o), {})
)

const filteredData = computed(() => {
  let { data, filterKey } = props
  if (filterKey) {
    filterKey = filterKey.toLowerCase()
    data = data.filter((row) => {
      return Object.keys(row).some((key) => {
        return String(row[key]).toLowerCase().indexOf(filterKey) > -1
      })
    })
  }

  const key = sortKey.value
  if (key) {
    const order = sortOrders.value[key]
    data = data.slice().sort((a, b) => {
      a = a[key]
      b = b[key]
      return (a === b ? 0 : a > b ? 1 : -1) * order
    })
  }
  return data
})

function sortBy(key) {
  sortKey.value = key
  sortOrders.value[key] *= -1
}

function capitalize(str) {
  return str.charAt(0).toUpperCase() + str.slice(1)
}
</script>

<style>
table {
  border: 2px solid #42b983;
  border-radius: 3px;
  background-color: #fff;
}

th {
  background-color: #42b983;
  color: rgba(255, 255, 255, 0.66);
  cursor: pointer;
  user-select: none;
}

td {
  background-color: #f9f9f9;
}

th,
td {
  min-width: 120px;
  padding: 10px 20px;
}

th.active {
  color: #fff;
}

th.active .arrow {
  opacity: 1;
}

.arrow {
  display: inline-block;
  vertical-align: middle;
  width: 0;
  height: 0;
  margin-left: 5px;
  opacity: 0.66;
}

.arrow.asc {
  border-left: 4px solid transparent;
  border-right: 4px solid transparent;
  border-bottom: 4px solid #fff;
}

.arrow.dsc {
  border-left: 4px solid transparent;
  border-right: 4px solid transparent;
  border-top: 4px solid #fff;
}
</style>
```

<div align="center">Grid.vue</div>

```vue
<script setup>
import DemoGrid from './Grid.vue'
import { ref } from 'vue'

const searchQuery = ref('')
const gridColumns = ['name', 'power']
const gridData = [
  { name: 'Chuck Norris', power: Infinity },
  { name: 'Bruce Lee', power: 9000 },
  { name: 'Jackie Chan', power: 7000 },
  { name: 'Jet Li', power: 8000 }
]
</script>

<template>
  <form id="search">
    Search <input name="query" v-model="searchQuery">
  </form>
  <DemoGrid
    :data="gridData"
    :columns="gridColumns"
    :filter-key="searchQuery">
  </DemoGrid>
</template>
```

<div align="center">App.vue</div>

下面，我们来拆解分析Grid.vue组件：

这份代码实现了一个表格组件，包括数据的渲染、排序和搜索等功能。

从Vue中导入`ref`和`computed`方法，用于创建响应式数据和计算属性:
```javascript
import { ref, computed } from 'vue'
```

使用`defineProps()`方法定义`props`，`props`包括三个属性：data、columns和filterKey:
```javascript
const props = defineProps({
  data: Array,
  columns: Array,
  filterKey: String
})
```

使用ref()方法创建一个`sortKey`变量和一个`sortOrders`变量，用于控制表格的排序。其中sortKey是一个响应式变量，用于存储当前排序的列名。sortOrders也是一个响应式变量，它是一个对象，用于存储每一列的排序方式。

**对象的键名是每一列的名称，键值是1或-1，表示升序或降序。**这里使用了reduce方法将props.columns数组中的每一个元素作为键名，初始化为1作为键值，并最终返回一个对象:

```javascript
const sortKey = ref('')
const sortOrders = ref(
  props.columns.reduce((o, key) => ((o[key] = 1), o), {})
)
```

使用`computed()`方法创建一个filteredData计算属性，用于过滤和排序表格数据:

```javascript
const filteredData = computed(() => {  
  //定义了一个计算属性filteredData，它的值是一个函数，用于根据搜索关键字和排序状态对表格数据进行过滤和排序
  let { data, filterKey } = props //从props中获取表格数据和搜索关键字
  if (filterKey) {  //判断搜索关键字是否存在
    filterKey = filterKey.toLowerCase()  //将搜索关键字转换为小写字母
    data = data.filter((row) => {
      return Object.keys(row).some((key) => {
        return String(row[key]).toLowerCase().indexOf(filterKey) > -1
      })
    })//使用Array的some方法遍历每一行数据的所有列，只要有一列包含搜索关键字，就将这一行保留下来。这里使用了String的			toLowerCase方法将列的值转换为小写字母，再使用String的indexOf方法查找关键字是否存在于列的值中
  }
   
  const key = sortKey.value
  if (key) {
    const order = sortOrders.value[key]
    data = data.slice().sort((a, b) => {
      a = a[key]
      b = b[key]
      return (a === b ? 0 : a > b ? 1 : -1) * order
    })
  }
  return data
})
//获取当前排序列sortKey和排序方式sortOrders，然后使用Array的slice方法复制一份表格数据，以便进行排序后不影响原始数据。
//接着使用sort方法对数据进行排序，sort方法的参数是一个比较函数，用于指定排序规则。
//我们使用一个匿名函数作为比较函数，根据当前排序列sortKey和排序方式sortOrders来指定排序规则。
//我们先获取当前行的sortKey列的值，然后将两个值进行比较，根据升序或降序的要求，返回1或-1。
//最后，我们将过滤、排序后的结果返回，这个结果就是computed函数计算出来的filteredData计算属性的值。
```

`sortBy()`函数用于控制表格的排序，该函数接受一个参数key，表示排序的列。

```javascript
function sortBy(key) {
  sortKey.value = key
  sortOrders.value[key] *= -1
}
```

其中这行代码：

```javascript
sortOrders.value[key] *= -1
```

等价于：

```javascript
sortOrders.value[key] = sortOrders.value[key] \* -1 //可以简写为*=操作符
```

如果当前排序方式是升序，那么乘以-1后就变成了降序；如果当前排序方式是降序，那么乘以-1后就变成了升序。

`capitalize()`函数用于将字符串的首字母转换为大写字母。

```
function capitalize(str) {
  return str.charAt(0).toUpperCase() + str.slice(1)
}
```

`str.charAt(0)`获取字符串str的第一个字符，然后调用方法`toUpperCase()`将其转换为大写字母，再使用方法`slice(1)`获取字符串`str`的第二个字符到最后一个字符，返回这个子串。最后，使用+运算符将首字母大写的字符和剩余字符拼接起来，返回转换后的字符串。举个例子，如果传入的字符串是"apple"，那么这行代码的返回值就是"Apple"，即将字符串的首字母转换为大写字母后返回。

**整个代码的编写思路是先通过`defineProps()`方法定义`props`，然后使用`ref()`方法创建响应式数据，接着使用`computed()`方法创建计算属性，最后定义函数实现表格的排序和搜索功能。**

下面来分析模板部分。模板代码用于渲染表格，包括表头和表格数据。下面是代码的主要逻辑和相关指令的作用和用法意义：

1. 通过`v-if`指令判断filteredData数组的长度是否大于0，如果是，则显示表格，否则显示"No matches found."。
   ```vue
   <table v-if="filteredData.length">
     ...
   </table>
   <p v-else>No matches found.</p>
   ```

2. 通过`v-for`指令将表头和表格数据渲染为HTML元素。
   ```vue
   <th v-for="key in columns"
     @click="sortBy(key)"
     :class="{ active: sortKey == key }">
     {{ capitalize(key) }}
     <span class="arrow" :class="sortOrders[key] > 0 ? 'asc' : 'dsc'">
     </span>
   </th>
   
   <tr v-for="entry in filteredData">
     <td v-for="key in columns">
       {{entry[key]}}
     </td>
   </tr>
   ```

   v-for指令的参数是一个迭代器，用于遍历一个数组或对象。在这里，使用v-for指令将columns数组中的元素渲染为表头，将filteredData数组中的元素渲染为表格数据。

3. 通过`@click`指令绑定`sortBy()`函数，实现表格的排序功能。
   ```
   <th v-for="key in columns"
     @click="sortBy(key)"
     :class="{ active: sortKey == key }">
     ...
   </th>
   ```

   `@click`指令的参数是一个表达式，表示点击事件的处理函数。在这里，通过`@click`指令将`sortBy()`函数绑定到表头的点击事件上，当用户点击表头时，会触发`sortBy()`函数。

4. 通过`:class`指令绑定CSS类，实现表格的样式控制。
   ```
   <th v-for="key in columns"
     @click="sortBy(key)"
     :class="{ active: sortKey == key }">
     ...
   </th>
   
   <span class="arrow" :class="sortOrders[key] > 0 ? 'asc' : 'dsc'">
   </span>
   ```

   :class指令的参数是一个对象，对象的属性名表示CSS类名，属性值表示该CSS类是否生效。在这里，通过:class指令将"active"类绑定到当前排序列的表头上，表示该列当前处于排序状态。另外，通过:class指令将"asc"和"dsc"类绑定到排序箭头上，表示排序的升序和降序状态。

5. 通过{{}}语法绑定数据，实现表格数据的动态更新。
   ```
   <td v-for="key in columns">
     {{entry[key]}}
   </td>
   ```

   {{}}语法用于绑定数据，将数据动态渲染为HTML元素。在这里，通过{{}}语法将表格数据绑定到表格中的单元格上，随着数据的更新，表格数据也会动态更新。

对于App组件，有：

- 在App组件中，我们定义了三个变量：searchQuery、gridColumns和gridData。其中，searchQuery是一个响应式引用类型变量，gridColumns和gridData是普通的数组类型变量。我们通过将这些变量作为props传递给DemoGrid组件，从而将数据传递到了grid组件中。

- 在DemoGrid组件中，我们可以通过props接收这些数据，并在组件中使用它们。具体来说，我们在DemoGrid组件的props中定义了三个属性：data、columns和filter-key，分别对应了app组件中的gridData、gridColumns和searchQuery。通过这种方式，我们可以将app组件中的数据传递到其子组件DemoGrid中，并在DemoGrid组件中使用这些数据。


如果你要自己写一个类似的表格组件，可以按照以下步骤入手：

1. 定义props，包括数据、列和筛选关键字。
2. 创建响应式数据，用于控制表格的排序。
3. 创建计算属性，用于过滤和排序表格数据。
4. 定义函数，实现表格的排序和搜索功能。
5. 在模板中使用v-for指令渲染表格。
6. 在模板中使用v-bind指令绑定表格的数据和排序事件。
7. 在模板中使用v-model指令绑定筛选关键字。

### 树状视图

一个可以递归渲染自己的嵌套树组件：

```vue
<script setup>
import { ref, computed } from 'vue'

const props = defineProps({
  model: Object
})

const isOpen = ref(false)
const isFolder = computed(() => {
  return props.model.children && props.model.children.length
})

function toggle() {
  isOpen.value = !isOpen.value
}

function changeType() {
  if (!isFolder.value) {
    props.model.children = []
    addChild()
    isOpen.value = true
  }
}

function addChild() {
  props.model.children.push({ name: 'new stuff' })
}
</script>

<template>
  <li>
    <div
      :class="{ bold: isFolder }"
      @click="toggle"
      @dblclick="changeType">
      {{ model.name }}
      <span v-if="isFolder">[{{ isOpen ? '-' : '+' }}]</span>
    </div>
    <ul v-show="isOpen" v-if="isFolder">
      <!--
        一个可以通过其“name”选项递归渲染自己的组件，
        (如果使用单文件组件，则从文件名推断)
      -->
      <TreeItem
        class="item"
        v-for="model in model.children"
        :model="model">
      </TreeItem>
      <li class="add" @click="addChild">+</li>
    </ul>
  </li>
</template>
```

<div align="center">TreeItem.vue</div>

这是Vue官方示例代码中提供的TreeItem子组件代码。

**注意，该代码的写法不恰当，会导致报错**：<span style="color:darkred">**Unexpected mutation of "model" prop。**</span>

因为该代码试图直接修改一个prop。**在Vue中，props是单向数据流，只能从父组件传递到子组件。**如果我们想要修改一个prop，一个可行的解决方案是在子组件中使用一个本地的data属性来存储这个prop的值，并在这个本地的data属性上进行修改。这样就不会修改到父组件中的prop了。比如：

```javascript
const children = ref(props.model.children)
```

以下为可运行的作为子组件的TreeItem.vue代码：

```vue
<script setup>
import { ref, computed ,defineProps} from 'vue'

const props = defineProps({
  model: Object
})   //定义一个model prop，用于接收父组件传递的节点数据

const isOpen = ref(false) //表示当前节点是否展开，初始值为false
const isFolder = computed(() => {
  return props.model.children && props.model.children.length
})   //一个计算属性，判断是否拥有子节点，如果有则确认该节点为文件夹

const children = ref(props.model.children) //创建了一个新的响应式引用对象children，并将props赋值给它

function toggle() {
  isOpen.value = !isOpen.value
}

function changeType() {
  if (!isFolder.value) {
    children.value= []
    addChild()
    isOpen.value = true
  }
}   //用于切换节点类型。若当前节点非文件夹，则清空children数据并添加一个新的子节点

function addChild() {
  children.value.push({ name: 'new stuff' })
}   //用于向children数组添加一个新的子节点
</script>

<template>
  <li>
      <!-- 渲染节点名称和展开/收起按钮 -->
    <div
      :class="{ bold: isFolder }"
      @click="toggle"
      @dblclick="changeType">
      {{ model.name }}
      <span v-if="isFolder">[{{ isOpen ? '-' : '+' }}]</span>
    </div>
    <ul v-show="isOpen" v-if="isFolder">
      <!--
        一个可以通过其“name”选项递归渲染自己的组件，
        (如果使用单文件组件，则从文件名推断)
      -->
      <TreeItem
        class="item"
        v-for="model in model.children" :key="model.id"
        :model="model">
      </TreeItem>
        <!-- 渲染添加子节点按钮 -->
      <li class="add" @click="addChild">+</li>
    </ul>
  </li>
</template>
```

然后是作为父组件的App.vue代码：

```vue
<script setup>
import { ref } from 'vue'
import TreeItem from './TreeItem.vue'

const treeData = ref({
  name: 'My Tree',
  children: [
    { name: 'hello' },
    { name: 'world' },
    {
      name: 'child folder',
      children: [
        {
          name: 'child folder',
          children: [{ name: 'hello' }, { name: 'world' }]
        },
        { name: 'hello' },
        { name: 'world' },
        {
          name: 'child folder',
          children: [{ name: 'hello' }, { name: 'world' }]
        }
      ]
    }
  ]
})
</script>

<template>
  <ul>
    <TreeItem class="item" :model="treeData"></TreeItem>
  </ul>
</template>

<style>
.item {
  cursor: pointer;
  line-height: 1.5;
}
.bold {
  font-weight: bold;
}
</style>
```

这段代码定义了一个名为 `treeData` 的响应式引用对象，该对象包含树形结构的数据。在模板中，它将 `treeData` 对象传递给名为 `TreeItem` 的子组件，用于渲染树形结构。在子组件中，它使用 `model prop` 来获取当前节点的数据，并根据数据的内容来渲染节点的内容和子节点。如果当前节点有子节点，则会递归地渲染子节点的内容。

### SVG图像

这个示例将会生成一个可调节的SVG雷达图像：

```javascript
export function valueToPoint(value,index,total){
    const x = 0
    const y = -value * 0.8
    const angle = ((Math.PI * 2) / total) * index
    const cos = Math.cos(angle)
    const sin = Math.sin(angle)
    const tx = x * cos - y * sin + 100
    const ty = x * sin + y * cos + 100
    return {
        x: tx,
        y: ty
    }
}
```

<div align="center">util.js</div>

这段代码定义了一个名为 `valueToPoint` 的函数，用于将给定的数值转换为二维坐标系中的点。具体来说，它的作用如下：

1. 接收三个参数：`value` 表示要转换的数值，`index` 表示该数值在数据数组中的索引，`total` 表示数据数组的长度。
2. 计算该数值在二维坐标系中的坐标。首先将 x 坐标设为 0，将 y 坐标设为 `-value * 0.8`，这里的乘法系数 0.8 是为了将数值在 y 方向上的范围缩小，以适应坐标系的大小。然后根据该数值在数据数组中的索引和数据数组的长度，计算出该数值在坐标系中对应的角度，并根据角度计算出 cos 和 sin 值。最后，将 x 和 y 坐标分别乘以 cos 和 sin 值，并加上一个偏移量 (100, 100)，得到该数值在坐标系中的最终坐标。
3. 返回一个包含 x 和 y 坐标的对象，表示该数值在坐标系中的点的位置。

```vue
<script setup>
import { computed, defineProps} from 'vue'
import { valueToPoint } from './util.js'

const props = defineProps({
  stat: Object,
  index: Number,
  total: Number
})

const point = computed(() =>
  valueToPoint(+props.stat.value + 10, props.index, props.total)
)
//props.stat.value 表示组件的一个 prop，它包含了当前数据标签的值。
//+props.stat.value 将 props.stat.value 转换为数值类型。
//+props.stat.value + 10 在 props.stat.value 的基础上加上一个偏移量 10，以使得数据标签在雷达图中不会被覆盖。
//valueToPoint 是一个函数，用于将给定的数值转换为二维坐标系中的点的坐标。它接收三个参数：要转换的数值、该数值在数据数组中的索引、数据数组的长度。
</script>

<template>
  <text :x="point.x" :y="point.y">{{stat.label}}</text>
</template>
```

<div align="center">AxisLabel.vue</div>

该组件的作用是在雷达图中显示数据标签，将数据标签转换为二维坐标，并在对应的位置上渲染文本。

具体来说，这段代码的实现逻辑如下：

1. 引入 `computed` 函数和 `valueToPoint` 函数，用于计算数据标签在二维坐标系中的位置。

2. 使用 `defineProps` 函数定义组件的 props，包括 `stat`、`index` 和 `total` 三个属性。`stat` 表示当前数据标签的信息，包括 `label` 和 `value` 两个属性；`index` 表示当前数据标签在数据数组中的索引；`total` 表示数据数组的长度。

3. 使用 `computed` 函数计算数据标签在二维坐标系中的位置。首先将 `props.stat.value` 转换为数值类型，并加上一个偏移量 10。

   > `valueToPoint` 函数将给定的数值转换为二维坐标系中的点的坐标，但是这里的**数值是从数据中获取的**，**数据的范围和取值不确定**，因此需要加上一个偏移量来调整数据标签在坐标系中的位置，以避免其与数据点重合。**加上偏移量后，数据标签会在数据点的外侧显示，使得数据点和数据标签都能够清晰地展示出来，提高可视化效果和数据的可读性**。

   然后调用 `valueToPoint` 函数将该数值转换为二维坐标系中的点。这里使用了 Vue 3 的响应式特性，当组件的 props 改变时，`computed` 函数会重新计算并更新 `point` 的值。

4. 在模板中使用 `text` 元素渲染数据标签。使用 `:x` 和 `:y` 绑定计算出的 `point` 对象的 `x` 和 `y` 属性，以指定文本在二维坐标系中的位置；使用 `{{stat.label}}` 显示数据标签的文本内容。

```vue
<script setup>
import AxisLabel from './AxisLabel.vue';
import { computed, defineProps} from 'vue';
import { valueToPoint } from '@/util';

const props = defineProps({
  stats: Array
})

const points = computed(() => {
  const total = props.stats.length
  return props.stats
    .map((stat, i) => {
      const { x, y } = valueToPoint(stat.value, i, total)
      return `${x},${y}`
    })
    .join(' ')
})
</script>

<template>
  <g>
    <polygon :points="points"></polygon>
    <circle cx="100" cy="100" r="80"></circle>
    <axis-label
      v-for="(stat, index) in stats"
      :key="stat"
      :stat="stat"
      :index="index"
      :total="stats.length"
    >
    </axis-label>
  </g>
</template>
```

<div align="center">PolyGraph.vue</div>

这段代码实现了一个雷达图组件，它根据传入的数据数组 `props.stats` 绘制出一个多边形，并在多边形的顶点处显示数据标签。

具体来说，这段代码的实现逻辑如下：

1. 引入 `AxisLabel` 组件、`computed` 函数、`defineProps` 函数和 `valueToPoint` 函数。

2. 使用 `defineProps` 函数定义组件的 props，包括 `stats` 属性，它表示数据数组，每个元素包含 `label` 和 `value` 两个属性。

3. 使用 `computed` 函数计算多边形的顶点坐标。首先获取数据数组的长度 `total`，然后使用 `map` 方法遍历数据数组，对每个数据元素调用 `valueToPoint` 函数，将其转换为二维坐标系中的点的坐标，并将其转换为字符串格式 `${x},${y}`，最后使用 `join` 方法将所有顶点坐标连接起来，形成一个多边形的顶点坐标字符串。

4. 在模板中使用 `g` 元素渲染雷达图。首先使用 `polygon` 元素渲染多边形，将 `points` 属性绑定到之前计算得到的顶点坐标字符串。然后使用 `circle` 元素渲染圆形，作为多边形的外框。最后使用 `AxisLabel` 组件渲染数据标签，对每个数据元素都遍历一遍，将其传递给 `AxisLabel` 组件进行渲染，并传递 `index` 和 `total` 两个参数，用于计算数据标签在坐标系中的位置。

总体来说，这段代码的作用是根据传入的数据数组，绘制出一个雷达图，多边形表示数据的分布情况，数据标签显示在多边形的顶点处，以便用户更直观地了解数据的具体数值。

### 带过渡动效的模态框

可定制插槽和CSS过渡效果的模态框组件：

```vue
<script setup>
import { defineProps } from 'vue';
defineProps({
  show: Boolean
})
</script>

<template>
  <Transition name="modal">
    <div v-if="show" class="modal-mask">
      <div class="modal-container">
        <div class="modal-header">
          <slot name="header">default header</slot>
        </div>

        <div class="modal-body">
          <slot name="body">default body</slot>
        </div>

        <div class="modal-footer">
          <slot name="footer">
            default footer
            <button
              class="modal-default-button"
              @click="$emit('close')"
            >OK</button>
          </slot>
        </div>
      </div>
    </div>
  </Transition>
</template>

<style>
.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  transition: opacity 0.3s ease;
}

.modal-container {
  width: 300px;
  margin: auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;
}

.modal-header h3 {
  margin-top: 0;
  color: #42b983;
}

.modal-body {
  margin: 20px 0;
}

.modal-default-button {
  float: right;
}

/*
 * 对于 transition="modal" 的元素来说
 * 当通过 Vue.js 切换它们的可见性时
 * 以下样式会被自动应用。
 *
 * 你可以简单地通过编辑这些样式
 * 来体验该模态框的过渡效果。
 */

.modal-enter-from {
  opacity: 0;
}

.modal-leave-to {
  opacity: 0;
}

.modal-enter-from .modal-container,
.modal-leave-to .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}
</style>
```

<div align="center">Modal.vue</div>

这段代码实现了一个基本的模态框组件，通过传入 `show` 属性来控制模态框的显示和隐藏，同时支持自定义模态框的头部、主体和底部。

具体来说，这段代码的实现逻辑如下：

1. 使用 `defineProps` 函数定义组件的 props，包括 `show` 属性，它表示模态框是否显示。
2. 在模板中使用 `Transition` 组件来实现过渡效果，其中 `name` 属性为过渡动画的名称，可以在 CSS 中定义相关的动画效果。
3. 在 `div` 元素中使用 `v-if` 指令来根据 `show` 属性的值来控制模态框的显示和隐藏。
4. 在模态框的主体中，使用 `slot` 元素来支持自定义模态框的头部、主体和底部。具体来说，使用 `slot` 元素来分别定义 `header`、`body` 和 `footer` 插槽，并提供默认的插槽内容。其中，`header` 插槽用于自定义模态框的头部，`body` 插槽用于自定义模态框的主体，`footer` 插槽用于自定义模态框的底部。如果不提供自定义插槽，则使用默认的插槽内容。
5. 在 `footer` 插槽中，提供一个默认的底部按钮，用于关闭模态框。当点击该按钮时，调用 `$emit` 方法触发 `close` 事件，从而关闭模态框。

```vue
<script setup>
import Modal from './Modal.vue'
import { ref } from 'vue'

const showModal = ref(false)
</script>

<template>
  <button id="show-modal" @click="showModal = true">Show Modal</button>

  <Teleport to="body">
    <!-- 使用这个 modal 组件，传入 prop -->
    <modal :show="showModal" @close="showModal = false">
      <template #header>
        <h3>custom header</h3>
      </template>
    </modal>
  </Teleport>
</template>
```

<div align="center">App.vue</div>

这段代码实现了一个简单的示例，包含一个按钮和一个模态框组件。当用户点击按钮时，会显示模态框，当用户点击模态框的关闭按钮时，会隐藏模态框。

具体来说，这段代码的实现逻辑如下：

1. 引入 `Modal` 组件和 `ref` 函数。
2. 使用 `ref` 函数创建一个名为 `showModal` 的响应式引用，它的初始值为 `false`，用于控制模态框的显示和隐藏。
3. 在模板中，使用 `button` 元素渲染一个按钮，当用户点击该按钮时，会将 `showModal` 的值设置为 `true`，从而显示模态框。
4. 使用 `Teleport` 组件将模态框组件渲染到 `body` 元素中，以便在页面中的任何位置显示模态框。
5. 在 `Teleport` 组件内部，使用 `Modal` 组件来实现模态框的显示和隐藏。将 `show` 属性绑定到 `showModal` 的值，从而控制模态框的显示和隐藏。同时，在模态框的头部中使用 `slot` 元素来自定义头部内容，将 `h3` 元素作为 `header` 插槽的默认内容。
6. 给模态框组件绑定 `close` 事件，当用户点击模态框的关闭按钮时，会触发该事件，从而将 `showModal` 的值设置为 `false`，从而隐藏模态框。

总体来说，这段代码展示了如何使用 Vue 3 中的 `Teleport` 组件将模态框渲染到页面中的任何位置，并展示了如何使用 `slot` 元素自定义模态框的头部内容。同时，通过使用响应式引用 `showModal`，实现了模态框的显示和隐藏。

### 带过渡动效的列表

通过内建的 <TransitionGroup> 实现“FLIP”列表过渡效果。https://aerotwist.com/blog/flip-your-animations/

```vue
<script setup>
import { shuffle as _shuffle } from 'lodash-es'
import { ref } from 'vue'

const getInitialItems = () => [1, 2, 3, 4, 5]
const items = ref(getInitialItems())
let id = items.value.length + 1

function insert() {
  const i = Math.round(Math.random() * items.value.length)
  items.value.splice(i, 0, id++)
}

function reset() {
  items.value = getInitialItems()
}

function shuffle() {
  items.value = _shuffle(items.value)
}

function remove(item) {
  const i = items.value.indexOf(item)
  if (i > -1) {
    items.value.splice(i, 1)
  }
}
</script>

<template>
  <button @click="insert">insert at random index</button>
  <button @click="reset">reset</button>
  <button @click="shuffle">shuffle</button>

  <TransitionGroup tag="ul" name="fade" class="container">
    <div v-for="item in items" class="item" :key="item">
      {{ item }}
      <button @click="remove(item)">x</button>
    </div>
  </TransitionGroup>
</template>

<style>
.container {
  position: relative;
  padding: 0;
}

.item {
  width: 100%;
  height: 30px;
  background-color: #f3f3f3;
  border: 1px solid #666;
  box-sizing: border-box;
}

/* 1. 声明过渡效果 */
.fade-move,
.fade-enter-active,
.fade-leave-active {
  transition: all 0.5s cubic-bezier(0.55, 0, 0.1, 1);
}

/* 2. 声明进入和离开的状态 */
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: scaleY(0.01) translate(30px, 0);
}

/* 3. 确保离开的项目被移除出了布局流
      以便正确地计算移动时的动画效果。 */
.fade-leave-active {
  position: absolute;
}
</style>
```

这段代码实现了一个基于 Vue 3 和 `TransitionGroup` 组件的简单动态列表，包含插入、删除、重置和打乱顺序等操作，并提供了一个简单的过渡效果。

具体来说，这段代码的实现逻辑如下：

1. 引入 `lodash-es` 库中的 `shuffle` 函数和 `ref` 函数。
2. 创建一个名为 `items` 的响应式引用，初始值为一个包含 5 个元素的数组。
3. 定义一个 `getInitialItems` 函数，用于返回初始的数组，其中包含 5 个元素。
4. 定义 `id` 变量，用于生成新的元素 ID。
5. 定义 `insert` 函数，用于在随机的位置插入一个新的元素。
6. 定义 `reset` 函数，用于将列表重置为初始状态，即包含 5 个元素的数组。
7. 定义 `shuffle` 函数，用于随机打乱列表中元素的顺序。
8. 定义 `remove` 函数，用于移除指定的元素。
9. 在模板中，使用 `button` 元素渲染三个操作按钮，分别对应插入、重置和打乱顺序操作。
10. 使用 `TransitionGroup` 组件将元素列表渲染为一个 `ul` 元素，并为其添加一个名为 `fade` 的过渡效果。
11. 在 `TransitionGroup` 组件内部，使用 `v-for` 指令遍历 `items` 数组，并将每个元素渲染为一个 `div` 元素。将 `:key` 属性绑定到元素的 ID 上，以便 Vue 可以正确地跟踪每个元素的状态。
12. 在每个 `div` 元素内部，渲染元素的值，并添加一个按钮，用于移除当前元素。将按钮的 `@click` 事件绑定到 `remove` 函数，传入当前元素作为参数。
13. 在样式中，声明一个名为 `fade` 的过渡效果，并定义进入和离开的转换效果。使用 `TransitionGroup` 组件提供的 CSS 类名，将过渡效果应用于进入、离开和移动状态。

总体来说，这段代码展示了在 Vue 3 中使用 `TransitionGroup` 组件实现动态列表和简单过渡效果的方法，以及如何使用 `ref` 函数创建响应式引用，并使用 `lodash-es` 库中的函数进行操作。

### TodoMVC

一个完全标准的TodoMVC实现：

```javascript
<script setup>
import { ref, computed, watchEffect } from 'vue'

const STORAGE_KEY = 'vue-todomvc' //用于在本地存储中存储待办事项列表的数据。

const filters = {
  all: (todos) => todos,
  active: (todos) => todos.filter((todo) => !todo.completed),
  completed: (todos) => todos.filter((todo) => todo.completed)
}   //用于定义不同的筛选条件及其对应的过滤函数。

// 状态
const todos = ref(JSON.parse(localStorage.getItem(STORAGE_KEY) || '[]'))
//创建一个响应式引用 todos，初始值为从本地存储中读取的待办事项列表数据
//如果本地存储中没有数据，则初始值为一个空数组
const visibility = ref('all')
//创建一个响应式引用 visibility，初始值为字符串 'all'，表示当前的筛选条件为“全部”。
const editedTodo = ref()
//创建一个响应式引用 editedTodo，用于表示当前正在编辑中的待办事项。

// 获取的状态
const filteredTodos = computed(() => filters[visibility.value](todos.value))
//创建一个计算属性 filteredTodos，用于根据当前筛选条件过滤待办事项列表。
const remaining = computed(() => filters.active(todos.value).length)
//创建一个计算属性 remaining，用于计算未完成的待办事项数量。

// 处理路由
window.addEventListener('hashchange', onHashChange)
onHashChange()//监听路由变化，当路由变化时，根据路由切换当前的筛选条件。

// 状态持久化
watchEffect(() => {
  localStorage.setItem(STORAGE_KEY, JSON.stringify(todos.value))
})//监听待办事项列表的变化，当待办事项列表发生变化时，将新的列表数据存储到本地存储中。

//用于标记所有待办事项为已完成或未完成。
function toggleAll(e) {
  todos.value.forEach((todo) => (todo.completed = e.target.checked))
}
//用于添加一个新的待办事项
function addTodo(e) {
  const value = e.target.value.trim()
  if (value) {
    todos.value.push({
      id: Date.now(),
      title: value,
      completed: false
    })
    e.target.value = ''
  }
}
//用于删除一个待办事项
function removeTodo(todo) {
  todos.value.splice(todos.value.indexOf(todo), 1)
}
//用于开始编辑一个待办事项。
let beforeEditCache = ''
function editTodo(todo) {
  beforeEditCache = todo.title
  editedTodo.value = todo
}
//用于取消编辑一个待办事项。
function cancelEdit(todo) {
  editedTodo.value = null
  todo.title = beforeEditCache
}
//用于取消编辑一个待办事项。
function doneEdit(todo) {
  if (editedTodo.value) {
    editedTodo.value = null
    todo.title = todo.title.trim()
    if (!todo.title) removeTodo(todo)
  }
}
//用于删除所有已完成的待办事项。
function removeCompleted() {
  todos.value = filters.active(todos.value)
}

function onHashChange() {
  const route = window.location.hash.replace(/#\/?/, '')
  if (filters[route]) {
    visibility.value = route
  } else {
    window.location.hash = ''
    visibility.value = 'all'
  }
}
</script>
```

这段代码实现了一个简单的待办事项列表，包含添加、编辑、删除、标记完成等功能，并支持根据路由切换不同的筛选条件。

以下为具体分析：

```javascript
import { ref, computed, watchEffect } from 'vue';
```

这行代码使用了 `import` 语句从 Vue 3 中导入了 `ref`、`computed` 和 `watchEffect` 等函数。

```javascript
const STORAGE_KEY = 'vue3-todo-list';
```

这行代码定义了一个名为 `STORAGE_KEY` 的常量，用于指定本地存储中待办事项列表的键名。

```javascript
const filters = {
  all: () => true,
  active: (todo) => !todo.completed,
  completed: (todo) => todo.completed
};
```

这行代码定义了一个名为 `filters` 的对象，其中包括了不同的筛选条件及其对应的过滤函数。例如，`all` 筛选条件对应的过滤函数返回 `true`，表示不做任何过滤；`active` 筛选条件对应的过滤函数返回未完成的待办事项；`completed` 筛选条件对应的过滤函数返回已完成的待办事项。

```javascript
const todos = ref(JSON.parse(localStorage.getItem(STORAGE_KEY)) || []);
```

这行代码使用了 `ref` 函数创建了一个名为 `todos` 的响应式引用，它的初始值为从本地存储中获取的待办事项列表。如果本地存储中没有待办事项列表，则初始值为一个空数组。

```javascript
const todo = ref('');
```

这行代码使用了 `ref` 函数创建了一个名为 `todo` 的响应式引用，它的初始值为空字符串。

```javascript
const visibility = ref('all');
```

这行代码使用了 `ref` 函数创建了一个名为 `visibility` 的响应式引用，它的初始值为 `all`，表示默认显示所有待办事项。

```javascript
const remaining = computed(() => {
  return filters.active(todos.value).length;
});
```

这行代码使用了 `computed` 函数创建了一个名为 `remaining` 的计算属性，它的值为未完成的待办事项的数量。

```javascript
const filteredTodos = computed(() => {
  return filters[visibility.value](todos.value);
});
```

这行代码使用了 `computed` 函数创建了一个名为 `filteredTodos` 的计算属性，它的值为根据当前的筛选条件过滤后的待办事项列表。

```javascript
watchEffect(() => {
  localStorage.setItem(STORAGE_KEY, JSON.stringify(todos.value));
});
```

这行代码使用了 `watchEffect` 函数创建了一个副作用函数，它会在 `todos` 的值发生变化时自动执行，将新的待办事项列表存储到本地存储中。

```javascript
function addTodo() {
  const text = todo.value.trim();
  if (text.length === 0) {
    return;
  }
  todos.value.push({
    id: Date.now(),
    text,
    completed: false
  });
  todo.value = '';
}
```

这是一个名为 `addTodo` 的函数，它会添加一个新的待办事项到 `todos` 中。首先，它会获取输入框中的文本，然后根据文本长度判断是否为空。如果不为空，则将一个新的待办事项添加到 `todos` 中，包括一个自动生成的 `id`、文本和完成状态。最后，清空输入框中的文本。

```javascript
function removeTodo(todo) {
  const index = todos.value.indexOf(todo);
  todos.value.splice(index, 1);
}
```

这是一个名为 `removeTodo` 的函数，它会从 `todos` 中删除指定的待办事项。首先，它会获取待删除的待办事项在 `todos` 中的索引，然后使用 `splice` 方法从 `todos` 中删除该待办事项。

```javascript
function toggleAll() {
  const isCompleted = remaining.value === 0;
  todos.value.forEach((todo) => {
    todo.completed = isCompleted;
  });
}
```

这是一个名为 `toggleAll` 的函数，它会将所有待办事项的完成状态设置为相反的状态。首先，它会根据 `remaining` 的值判断是否所有待办事项都已完成，然后遍历 `todos` 中的每个待办事项，将其完成状态设置为相反的状态。

```javascript
function clearCompleted() {
  todos.value = filters.active(todos.value);
}
```

这是一个名为 `clearCompleted` 的函数，它会从 `todos` 中删除所有已完成的待办事项。首先，它会使用 `filters.active` 过滤出所有未完成的待办事项，并将过滤后的列表赋值给 `todos`。

```javascript
function onHashChange() {
  const route = window.location.hash.replace(/#\/?/, '')
  if (filters[route]) {
    visibility.value = route
  } else {
    window.location.hash = ''
    visibility.value = 'all'
  }
}
```

这是一个名为 `onHashChange` 的函数，它会在浏览器 URL 中的哈希值发生变化时触发。具体来说，它会获取当前 URL 中的哈希值，并使用正则表达式将可能存在的 `#` 或 `/#` 前缀删除，然后根据该值更新 `visibility` 的值。如果该值存在于 `filters` 中，则将其设置为当前的筛选条件；否则，将 `window.location.hash` 设置为空字符串，并将 `visibility` 设置为默认值 `'all'`。

这段代码的作用是实现了一个简单的路由功能，根据 URL 中的哈希值来切换不同的筛选条件，从而实现在不同筛选条件下展示不同的待办事项列表。当 URL 中的哈希值不存在于 `filters` 中时，会强制将哈希值设置为空字符串，并将 `visibility` 设置为默认值 `'all'`，以确保应用程序的状态始终保持一致。

最后，这个代码实现了一个简单的待办事项列表应用程序，它使用 Vue 3 中提供的响应式系统实现了数据的双向绑定和自动更新，同时利用本地存储将数据持久化到用户的浏览器中。

```vue
<template>
  <section class="todoapp">
    <header class="header">
      <h1>todos</h1>
      <input
        class="new-todo"
        autofocus
        placeholder="What needs to be done?"
        @keyup.enter="addTodo"
      >
    </header>
    <section class="main" v-show="todos.length">
      <input
        id="toggle-all"
        class="toggle-all"
        type="checkbox"
        :checked="remaining === 0"
        @change="toggleAll"
      >
      <label for="toggle-all">Mark all as complete</label>
      <ul class="todo-list">
        <li
          v-for="todo in filteredTodos"
          class="todo"
          :key="todo.id"
          :class="{ completed: todo.completed, editing: todo === editedTodo }"
        >
          <div class="view">
            <input class="toggle" type="checkbox" v-model="todo.completed">
            <label @dblclick="editTodo(todo)">{{ todo.title }}</label>
            <button class="destroy" @click="removeTodo(todo)"></button>
          </div>
          <input
            v-if="todo === editedTodo"
            class="edit"
            type="text"
            v-model="todo.title"
            @vnode-mounted="({ el }) => el.focus()"
            @blur="doneEdit(todo)"
            @keyup.enter="doneEdit(todo)"
            @keyup.escape="cancelEdit(todo)"
          >
        </li>
      </ul>
    </section>
    <footer class="footer" v-show="todos.length">
      <span class="todo-count">
        <strong>{{ remaining }}</strong>
        <span>{{ remaining === 1 ? ' item' : ' items' }} left</span>
      </span>
      <ul class="filters">
        <li>
          <a href="#/all" :class="{ selected: visibility === 'all' }">All</a>
        </li>
        <li>
          <a href="#/active" :class="{ selected: visibility === 'active' }">Active</a>
        </li>
        <li>
          <a href="#/completed" :class="{ selected: visibility === 'completed' }">Completed</a>
        </li>
      </ul>
      <button class="clear-completed" @click="removeCompleted" v-show="todos.length > remaining">
        Clear completed
      </button>
    </footer>
  </section>
</template>

<style>
@import "https://unpkg.com/todomvc-app-css@2.4.1/index.css";
</style>
```

这是一个使用 Vue 3 编写的待办事项列表的模板代码。下面对其中的关键部分进行分析：

1. `<input class="new-todo">`：这是添加新待办事项的输入框，当用户按下回车键时会触发 `@keyup.enter` 绑定的 `addTodo` 方法。

2. `<input id="toggle-all">` 和 `<label for="toggle-all">`：这是一个全选按钮和对应的标签，用于将所有待办事项的完成状态设置为相反的状态。当用户点击该标签时，会触发 `@change` 绑定的 `toggleAll` 方法。

3. `<li v-for="todo in filteredTodos">`：这是一个待办事项列表项，它使用 `v-for` 指令根据 `filteredTodos` 数组中的元素动态生成。每个列表项都包含一个复选框、一个待办事项标题和一个删除按钮。当用户双击待办事项标题时，会触发 `@dblclick` 绑定的 `editTodo` 方法，将该待办事项的标题设置为可编辑状态。当用户完成编辑时，可以按下回车键或将编辑框失去焦点，触发 `@blur` 或 `@keyup.enter` 绑定的 `doneEdit` 方法，将新的标题保存到待办事项对象中。如果用户想取消编辑，可以按下 ESC 键，触发 `@keyup.escape` 绑定的 `cancelEdit` 方法，将编辑框隐藏并恢复原来的标题。

4. `<span class="todo-count">`：这是一个显示待办事项数量的区域，它会根据 `remaining` 的值动态更新。如果只有一个待办事项未完成，会显示字符串 "1 item left"，否则会显示字符串 "n items left"，其中 n 为未完成的待办事项数量。

5. `<ul class="filters">` 和 `<li>`：这是一个筛选条件的列表，用于切换不同状态下的待办事项。当用户点击某个筛选条件时，会将 `visibility` 的值设置为相应的字符串，从而触发响应式更新，重新计算 `filteredTodos` 数组并动态更新待办事项列表。被选中的筛选条件会使用 `:class` 绑定动态添加 `selected` 类名，以便在界面上高亮显示。

6. `<button class="clear-completed">`：这是一个用于清除已完成待办事项的按钮，当用户点击该按钮时，会触发 `@click` 绑定的 `removeCompleted` 方法，从 `todos` 数组中删除所有已完成的待办事项。

这段代码中还使用了一些 Vue 3 中的高级特性，例如响应式数据绑定、计算属性、监听器等。整个应用程序的状态都被保存在一个名为 `state` 的响应式对象中，这个对象包含了待办事项数组 `todos`、筛选条件 `visibility`、编辑状态 `editedTodo` 等属性，每当这些属性发生变化时，界面会自动更新以反映最新的状态。

## 7 GUIs

7 GUIS（Graphical User Interface for Seven Tasks）是一项用户界面设计任务，旨在帮助软件开发人员和设计师熟悉常见的用户界面设计模式，并提高他们的设计能力。该任务由Jens Dietrich于2020年提出，并在GitHub上发布了相应的文档和示例代码，供开发人员和设计师使用。

7 GUIS任务包括七个常见的用户界面设计任务，分别是：

1. Counter：实现一个计数器应用，用户可以增加、减少和重置计数器的值。
2. Temperature Converter：实现一个温度单位转换应用，用户可以将摄氏度转换为华氏度或反之。
3. Flight Booker：实现一个航班预订应用，用户可以选择出发和到达城市，并选择日期和时间来搜索可用的航班。
4. Timer：实现一个计时器应用，用户可以设置倒计时时间并启动计时器。
5. CRUD：实现一个包含“创建”、“读取”、“更新”和“删除”操作的简单数据库应用。
6. Circle Drawer：实现一个绘图应用，用户可以在画布上绘制圆形。
7. File Browser：实现一个文件浏览器应用，用户可以浏览文件夹、查看文件和文件夹属性，并执行简单的文件操作（如复制、移动和删除）。

通过完成这些任务，开发人员和设计师可以学习如何设计和实现常见的用户界面元素，如按钮、文本框、下拉列表、弹出窗口等，并了解如何将它们组合起来以创建功能强大的应用程序。

### 计数器

```vue
<script setup>
    import {ref} from 'vue'
    
    const count = ref(0)
</script>

<template>
    {{ count }}
    <button @click="count++">count</button>
</template>
```

### 温度转换器

```vue
<script setup>
import { ref } from 'vue'

const c = ref(0)
const f = ref(32)

function setC(e, v = +e.target.value) {
  c.value = v
  f.value = v * (9 / 5) + 32
}

function setF(e, v = +e.target.value) {
  f.value = v
  c.value = (v - 32) * (5 / 9)
}
</script>

<template>
  <input type="number" :value="c" @change="setC"> Celsius =
  <input type="number" :value="f" @change="setF"> Fahrenheit
</template>
```

值得注意的是：

```javascript
function setC(e, v = +e.target.value) {
  c.value = v
  f.value = v * (9 / 5) + 32
}

function setF(e, v = +e.target.value) {
  f.value = v
  c.value = (v - 32) * (5 / 9)
}
```

函数`setC/F`接受两个参数，一个是事件对象`e`，另一个是可选的值`v`，如果没有传入`v`参数，则使用`+e.target.value`将事件对象中的值转换为数字。

> 事件对象中的值通常是字符串类型，例如当用户在一个`<input>`标签中输入数字时，事件对象中对应的值就是一个字符串类型的数字。如果需要将这个字符串类型的数字转换为数字类型，可以使用`+`运算符将其转换为数字类型。

在Vue 3组件中，如果没有传入可选的值`v`，则使用`+e.target.value`将事件对象中的值转换为数字类型。这样做是为了确保在计算摄氏度和华氏度的值时，始终使用数字类型的值进行计算，避免出现类型错误的问题。

### 机票预订

```javascript
<script setup>
import { ref, computed } from 'vue'

const flightType = ref('one-way flight')
const departureDate = ref(dateToString(new Date()))
const returnDate = ref(departureDate.value)

const isReturn = computed(() => flightType.value === 'return flight')

const canBook = computed(
  () =>
    !isReturn.value ||
    stringToDate(returnDate.value) > stringToDate(departureDate.value)
)

function book() {
  alert(
    isReturn.value
      ? `You have booked a return flight leaving on ${departureDate.value} and returning on ${returnDate.value}.`
      : `You have booked a one-way flight leaving on ${departureDate.value}.`
  )
}

function stringToDate(str) {
  const [y, m, d] = str.split('-')
  return new Date(+y, m - 1, +d)
}

function dateToString(date) {
  return (
    date.getFullYear() +
    '-' +
    pad(date.getMonth() + 1) +
    '-' +
    pad(date.getDate())
  )
}

function pad(n, s = String(n)) {
  return s.length < 2 ? `0${s}` : s
}
</script>
```

这是一个使用Vue 3编写的机票预订组件。组件包含一个单程/往返的选择框、一个出发日期输入框和一个返回日期输入框，用户可以在选择框和输入框中选择机票类型和日期，并在预订按钮上点击进行机票预订。

在这个组件中，通过`import { ref, computed } from 'vue'`引入了Vue 3的`ref`和`computed`函数，用于创建响应式数据和计算属性。

组件中定义了三个ref变量`flightType`、`departureDate`和`returnDate`，分别代表机票类型、出发日期和返回日期。其中，`departureDate`的初始值是当前日期，`returnDate`的初始值和`departureDate`相同。

使用`computed`函数定义了两个计算属性：`isReturn`和`canBook`。其中，`isReturn`表示机票类型是否为往返；`canBook`表示是否可以预订机票。在`canBook`中使用了三元运算符，如果是往返机票，则需要判断返回日期是否在出发日期之后，如果是单程机票则直接返回true。

组件中定义了三个函数：`book`、`stringToDate`和`dateToString`。其中，`book`函数用于在预订按钮上点击时弹出预订信息，根据机票类型和日期生成不同的预订信息；`stringToDate`函数用于将字符串类型的日期转换为Date对象；`dateToString`函数用于将Date对象转换为字符串类型的日期。

最后，组件中定义了一个`pad`函数，用于将数字转换为两位数的字符串。该函数接受一个数字参数和一个可选的字符串参数，如果数字小于10，则在其前面添加一个0，否则返回原字符串。

```vue
<template>
  <select v-model="flightType">
    <option value="one-way flight">One-way Flight</option>
    <option value="return flight">Return Flight</option>
  </select>

  <input type="date" v-model="departureDate">
  <input type="date" v-model="returnDate" :disabled="!isReturn">

  <button :disabled="!canBook" @click="book">Book</button>

  <p>{{ canBook ? '' : 'Return date must be after departure date.' }}</p>
</template>

<style>
select,
input,
button {
  display: block;
  margin: 0.5em 0;
  font-size: 15px;
}

input[disabled] {
  color: #999;
}

p {
  color: red;
}
</style>
```

### 计时器

```javascript
<script setup>
import { ref, onUnmounted } from 'vue'

const duration = ref(15 * 1000)
const elapsed = ref(0)

let lastTime = performance.now()
let handle
const update = () => {
  const time = performance.now()
  elapsed.value += Math.min(time - lastTime, duration.value - elapsed.value)
  lastTime = time
  handle = requestAnimationFrame(update)
}

update()
onUnmounted(() => {
  cancelAnimationFrame(handle)
})
</script>
```

通过`import { ref, onUnmounted } from 'vue'`引入了Vue 3的`ref`和`onUnmounted`函数，用于创建响应式数据和在组件销毁时清除计时器。组件中定义了两个ref变量`duration`和`elapsed`，分别代表计时器的总时间和已经流逝的时间。其中，`duration`的初始值为15秒，`elapsed`的初始值为0。

使用`let`关键字定义了两个变量`lastTime`和`handle`，分别代表上一个时间戳和计时器的句柄。在组件中定义了一个`update`函数，用于更新计时器的值。在`update`函数中，根据当前时间和上一个时间戳计算已经流逝的时间，并将其加到`elapsed`变量中。然后，根据`elapsed`和`duration`的时间差，更新计时器的值。最后，使用`requestAnimationFrame`函数递归调用`update`函数，实现计时器的更新。使用`update()`函数启动了计时器，并使用`onUnmounted`函数在组件销毁时清除计时器。

需要注意的是，`performance.now()`函数返回的是相对于导航开始时间的毫秒数，它提供了一个高精度的时间戳，可以用于测量性能和计时。`requestAnimationFrame`函数是浏览器提供的一个API，用于在下一次重绘之前调用指定的函数。通过使用`requestAnimationFrame`函数，可以实现更加精确的计时器。

```vue
<template>
  <label
    >Elapsed Time: <progress :value="elapsed / duration"></progress
  ></label>

  <div>{{ (elapsed / 1000).toFixed(1) }}s</div>

  <div>
    Duration: <input type="range" v-model="duration" min="1" max="30000">
    {{ (duration / 1000).toFixed(1) }}s
  </div>

  <button @click="elapsed = 0">Reset</button>
</template>

<style>
.elapsed-container {
  width: 300px;
}

.elapsed-bar {
  background-color: red;
  height: 10px;
}
</style>
```

这是一个基于Vue 3的简单计时器组件的模板部分。模板中包含一个`<label>`标签，用于显示已经流逝的时间，一个`<div>`标签，用于显示已经流逝的时间，一个`<input>`标签，用于控制计时器的总时间，和一个`<button>`标签，用于重置计时器。

在`<template>`标签中，使用了Vue 3的模板语法，通过`v-model`指令绑定了`elapsed`和`duration`变量，实现了计时器的显示和控制。在`<progress>`标签中，使用了`:value`绑定了计时器进度条的值，即已经流逝的时间占总时间的比例。在`<div>`标签中，使用了插值表达式`{{}}`显示了已经流逝的时间和总时间，其中使用了`toFixed()`函数将时间转换为带有一位小数的字符串。

在`<input>`标签中，使用了`type="range"`设置了控件类型为滑动条，使用了`min`和`max`属性分别设置了最小值和最大值，使用了`v-model`指令绑定了`duration`变量，实现了计时器总时间的控制。在`<div>`标签中，同样使用了插值表达式`{{}}`显示了总时间，使用了`toFixed()`函数将时间转换为带有一位小数的字符串。

在`<button>`标签中，使用了`@click`事件监听器绑定了重置按钮的点击事件，并在点击时将`elapsed`变量重置为0，实现了计时器的重置。

### CRUD

```vue
<script setup>
import { ref, reactive, computed, watch } from 'vue'

const names = reactive(['Emil, Hans', 'Mustermann, Max', 'Tisch, Roman'])
const selected = ref('')
const prefix = ref('')
const first = ref('')
const last = ref('')

const filteredNames = computed(() =>
  names.filter((n) =>
    n.toLowerCase().startsWith(prefix.value.toLowerCase())
  )
)

watch(selected, (name) => {
  [last.value, first.value] = name.split(', ')
})

function create() {
  if (hasValidInput()) {
    const fullName = `${last.value}, ${first.value}`
    if (!names.includes(fullName)) {
      names.push(fullName)
      first.value = last.value = ''
    }
  }
}

function update() {
  if (hasValidInput() && selected.value) {
    const i = names.indexOf(selected.value)
    names[i] = selected.value = `${last.value}, ${first.value}`
  }
}

function del() {
  if (selected.value) {
    const i = names.indexOf(selected.value)
    names.splice(i, 1)
    selected.value = first.value = last.value = ''
  }
}

function hasValidInput() {
  return first.value.trim() && last.value.trim()
}
</script>
```

这是一个使用Vue 3编写的简单CRUD（创建、读取、更新、删除）程序，用于管理一个名字列表。在这个程序中，使用了Vue 3的响应式数据和计算属性，通过对数据的修改和操作，实现对名字列表的增删改查。

在组件中，首先使用了`reactive`函数创建了一个名字列表的响应式数组`names`，并使用`ref`函数创建了四个变量`selected`、`prefix`、`first`和`last`，分别表示当前选中的名字、搜索前缀、名字的姓和名。然后，使用`computed`函数创建了一个计算属性`filteredNames`，用于根据搜索前缀过滤名字列表。

在组件中，使用了`watch`函数监听了`selected`变量的变化，并在变化时更新了`first`和`last`变量的值，以便在修改或删除名字时使用。

组件中定义了三个函数`create()`、`update()`和`del()`，分别用于创建、更新和删除名字。在这些函数中，首先使用`hasValidInput()`函数判断输入是否合法，然后根据情况对名字列表进行增删改操作。其中，`create()`函数用于创建新的名字，`update()`函数用于更新已有的名字，`del()`函数用于删除选中的名字。在这些操作完成后，还需要更新`selected`、`first`和`last`变量的值，以便在界面上反映出修改后的结果。

`hasValidInput()`函数用于检查输入是否合法，即名字的姓和名都不为空。如果输入合法，则返回`true`，否则返回`false`。

这个程序的本质是使用Vue 3的响应式数据和计算属性，实现了对名字列表的增删改查功能。通过使用Vue 3提供的响应式数据和计算属性，可以轻松地实现数据的双向绑定和自动更新，简化了编写复杂交互的前端应用程序的难度。

```javascript
<template>
  <div><input v-model="prefix" placeholder="Filter prefix"></div>

  <select size="5" v-model="selected">
    <option v-for="name in filteredNames" :key="name">{{ name }}</option>
  </select>

  <label>Name: <input v-model="first"></label>
  <label>Surname: <input v-model="last"></label>

  <div class="buttons">
    <button @click="create">Create</button>
    <button @click="update">Update</button>
    <button @click="del">Delete</button>
  </div>
</template>

<style>
* {
  font-size: inherit;
}

input {
  display: block;
  margin-bottom: 10px;
}

select {
  float: left;
  margin: 0 1em 1em 0;
  width: 14em;
}

.buttons {
  clear: both;
}

button + button {
  margin-left: 5px;
}
</style>
```

在这个模板中，使用了Vue 3的模板语法和指令，实现了对名字列表的搜索、选择、修改和删除功能。

在模板中，首先使用了一个`<div>`标签和一个输入框，用于输入搜索前缀。在输入框中使用了`v-model`指令，将输入框的值绑定到`prefix`变量上，实现了搜索前缀的双向绑定。

接下来使用了一个`<select>`标签，用于显示名字列表。使用了`v-model`指令将当前选中的名字绑定到`selected`变量上，实现了名字的选择。在`<option>`标签中使用了`v-for`指令，遍历`filteredNames`计算属性中过滤后的名字列表，并使用`:key`绑定了每个选项的唯一标识。

在模板中使用了两个`<label>`标签和两个输入框，分别用于输入名字的姓和名。在输入框中使用了`v-model`指令，将输入框的值绑定到`first`和`last`变量上，实现了名字的双向绑定。

最后，在模板中使用了三个按钮，分别用于创建、更新和删除名字。在`<button>`标签中使用了`@click`指令，绑定了每个按钮的点击事件，实现了对应操作的触发。

### 画圆

```vue
<script setup>
import { ref, shallowReactive, toRaw } from 'vue'

const history = shallowReactive([[]])
const index = ref(0)
const circles = ref([])
const selected = ref()
const adjusting = ref(false)

function onClick({ clientX: x, clientY: y }) {
  if (adjusting.value) {
    adjusting.value = false
    selected.value = null
    push()
    return
  }

  selected.value = [...circles.value].reverse().find(({ cx, cy, r }) => {
    const dx = cx - x
    const dy = cy - y
    return Math.sqrt(dx * dx + dy * dy) <= r
  })

  if (!selected.value) {
    circles.value.push({
      cx: x,
      cy: y,
      r: 50
    })
    push()
  }
}

function adjust(circle) {
  selected.value = circle
  adjusting.value = true
}

function push() {
  history.length = ++index.value
  history.push(clone(circles.value))
  console.log(toRaw(history))
}

function undo() {
  circles.value = clone(history[--index.value])
}

function redo() {
  circles.value = clone(history[++index.value])
}

function clone(circles) {
  return circles.map((c) => ({ ...c }))
}
</script>
```

这段代码使用Vue 3的`<script setup>`语法，定义了一个包含多个函数和变量的模块。这些函数和变量用于实现一个简单的画圆程序，可以通过鼠标点击和拖动来绘制和调整圆形的位置和大小，并支持撤销和重做操作。

下面是对每行代码的分析和解释：

```javascript
import { ref, shallowReactive, toRaw } from 'vue'
```

这一行代码使用ES6的`import`语法导入了Vue 3中的三个函数：`ref`、`shallowReactive`和`toRaw`。这些函数用于创建响应式数据和深度复制对象等功能。

```javascript
const history = shallowReactive([[]])
```

这一行代码定义了一个响应式变量`history`，它是一个数组，用于保存绘画历史记录。初始时，`history`只包含一个空数组。

```javascript
const index = ref(0)
```

这一行代码定义了一个响应式变量`index`，它是一个数字，用于表示当前历史记录的索引。初始时，`index`的值为0。

```javascript
const circles = ref([])
```

这一行代码定义了一个响应式变量`circles`，它是一个数组，用于保存所有的圆形数据。初始时，`circles`为一个空数组。

```javascript
const selected = ref()
```

这一行代码定义了一个响应式变量`selected`，它用于保存当前选中的圆形数据。初始时，`selected`为`undefined`。

```javascript
const adjusting = ref(false)
```

这一行代码定义了一个响应式变量`adjusting`，它用于表示当前是否处于调整圆形状态。初始时，`adjusting`的值为`false`。

```javascript
function onClick({ clientX: x, clientY: y }) {
```

这一行代码定义了一个名为`onClick`的函数，它接收一个鼠标事件对象，并从中提取出`clientX`和`clientY`属性，分别表示鼠标点击的横纵坐标。

```javascript
if (adjusting.value) {
  adjusting.value = false
  selected.value = null
  push()
  return
}
```

这一段代码判断当前是否处于调整圆形状态，如果是，则将`adjusting`和`selected`变量重置为初始状态，并保存历史记录。

```javascript
selected.value = [...circles.value].reverse().find(({ cx, cy, r }) => {
  const dx = cx - x
  const dy = cy - y
  return Math.sqrt(dx * dx + dy * dy) <= r
})
```

这一行代码使用ES6的扩展运算符和`reverse`方法，将`circles`数组复制一份，并反转顺序。然后使用`find`方法遍历数组，查找包含鼠标点击点的圆形。如果找到了圆形，则将其赋值给`selected`变量。

```javascript
if (!selected.value) {
  circles.value.push({
    cx: x,
    cy: y,
    r: 50
  })
  push()
}
```

这一段代码判断当前是否选中了圆形，如果没有，则在`circles`数组中添加一个新的圆形数据，并保存历史记录。

```javascript
function adjust(circle) {
  selected.value = circle
  adjusting.value = true
}
```

这一行代码定义了一个名为`adjust`的函数，它接收一个圆形数据作为参数，并将其赋值给`selected`变量，并将`adjusting`变量设置为`true`，表示进入调整圆形状态。

```javascript
function push() {
  history.length = ++index.value
  history.push(clone(circles.value))
  console.log(toRaw(history))
}
```

这一行代码定义了一个名为`push`的函数，它用于保存历史记录。具体来说，它将`history`数组的长度增加1，将当前的`circles`数组复制一份，并使用`push`方法添加到`history`数组中。最后，它使用`toRaw`函数打印出`history`数组的原始值，用于调试和测试。

```javascript
function undo() {
  circles.value = clone(history[--index.value])
}
```

这一行代码定义了一个名为`undo`的函数，它用于执行撤销操作。具体来说，它将`index`变量减1，然后将`circles`数组重新赋值为历史记录中上一个状态的值。

```javascript
function redo() {
  circles.value = clone(history[++index.value])
}
```

这一行代码定义了一个名为`redo`的函数，它用于执行重做操作。具体来说，它将`index`变量加1，然后将`circles`数组重新赋值为历史记录中下一个状态的值。

```javascript
function clone(circles) {
  return circles.map((c) => ({ ...c }))
}
```

这一行代码定义了一个名为`clone`的函数，它用于深度复制一个圆形数组。具体来说，它使用`map`方法遍历数组，将每个圆形对象复制一份，并返回一个新的数组。

```vue
<template>
  <svg @click="onClick">
    <foreignObject x="0" y="40%" width="100%" height="200">
      <p class="tip">
        Click on the canvas to draw a circle. Click on a circle to select it.
        Right-click on the canvas to adjust the radius of the selected circle.
      </p>
    </foreignObject>
    <circle
      v-for="circle in circles"
      :key="circle"
      :cx="circle.cx"
      :cy="circle.cy"
      :r="circle.r"
      :fill="circle === selected ? '#ccc' : '#fff'"
      @click="selected = circle"
      @contextmenu.prevent="adjust(circle)"
    ></circle>
  </svg>

  <div class="controls">
    <button @click="undo" :disabled="index <= 0">Undo</button>
    <button @click="redo" :disabled="index >= history.length - 1">Redo</button>
  </div>

  <div class="dialog" v-if="adjusting" @click.stop>
    <p>Adjust radius of circle at ({{ selected.cx }}, {{ selected.cy }})</p>
    <input type="range" v-model="selected.r" min="1" max="300">
  </div>
</template>
```

这段代码使用Vue 3的模板语法，定义了一个SVG画布和几个控件，用于实现一个简单的绘画程序。下面是对每个元素和属性的分析和解释：

```html
<svg @click="onClick">
```

这一行代码定义了一个SVG画布，并绑定了一个`click`事件处理函数`onClick`。当用户在画布上点击时，就会触发该函数。

```html
<foreignObject x="0" y="40%" width="100%" height="200">
  <p class="tip">
    Click on the canvas to draw a circle. Click on a circle to select it.
    Right-click on the canvas to adjust the radius of the selected circle.
  </p>
</foreignObject>
```

这一段代码定义了一个`foreignObject`元素，它用于在SVG画布上添加一个HTML元素。具体来说，它添加了一个包含提示信息的段落元素，提示用户如何使用绘画程序。

```html
<circle
  v-for="circle in circles"
  :key="circle"
  :cx="circle.cx"
  :cy="circle.cy"
  :r="circle.r"
  :fill="circle === selected ? '#ccc' : '#fff'"
  @click="selected = circle"
  @contextmenu.prevent="adjust(circle)"
></circle>
```

这一段代码定义了一个`circle`元素，并使用`v-for`指令遍历`circles`数组，为每个圆形对象生成一个`circle`元素。具体来说，它为每个圆形对象设置`cx`、`cy`、`r`和`fill`属性，用于指定圆心坐标、半径和填充颜色。它还使用条件表达式`:fill="circle === selected ? '#ccc' : '#fff'"`来根据圆形是否被选中来设置填充颜色。当圆形被选中时，填充颜色为灰色；否则，填充颜色为白色。它还为每个圆形对象绑定了一个`click`事件处理函数`selected = circle`，用于选中该圆形。当用户点击一个圆形时，就会触发该函数，并将该圆形对象赋值给`selected`变量。它还为每个圆形对象绑定了一个`@contextmenu.prevent`事件处理函数`adjust(circle)`，用于在用户右键点击该圆形时调整其半径。

```html
<div class="controls">
  <button @click="undo" :disabled="index <= 0">Undo</button>
  <button @click="redo" :disabled="index >= history.length - 1">Redo</button>
</div>
```

这一段代码定义了两个按钮，用于执行撤销和重做操作。具体来说，它为每个按钮绑定了一个`click`事件处理函数`undo`和`redo`，分别用于执行撤销和重做操作。它还使用`:disabled`属性来禁用按钮，当`index`变量小于等于0时，禁用撤销按钮；当`index`变量大于等于`history.length - 1`时，禁用重做按钮。

```html
<div class="dialog" v-if="adjusting" @click.stop>
  <p>Adjust radius of circle at ({{ selected.cx }}, {{ selected.cy }})</p>
  <input type="range" v-model="selected.r" min="1" max="300">
</div>
```

这一段代码定义了一个对话框，用于在调整圆形半径时显示。具体来说，它使用`v-if`指令根据`adjusting`变量的值来控制对话框的显示和隐藏。当`adjusting`为`true`时，显示对话框；否则，隐藏对话框。它还使用`@click.stop`事件修饰符来阻止点击事件冒泡，以避免在对话框外单击时关闭对话框。它在对话框中展示了一个段落元素，用于显示当前要调整半径的圆形对象的坐标，以及一个滑动条元素，用于调整圆形的半径。它使用`v-model`指令将`selected.r`绑定到滑动条元素上，以实现双向绑定。

### 单元格

```vue
import { reactive } from 'vue'

const COLS = 5
const ROWS = 20
export const cells = reactive(
  Array.from(Array(COLS).keys()).map((i) =>
    Array.from(Array(ROWS).keys()).map((i) => '')
  )
)

export function evalCell(exp) {
  if (!exp.startsWith('=')) {
    return exp
  }

  // = A1 + B2 ---> get(0,1) + get(1,2)
  exp = exp
    .slice(1)
    .replace(
      /\b([A-Z])(\d{1,2})\b/g,
      (_, c, r) => `get(${c.charCodeAt(0) - 65},${r})`
    )

  try {
    return new Function('get', `return ${exp}`)(getCellValue)
  } catch (e) {
    return `#ERROR ${e}`
  }
}

function getCellValue(c, r) {
  const val = evalCell(cells[c][r])
  const num = Number(val)
  return Number.isFinite(num) ? num : val
}
```

<div align="center">store.js</div>

这段代码定义了一个名为`cells`的响应式数据对象和一个名为`evalCell`的函数，用于计算单元格表达式的值。在代码最后，还定义了一个名为`getCellValue`的函数，用于获取指定单元格的值。

其中，`cells`响应式数据对象是一个二维数组，用于存储单元格的值。它使用`reactive`函数创建，可以在Vue 3的组件中使用。这个二维数组的大小是`COLS`列和`ROWS`行，每个单元格的初始值为空字符串`''`。

`evalCell`函数用于计算单元格表达式的值。它接受一个表示单元格表达式的字符串参数`exp`，并返回计算得到的值。如果`exp`不是以等号`=`开头的普通字符串，则直接返回该字符串；否则，将其视为一个表达式进行计算。

`evalCell`函数使用正则表达式`\b([A-Z])(\d{1,2})\b/g`来搜索表达式中的单元格引用，例如`A1`、`B2`等。如果找到了单元格引用，则将其替换为调用`get`函数获取单元格的值，例如`get(0,1)`、`get(1,2)`等。这个过程使用了正则表达式的替换功能和箭头函数的特性。

`evalCell`函数使用`try...catch`语句块来捕获表达式计算过程中的错误，并返回带有错误信息的字符串`#ERROR ${e}`。如果表达式计算成功，则返回计算得到的值。

`getCellValue`函数用于获取指定单元格的值。它接受两个参数，分别是单元格的列索引`c`和行索引`r`。它首先调用`evalCell`函数计算单元格的值，然后将其转换为数字类型。如果转换成功，则返回转换后的数字；否则，返回原始的值。

```vue
<script setup>
import { ref } from 'vue'
import { cells, evalCell } from './store.js'

const props = defineProps({
  c: Number,
  r: Number
})

const editing = ref(false)

function update(e) {
  editing.value = false
  cells[props.c][props.r] = e.target.value.trim()
}
</script>
```

<div align="center">Cell.vue</div>

首先，使用`import`语句导入了`ref`、`cells`和`evalCell`三个变量，其中`ref`是Vue 3提供的响应式数据工具函数，`cells`和`evalCell`是之前定义的响应式数据对象和计算单元格表达式的函数。

接着，使用`defineProps`函数定义了两个组件属性`c`和`r`，分别表示当前单元格的列索引和行索引，类型均为`Number`。

然后，定义了一个名为`editing`的响应式引用变量，用于表示当前单元格是否处于编辑状态，初始值为`false`。当单元格被点击时，会将`editing`的值设置为`true`，表示进入编辑状态。

最后，定义了一个名为`update`的函数，用于更新单元格的值。它接受一个事件参数`e`，并将单元格的值设置为事件目标元素的`value`属性的去除空格后的值。同时，将`editing`的值设置为`false`，表示退出编辑状态。

这段代码的作用是实现单元格的编辑功能。当单元格被点击时，会进入编辑状态，并显示一个输入框，用于修改单元格的值。当输入框失去焦点或按下回车键时，会触发`update`函数，将新的单元格值保存到`cells`响应式数据对象中，并退出编辑状态。这样，用户就可以方便地编辑单元格的值，而且修改后的值会自动更新到UI界面上。

```vue
<template>
  <div class="cell" :title="cells[c][r]" @click="editing = true">
    <input
      v-if="editing"
      :value="cells[c][r]"
      @change="update"
      @blur="update"
      @vnode-mounted="({ el }) => el.focus()"
    >
    <span v-else>{{ evalCell(cells[c][r]) }}</span>
  </div>
</template>

<style>
.cell, .cell input {
  height: 1.5em;
  line-height: 1.5;
  font-size: 15px;
}

.cell span {
  padding: 0 6px;
}

.cell input {
  width: 100%;
  box-sizing: border-box;
}
</style>
```

<div align='center'>Cell.vue</div>

首先，在`<div>`元素上绑定了`class`属性，表示该元素的样式类名为`cell`。同时，使用`:title`指令将该元素的`title`属性绑定到`cells[c][r]`，用于在鼠标悬停时显示单元格的值。

接着，在`<div>`元素上绑定了`@click`事件监听器，表示当该元素被点击时，会触发`editing = true`语句，将`editing`的值设置为`true`，表示进入编辑状态。

然后，使用`v-if`指令判断`editing`的值是否为`true`。如果是，表示当前单元格处于编辑状态，需要显示一个输入框，用于修改单元格的值。此时，使用`<input>`元素来渲染输入框，并使用`:value`指令将其值绑定到`cells[c][r]`，表示当前输入框中的值与该单元格的值同步。同时，使用`@change`和`@blur`事件监听器来监视输入框的值变化和失去焦点事件，并触发`update`函数来保存修改后的单元格值。此外，使用`@vnode-mounted`指令在输入框元素创建完成后，立即将其聚焦，方便用户进行编辑。

最后，使用`v-else`指令表示如果`editing`的值为`false`，表示当前单元格不处于编辑状态，需要显示该单元格的值。此时，使用`<span>`元素来渲染该单元格的值，使用插值语法`{{ evalCell(cells[c][r]) }}`将其值绑定到`evalCell(cells[c][r])`的计算结果上，表示该单元格的值已经经过计算单元格表达式的函数处理后得到。

```vue
<script setup>
import Cell from './Cell.vue'
import { cells } from './store.js'

const cols = cells.map((_, i) => String.fromCharCode(65 + i))
</script>

<template>
  <table>
    <thead>
      <tr>
        <th></th>
        <th v-for="c in cols" :key="c">{{ c }}</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="i in cells[0].length" :key="i">
        <th>{{ i - 1 }}</th>
        <td v-for="(c, j) in cols" :key="c">
          <Cell :r="i - 1" :c="j"></Cell>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<style>
body {
  margin: 0;
}

table {
  border-collapse: collapse;
  table-layout: fixed;
  width: 100%;
}

th {
  background-color: #eee;
}

tr:first-of-type th {
  width: 100px;
}

tr:first-of-type th:first-of-type {
  width: 25px;
}

td {
  border: 1px solid #ccc;
  height: 1.5em;
  overflow: hidden;
}
</style>
```

<div align='center'>App.vue</div>

首先，在`<script setup>`部分，使用`import`语句导入了`Cell`组件和`cells`响应式数据对象，其中`Cell`组件用于渲染单个单元格的UI界面，`cells`对象用于存储所有单元格的值。

接着，定义了一个名为`cols`的常量，使用`map`方法遍历`cells`数组，生成一个由字母组成的数组，用于表示表格的列头，每个字母都是从'A'开始，依次递增。

然后，在`<template>`部分，使用`<table>`、`<thead>`、`<tbody>`、`<tr>`、`<th>`和`<td>`等元素来渲染表格的UI界面。首先，使用`<thead>`元素渲染表格的表头部分，其中使用`<th>`元素渲染第一列的表头，留空用于占位，而使用`v-for`指令渲染其他列的表头，将`cols`数组中的每个字母依次渲染出来。

接着，使用`<tbody>`元素渲染表格的主体部分，其中使用`<tr>`元素渲染每一行的数据行，使用`v-for`指令遍历`cells[0].length`，将每一行的行号依次渲染出来，并使用`<th>`元素渲染该行的第一列，显示该行的行号。而使用`<td>`元素渲染其他列的单元格，使用`v-for`指令遍历`cols`数组，将每个字母依次渲染出来，并使用`Cell`组件渲染该单元格的UI界面，将该单元格的行号和列号传递给`Cell`组件作为属性，方便组件内部处理。

最后，在`<style>`部分，定义了一些CSS样式，用于美化表格的UI界面。其中，设置了表格的边框折叠、布局方式、宽度等属性，设置了表头和数据行的背景颜色，设置了单元格的边框、高度和溢出隐藏等属性。