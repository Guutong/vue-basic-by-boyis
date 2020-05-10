# Basic Vue js

## Install
  > for development
  ```
  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  ```
  > for production
  ```
  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  ```

## Basic Rendering
  ```
    <body>
      <div id="app">
        {{message}}
      </div>
    </body>
  ```
  ```
    <script>
      const app = new Vue({
        el: "#app",
        data: {
          message: "Hello Vue!"
        }
      })
    </script>
  ```

## Interpolations
  ```
    <div id="app">
      <span>Message: {{message}}</span>
    </div>
  ```

  ```
    <script>
    const app = new Vue({
      el: "#app",
      data: {
        message: "Hello Vue!"
      }
    })
  </script>
  ```

  > add v-once : one-time interpolations that do not update
  ```
    <div id="app">
      <span v-once>Message: {{message}}</span>
    </div>
  ```
### JavaScript Expressions (Interpolations)
  ```
    <div id="app">
      {{number + 1}}
      <br/>
      {{ok ? 'YES' : 'NO'}}
      <br/>
      {{ message.split('').reverse().join('')}}
      <br/>
      {{Math.random()}}
      <br/>
      {{new Date()}}
    </div>
  ```

  ```
    const app = new Vue({
      el: "#app",
      data: {
        number: 0,
        ok: true,
        message: "Hello Vue!"
      }
    })
  ```

  > change interpolations
  ```
    <div id="app">
      <% number + 1 }}
    </div>
  ```
  ```
    const app = new Vue({
      el: "#app",
      data: {
        number: 0,
      },
      delimiters: ["<%", "}}"]
    })
  ```

## Directive
  > v-if
  ```
   <div id="app">
      <p v-if="seen">Now you see me</p>
   </div>
  ```
  ```
    const app = new Vue({
      el: "#app",
      data: {
        seen: true,
      },
    })
  ```
  > if-else
  ```
    <div id="app">
      <p v-if="seen">Now you see me</p>
      <p v-else>Now you can not see me</p>
    </div>
  ```
  ```
    const app = new Vue({
      el: "#app",
      data: {
        seen: true,
      },
    })
  ```
  > v-if-elseif
  ```
    <div id="app">
      <p v-if="type === 'A'">Now you see me</p>
      <p v-else-if="type === 'B'">Now you can not see me</p>
    </div>
  ```
  ```
    const app = new Vue({
      el: "#app",
      data: {
        type: 'A',
      },
    })
  ```
  > v-if-else-if-else
  ```
    <div id="app">
      <p v-if="type === 'A'">Now you see me</p>
      <p v-else-if="type === 'B'">Now you can not see me</p>
      <p v-else>Not A/B</p>
    </div>
  ```
  > v-show (use css display (if false use display:none))
   ```
   <div id="app">
      <p v-show="seen">Now you see me</p>
    </div>
  ```
  ```
    const app = new Vue({
      el: "#app",
      data: {
        seen: true,
      },
    })
  ```
  > v-for
  ```
    <div id="app">
      <p v-for="l in list">{{l}}</p>
    </div>
  ```
  ```
    const app = new Vue({
      el: "#app",
      data: {
        list: ["1", "2", "3", "4"],
      },
    })
  ```
  > v-for (with index)
  ```
    <div id="app">
      <p v-for="(value, index) in list">{{index}}: {{value}}</p>
    </div>
  ```
  > v-for (Object)
  ```
    <div id="app">
      <p v-for="value in object">{{value}}</p>
    </div>
  ```
  ```
    const app = new Vue({
      el: "#app",
      data: {
        object: {
          hello1: 'Hello 1',
          hello2: 'Hello 2',
          hello3: 'Hello 3',
        }
      },
    })
  ```
  > v-for (Object)(with key)
  ```
    <div id="app">
      <p v-for="(value, key) in object">{{key}}: {{value}}</p>
    </div>
  ```
  > v-for (Object)(with key and index)
  ```
    <div id="app">
      <p v-for="(value, key, index) in object">{{index}} -> {{key}}: {{value}}</p>
    </div>
  ```
  > v-bind (Arguments)
  ```
    <div id="app">
      <p v-bind:title="title">Hello binding</p>
    </div>
  ```
  ```
    const app = new Vue({
      el: "#app",
      data: {
        title: 'Hello title'
      },
    })
  ```
  > v-bind (Dynamic component)
  ```
    const app = new Vue({
      el: "#app",
      data: {
        attrname: "title",
        title: 'Hello title'
      },
    })
  ```
  ```
    <div id="app">
      <p v-bind:[attrname]="title">Hello binding</p>
    </div>
  ```
  > v-on
  ```
    <div id="app">
      <p>Counter: {{counter}} times.</p>
      <button v-on:click="counter += 1">Add 1</button>
    </div>
  ```
  ```
    const app = new Vue({
      el: "#app",
      data: {
        counter: 0
      },
    })
  ```

