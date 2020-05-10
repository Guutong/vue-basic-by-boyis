# Vue 101
 ใช้ MVVM pattern

# Install 
- สามารถใช้ cdn ได้
```
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```
- vue cli (Recommended)

# App
```
  <body>
    <div id="app">
      <p>Hello Vue</p>
    </div>
  </body>
  <script>
    const app = new Vue({})
  </script>
```

# Template Syntax
- Interpolations
    
- Directive
    - v-[directive name]:[argument-name] // directive pattern
    - v-if 
        ```
        <p v-if="type === 'A"> show </p>
        ```
    - v-else 
        ```
        <p v-if="type === 'A"> show </p>
        <p v-else> not show </p>
        ```
    - v-else-if 
    - v-show ใช้กับ css
    - v-for loop ใน template
        
        ex.1
        ```
        <p v-for="(v, i) in list">{{v}}</p>
        ...
        data: {
            list: [1,2,3,4]
        }
        ```
        ex.2
        ```
        <p v-for="(value, key) in obj">{{value}}</p>
        ...
        data: {
            obj: {
                key1: 'value1',
                key2: 'value2',
                key3: 'value3',
            }
        }
        ```
    - v-bind access data ใน attribute
        
        ex.1
        ```
        <p v-bind:title>Hello Vue</p>
        ...
        data: {
            title: 'Hello Angular'
        }
        ```

        ex.2
        ```
        <p v-bind:[attr]>Hello Vue</p>
        ...
        data: {
            attr: 'title',
            title: 'Hello Angular'
        }
        ```
    - v-on event listener ฟัง event ที่เกิดขึ้น
        ```
        <button v-on:click="count += 1">add</button>
        ...
        data: {
            count: 0
        }
        ```

- ShortHands
    - v-bind
        -> v-bind:title
        -> :title
    - v-on
        -> v-on:click
        -> @click

- Modifiers
    - v-[directive-name]:[argument-name].[modifier-name]
    - v-[directive-name].[modifier-name]
    - v-[directive-name]:[argument-name].[modifier-name].[modifier-name]

        - v-model
            
            ex.1
            ```
                <p>Message: {{message}}</p>
                <input v-model="message"/>
                ...
                data: {
                    message: 'Hello Angular'
                }
            ```
            ex.2 on key
            ```
                <p>Message: {{message}}</p>
                <input v-model="message" v-on:keydown.enter="onKey"/>
                ...
                data: {
                    message: 'Hello Angular'
                },
                methods: {
                    onKey: function() {
                        console.log('on enter key')
                    }
                }
            ``` 
            ex.3 on key command + c
            ```
                <p>Message: {{message}}</p>
                <input v-model="message" v-on:keydown.meta.67="onKey"/>
                ...
                data: {
                    message: 'Hello Angular'
                },
                methods: {
                    onKey: function() {
                        console.log('on enter key command + c')
                    }
                }
            ``` 
            ex.4 .lazy ทำที่หลังจาก เปลี่ยน event
            ```
                <p>Message: {{message}}</p>
                <input v-model.lazy="message"/>
                ...
                data: {
                    message: 'Hello Angular'
                }
            ``` 

# Methods

ex.1
```
<p>Hello: getReverse()</p>
...
data: {
    message: 'Hello Angular'
},
methods: {
    getReverse: function() {
        return this.message.split('').reverse().join('')
    }
}
```
ex.2
```
<p>Hello: getReverse()</p>
...
data: {
    message: 'Hello Angular'
},
methods: {
    getReverse: function() {
        return this.join(this.message.split('').reverse())
    },
    join: function(value) {
        return value.join('')
    }
}
```
ex.3 event
```
<p>Count: {{count}}</p>
<button v-on:click="addCounter">add</button>
...
data: {
    count: 0
},
methods: {
    addCounter: function(event) {
        this.count += 1;
    }
}
```
ex.4 value
```
<p>Count: {{count}}</p>
<button v-on:click="addCounter(1)">add</button>
...
data: {
    count: 0
},
methods: {
    addCounter: function(value) {
        this.count += value;
    }
}
```
ex.4 value + event
```
<p>Count: {{count}}</p>
<button v-on:click="addCounter(1, $event)">add</button>
...
data: {
    count: 0
},
methods: {
    addCounter: function(value, event) {
        this.count += value;
    }
}
```

# Forms
  
ex.1 show value
```
    <p>Message: {{message}}</p>
    <input :value="message"/>
    ...
    data: {
        message: 'Hello Angular'
    }
```
ex.2 checkbox
```
    <p>Message: {{message}}</p>
    <input :value="message"/>
    <label for="checkbox">{{checked}}</label>
    <input type="checkbox" id="checkbox" v-model="checked">
    ...
    data: {
        message: 'Hello Angular',
        checked: false
    }
```
ex.3 v-model+value -> checkbox value 
```
    <p>Message: {{message}}</p>
    <input :value="message"/>
    <label for="checkbox">{{checked}}</label>
    <input type="checkbox" id="checkbox" v-model="checked" true-value="yes" false-value="no">
    ...
    data: {
        message: 'Hello Angular',
        checked: 'no'
    }
```

ex.4 select v-bind
```
    <select v-model="selected">
        <option v-bind:value="{number: 1}">1</option>
        <option v-bind:value="{number: 2}">2</option>
    </select>
    ...
    data: {
        selected: null
    }
```
ex.5 select v-bind option
```
    <select v-model="selected">
        <option v-bind:value="bindone">1</option>
        <option v-bind:value="{number: 2}">2</option>
    </select>
    ...
    data: {
        bindone: {number: 1},
        selected: null
    }
```