### Shorthands
  > v-bind
  ```
    <div id="app">
      <p v-bind:title="title">Hello Shorthand 1</p>
      <p :title="title">Hello Shorthand 2</p>
      <p :[attrname]="title">Hello Shorthand 3</p>
    </div>
  ```
  ```
    const app = new Vue({
      el: "#app",
      data: {
        attrname: "title",
        title: "This is title"
      },
    })
  ```
  > v-on
  ```
    <div id="app">
      <p>Counter: {{counter}}</p>
      <button v-on:click="counter += 1">Add 1</button>
      <button @click="counter += 1">Add 1</button>
      <button @[attrname]="counter += 1">Add 1</button>
    </div>
  ```
  ```
    const app = new Vue({
      el: "#app",
      data: {
        attrname: "click",
        counter: 0
      },
    })
  ```

## Methods
```
  <div id="app">
    <p>{{getReverse()}}</p>
  </div>
```
```
  const app = new Vue({
    el: "#app",
    data: {
      message: 'Hello World'
    },
    methods: {
      getReverse: function () {
        return this.message.split('').reverse().join('');
      }
    },
  })
```
```
  <div id="app">
    <p v-bind:title="getReverse()">{{message}}</p>
  </div>
```
```
  const app = new Vue({
    el: "#app",
    data: {
      message: 'Hello World'
    },
    methods: {
      getReverse: function () {
        return this.message.split('').reverse().join('');
      }
    },
  })
```

## Event Handling
```
  <div id="app">
    <p>Counter: {{counter}} times.</p>
    <button v-on:click="addCounter">Add 1</button>
  </div>
```
```
const app = new Vue({
    el: "#app",
    data: {
      counter: 0
    },
    methods: {
      addCounter: function() {
        this.counter += 1;
      }
    },
  })
```
> with event
```
  const app = new Vue({
      el: "#app",
      data: {
        counter: 0
      },
      methods: {
        addCounter: function(event) {
          this.counter += 1;
          console.log(event.target.tagName);
        }
      },
    })
```
> specific param
```
<div id="app">
  <p>Counter: {{counter}} times.</p>
  <button v-on:click="addCounter(counter)">Add 1</button>
</div>
```
```
  const app = new Vue({
    el: "#app",
    data: {
      counter: 0
    },
    methods: {
      addCounter: function(counter) {
        this.counter = counter + 1;
      }
    },
  })
```
> param event
```
  <div id="app">
    <p>Counter: {{counter}} times.</p>
    <button v-on:click="addCounter(counter, $event)">Add 1</button>
  </div>
```
```
  const app = new Vue({
    el: "#app",
    data: {
      counter: 0
    },
    methods: {
      addCounter: function(counter, event) {
        this.counter = counter + 1;
        console.log(event.target.tagName);
      }
    },
  })
```

### Modifiers
```
<div id="app">
  <p>Counter: {{counter}} times.</p>
  <button v-on:click.once="addCounter(counter, $event)">Add 1</button>
</div>
```
```
const app = new Vue({
  el: "#app",
  data: {
    counter: 0
  },
  methods: {
    addCounter: function(counter, event) {
      this.counter = counter + 1;
      console.log(event.target.tagName);
    }
  },
})
```
### KeyModifiers
```
<div id="app">
  <!-- <input v-model="message" v-on:keyup.enter="onEnter"> -->
  <!-- <input v-model="message" v-on:keyup.space="onEnter"> -->
  <!-- <input v-model="message" v-on:keydown.meta.67="onEnter"> -->
  <!-- <input v-model="message" v-on:keyup.enter="onEnter"> -->
</div>
```
```
const app = new Vue({
  el: "#app",
  data: {
    message: 'hello'
  },
  methods: {
    onEnter: function() {
      console.log(this.message)
    }
  },
})
```

## Form Input Binding
  > basic v-model
  ```
    <div id="app">
      <input v-model="message">
      <p>Message is : {{message}}</p>
    </div>
  ```
  > input checkbox
  ```
    <div id="app">
      <input v-model="message">
      <p>Message is : {{message}}</p>
      <input type="checkbox" id="checkbox" v-model="checked">
      <label for="checkbox">{{ checked }}</label>
    </div>
  ```
  ```
  const app = new Vue({
    el: "#app",
    data: {
      message: "",
      checked: false,
    },
  })
```

### Value binding
  ```
  <div id="app">
    <p>Radio: {{type}}</p>
    <input type="radio" v-model="type" v-bind:value="a">A
    <input type="radio" v-model="type" value="B">B
    <p>Checkbox: {{check}}</p>
    <input type="checkbox" v-model="check" true-value="yes" false-value="no">
    <p>Select {{selected}}</p>
    <select v-model="selected">
      <option v-bind:value="{ number: 1 }">1</option>
      <option v-bind:value="{ number: 2 }">2</option>
    </select>
  </div>
```
  ```
    const app = new Vue({
        el: "#app",
        data: {
          a: "A",
          type: '',
          check: '',
          selected: 0,
        },
      })
  ```

### Modifiers
  > .lazy

    <div id="app">
      <p>Title : {{title}}</p>
      <input type="text" v-model.lazy="title">
    </div>

    const app = new Vue({
      el: "#app",
      data: {
        title: "",
      },
    })

  > .trim

    <div id="app">
      <p>Title : {{title}}</p>
      <input type="text" v-model.trim="title">
    </div>

    const app = new Vue({
      el: "#app",
      data: {
        title: "",
      },
    })

  > .number

      <div id="app">
        <p>Age : {{age}}</p>
        <input type="number" v-model.number="age">
      </div>

      const app = new Vue({
        el: "#app",
        data: {
          age: 0,
        },
      })


## Watchers
  ```
    <div id="app">
      <p>Search : {{search}}</p>
      <input type="text" v-model="search">
    </div>
  ```
  ```
    const app = new Vue({
      el: "#app",
      data: {
        search: "",
        timeout: null,
      },
      watch: {
        search: function () {
          clearTimeout(this.timeout);
          const _this = this;
          this.timeout = setTimeout(function () {
            _this.querySearch();
          }, 500);
        }
      },
      methods: {
        querySearch: function () {
          console.log(this.search);
        }
      },
    })
  ```

## Computed
  ```
    <div id="app">
      {{ message.split('').reverse().join('') }}
    </div>
  ```

  ```
    <div id="app">
      <p>Message : {{message}}</p>
      <p>Reverse Message : {{reversedMessage}}</p>
    </div>
  ```
  ```
    const app = new Vue({
      el: "#app",
      data: {
        message: 'Hello World',
      },
      computed: {
        reversedMessage: function() {
          return this.message.split('').reverse().join('')
        }
      },
    })
  ```

  ### Computed Setter
  > Computed default is getter

    <div id="app">
      <p>Full name: {{fullName}}</p>
      first-name: <input v-model="firstName">
      last-name: <input v-model="lastName">
    </div>

    const app = new Vue({
      el: "#app",
      data: {
        firstName: '',
        lastName: '',
      },
      computed: {
        fullName: {
          get: function() {
            return [this.firstName, this.lastName].join(' ');
          },
          set: function(value) {
            const [firstName, lastName] = value.split(' ');
            this.firstName = firstName;
            this.lastName = lastName;
          }
        }
      },
    })

  ### Computed Caching vs Methods
  ```
    <div id="app">
      <input v-model="message">
      <p>Computed: {{comp}}</p>
      <p>Method: {{method()}}</p>
    </div>
  ```
  ```
  const app = new Vue({
    el: "#app",
    data: {
      message: '',
    },
    computed: {
      comp: function() {
        return new Date();
      }
    },
    methods: {
      method: function() {
        return new Date();
      }
    },
  })
  ```

  ### Computed vs Watched Property

## LifeCycle
- ก่อน create vue instance
 	  - beforeCreate
	  - created

      ```
      <div id="app">
        <p>Message: {{message}}</p>
        <input v-model="message" ref="input">
      </div>
      ```
      ```
        const app = new Vue({
            el: "#app",
            data: {
              title: "Hello Title",
              helloCreate: "Hello create",
              message: 'Hello World!',
            },
            beforeCreate() {
              console.log('before create: ', this.message);
              // console.log(document.getElementsByTagName('p')[0].innerHTML = "{{title}}")
            },
            created() {
              console.log('created: ', this.message);
              // console.log(document.getElementsByTagName('p')[0].innerHTML = "{{helloCreate}}")
            },
          })
      ```

  - ก่อน DOM สร้าง
	  - beforeMount

  - หลัง DOM สร้าง
	  - mounted

  - ก่อน DOM re-renders
	  - beforeUpdate

  - หลัง DOM re-renders
	  - updated

    ```
      beforeUpdate() {
        console.log('before updated: ', this.$refs.input.value)
        this.message = this.message.toUpperCase();
      },
      updated() {
        console.log('updated: ', this.$refs.input.value)
      },
    ```

  - ก่อน Vue instance ถูกทำลาย
	  - beforeDestroy

  - หลัง Vue instance ถูกทำลาย
	  - destroyed

    ```
     <button @click="destroy()">Destroy</button>
    ```

    ```
    beforeDestroy() {
      console.log('before destroy', this.$refs.input);
    },
    destroyed() {
      console.log('destroyed', this.$refs.input);
    },
    ```

## Basic Components
  > basic component

  ```
    <div id="app">
      <button-counter></button-counter>
    </div>
  ```
  ```
    Vue.component('box-title', {
      data: function() {
        return {
          count: 0,
        }
      },
      template: `<button @click="count++">Count: {{count}}</button>`
    });
    const app = new Vue({
      el: "#app",
    })
  ```
  > Props
  ```
    <div id="app">
      <box-message message="This is message"></box-message>
    </div>
  ```
  ```
    Vue.component('box-message', {
      props: ['message'],
      template: `<h1>{{message}}</h1>`
    });
    const app = new Vue({
      el: "#app",
    })
  ```
  > With data
  ```
    <div id="app">
      <box-message  v-bind:message="message"></box-message>
    </div>
  ```
  ```
    Vue.component('box-message', {
      props: ['message'],
      template: `<h1>{{message}}</h1>`
    });
    const app = new Vue({
      el: "#app",
      data: {
        message: "This is message"
      }
    })
  ```

  ### Emitting
  ```
    <div id="app">
      <p>Count: {{count}}</p>
      <button v-on:click="count += 1">Button</button>
      <custom-button v-on:click="count += 1"></custom-button>
    </div>
  ```
  ```
    Vue.component('custom-button', {
      template: `<button @click="$emit('click')">Button</button>`
    });
    const app = new Vue({
      el: "#app",
      data: {
        count: 0,
      }
    })
  ```
  > with param
  ```
      <div id="app">
        <p>Count: {{count}}</p>
        <button v-on:click="count += 1">Button</button>
        <custom-button v-on:click="count += $event"></custom-button>
      </div>
  ```
  ```
  Vue.component('custom-button', {
    data: function() {
      return {
        count: 0
      }
    },
    template: `<button @click="$emit('click', ++count)">Button</button>`
  });
  ```
  > call on method
  ```
    Vue.component('custom-button', {
      data: function() {
        return {
          count: 0
        }
      },
      methods: {
        onClick: function() {
          this.$emit('click', ++this.count)
        }
      },
      template: `<button @click="onClick">Button</button>`
    });
  ```
  > call on method on main component
  ```
    <div id="app">
      <p>Count: {{count}}</p>
      <button v-on:click="onClick(1)">Button</button>
      <custom-button v-on:click="onClick"></custom-button>
    </div>
  ```
  ```
    Vue.component('custom-button', {
      data: function() {
        return {
          count: 0
        }
      },
      methods: {
        onClick: function() {
          this.$emit('click', ++this.count)
        }
      },
      template: `<button @click="onClick">Button</button>`
    });
    const app = new Vue({
      el: "#app",
      data: {
        count: 0,
      },
      methods: {
        onClick: function(value) {
          this.count += value;
        }
      }
    })
  ```
  > with naming
  ```
    <div id="app">
      <p>Count: {{count}}</p>
      <button v-on:click="onClick(1)">Button</button>
      <custom-button v-on:target-name="onClick"></custom-button>
    </div>
  ```
  ```
    Vue.component('custom-button', {
      data: function() {
        return {
          count: 0
        }
      },
      methods: {
        onClick: function() {
          this.$emit('target-name', ++this.count)
        }
      },
      template: `<button @click="onClick">Button</button>`
    });
  ```

## Slot
```
  <div id="app">
    <box-message>
      <p>Hello World!</p>
    </box-message>
  </div>
```
```
  Vue.component('box-message', {
    template: `<div>
      <slot></slot>
    </div>`
  });
```
> default content
```
  <div id="app">
    <box-message>
      <span>{{message}}</span>
    </box-message>
  </div>
```
```
  Vue.component('box-message', {
    template: `<div>
      <slot>This is message</slot>
    </div>`
  });
  const app = new Vue({
    el: "#app",
    data: {
      message: "This is message"
    }
  })
```
> with name
```
 <div id="app">
    <box-message>
      <template v-slot:message>
        <p>Hello World!</p>
      </template>
      <template v-slot:default>
        <span>This is default</span>
      </template>
      <template v-slot:title>
        <span>This is title</span>
      </template>
    </box-message>
  </div>
```
```
  Vue.component('box-message', {
    template: `<div>
      <slot name="message"></slot>
      <slot></slot>
      <slot name="title"></slot>
    </div>`
  });
```
> scope

## Dynamic Component
  ```
    <div id="app">
      <button v-on:click="onSwitch">Switch</button>
      <component v-bind:is="currentTabComponent"></component>
    </div>
  ```
  ```
    Vue.component('component-one', {
      template: `<div>component-one</div>`,
      created() {
        console.log('component-one created');
      },
      destroyed() {
        console.log('component-one destroy');
      },
    });
    Vue.component('component-two', {
      template: `<div>component-two</div>`,
      created() {
        console.log('component-two created');
      },
      destroyed() {
        console.log('component-two destroy');
      }
    });
    const app = new Vue({
      el: "#app",
      data: {
        currentTabComponent: 'component-one'
      },
      methods: {
        onSwitch: function() {
          this.currentTabComponent = this.currentTabComponent === 'component-one' ? 'component-two' : 'component-one';
        }
      },
    })
  ```
  > keep-alive
  ```
    <div id="app">
      <button v-on:click="onSwitch">Switch</button>
      <keep-alive>
        <component v-bind:is="currentTabComponent"></component>
      </keep-alive>
    </div>
  ```
  ```
    Vue.component('component-one', {
      template: `<div>component-one {{new Date()}}</div>`,
      created() {
        console.log('component-one created');
      },
      destroyed() {
        console.log('component-one destroy');
      },
    });
    Vue.component('component-two', {
      template: `<div>component-two {{new Date()}}</div>`,
      created() {
        console.log('component-two created');
      },
      destroyed() {
        console.log('component-two destroy');
      }
    });
  ```

## Mixin
  ### Basic
  ```
    <div id="app">
      {{message}}
      {{callback()}}
    </div>
  ```
  ```
    var mixin = {
      data: function () {
        return {
          message: 'Hello',
        }
      },
      created() {
        console.log('mixin called 1')
      },
      methods: {
        callback: function() {
          console.log('Hello 1');
        }
      },
    }

    var mixin2 = {
      data: function() {
        return {
          mixin2: 'Mixin2',
          message: 'Hello 2',
        }
      },
      created() {
        console.log('mixin called 2')
      },
      methods: {
        callback: function() {
          console.log('Hello 2');
        }
      },
    }

    const app = new Vue({
      el: "#app",
      mixins: [mixin, mixin2],
      data: {
        hello: 'Hello',
        message: 'Hey myself!'
      },
      created() {
        console.log('Component called');
        console.log(this.$data);
      },
      methods: {
        callback: function() {
          console.log('Hello myself');
        }
      },
    })
  ```
  ### Global Mixin
  ```
    <div id="app">
      {{message}}
    </div>
    <div id="app-2">
      {{message}}
      <input v-model="message">
    </div>
  ```
  ```
    Vue.mixin({
      data: function() {
        return {
          message: 'Hello'
        }
      }
    })

    const app = new Vue({
      el: "#app",
    })

    const app1 = new Vue({
      el: "#app-2",
    })
  ```

## Custom Directive
```
  <div id="app">
    <p v-text-ul>{{message}}</p>
  </div>
```
```
   Vue.directive('text-ul', function(el, binding) {
    el.textContent = el.textContent.toUpperCase();
  })

  const app = new Vue({
    el: "#app",
    data: {
      message: "Hello"
    }
  })
```
> with arg
```
  <div id="app">
    <p v-text-ul:lower>{{message}}</p>
  </div>
```
```
  Vue.directive('text-ul', function(el, binding) {
    const arg = binding.arg;
    if (arg === 'lower') {
      el.textContent = el.textContent.toLowerCase();
    } else {
      el.textContent = el.textContent.toUpperCase();
    }
  })
```
> with modifiers
```
  <div id="app">
    <p v-text-ul:lower.font-blue.font-small>{{message}}</p>
  </div>
```
```
  Vue.directive('text-ul', function(el, binding) {
    const arg = binding.arg;
    if (arg === 'lower') {
      el.textContent = el.textContent.toLowerCase();
    } else {
      el.textContent = el.textContent.toUpperCase();
    }
    if (binding.modifiers['font-red']) {
      el.style.color = 'red';
    } else if (binding.modifiers['font-blue']) {
      el.style.color = 'blue';
    }
    if (binding.modifiers['font-big']) {
      el.style.fontSize = 50 + 'px';
    } else if (binding.modifiers['font-small']) {
      el.style.fontSize = 5 + 'px';
    }
  })
```

## Filter
```
<div id="app">
  <p>{{message | text('upper')}}</p>
</div>
```
```
Vue.filter('text', function(...args) {
  let value = args.shift();
  if (!value) return '';
  if (args.includes('lower')) {
    value = value.toLowerCase();
  } else {
    value = value.toUpperCase();
  }
  return value;
})

const app = new Vue({
  el: "#app",
  data: {
    message: "Hello"
  },
})
```