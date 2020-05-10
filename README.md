# Vue 101
 ใช้ MVVM pattern

# Install 
- สามารถใช้ cdn ได้
```
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```
- vue cli `(Recommended)`

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
ex.5 input number แปลง เป็นให้
```
    <input v-model.number="price" type="number"/>
    ...
    data: {
        price: 0
    }
```

# Watchers 
    observe ตัวแปล เพื่อจะทำอะไรสักอย่าง

ex.1
```
    <p>{{messageUpper}}</p>
    <input v-model="message"/>
    ...
    data: {
        message: '',
        messageUpper: ''
    },
    watch: {
        message: function() {
            this.messageUpper = this.message.toUpperCase()
        }
    }
```
ex.2 auto complete
หลีกเลี่ยง การใช้ arrow function ใน callback `(Recommended)`
```
    <p>{{messageUpper}}</p>
    <input v-model="message"/>
    ...
    data: {
        message: '',
        timeout: null,
    },
    methods: {
        querySearch: function() {
            console.log('hello')
        }
    },
    watch: {
        message: function() {
            clearTimeout(this.timeout);
            const _this = this;
            this.timeout = setTimeout(function() {
                _this.querySearch();
            }, 800)
        }
    }
```

# Computed `(Recommended)`
    มองสิ่งที่เปลี่ยนแปลงใน scope, สามารถ watch ได้หลายตัว

ex.1
```
    <p>Message : {{message}}</p>
    <p>Reverse Message : {{reverseMessage}}</p>
    <p>{{date}}</p>
    <input v-model="message"/>
    ...
    data: {
        message: 'Hello Angular',
    },
    computed: {
        reverseMessage: function() {
           return this.message.split('').reverse().join('')
        },
        date: function() {
            console.log(this.message)
            return new Date()
        }
    }
```
ex.2 getter setter
```
    <p>First Name : {{firstName}}</p>
    <p>Last Name : {{lastName}}</p>
    <p>Full Name : {{fullName}}</p>
    ...
    data: {
        firstName: 'John',
        lastName: 'Son',
        fullName: 'John Son',
    },
    computed: {
        // getter default
        // setter
        fullName: {
            get: function() {
                return this.firstName + ' ' + this.lastName;
            }
            set: function(val) {
                const [firstName, lastName] = val.split(' ');
                this.firstName = firstName;
                this.lastName = lastName;
            }
        }
    }
```

# ความแตกต่าง
- Computed vs Methods
    - computed มี cache
    - methods ไม่มี cache
- Computed vs Watchers
    - computed observe ได้มากกว่า 1 ตัว
    - watchers observe ได้ 1 ตัว
    - watchers เป็น 2 way binding

# LifeCycle
![](https://vuejs.org/images/lifecycle.png)

- ก่อนที่ Vue จะ create instance 
    - beforeCreate - ของใน `data`, `methods` ยังไม่ถูกสร้าง
    - created
    ex.1
    ```
    <body>
        <div id="app">
            <p>{{message}}</p>
        </div>
    </body>
    <script>
        const app = new Vue({
            el: '#app',
            beforeCreate() {
                console.log('Vue ::beforeCreated::');
            },
            created() {
                console.log('Vue ::created::');
            }
        })
    </script>
    ``` 
- ก่อนที่ Vue จะ compile DOM
    - beforeMount - มีของใน `data`, `methods`, `computed` แล้ว สามารถ access ได้
    ex.1
    ```
    <body>
        <div id="app">
            <p>{{message}}</p>
        </div>
    </body>
    <script>
        const app = new Vue({
            el: '#app',
            beforeCreate() {
                console.log('Vue ::beforeCreated::');
            },
            created() {
                console.log('Vue ::created::');
            },
            beforeMount() {
                console.log('Vue ::beforeMount::');
            }
        })
    </script>
    ``` 
- หลังจากที่ Vue compile DOM
    - mounted - มีของใน `data`, `methods`, `computed` แล้ว สามารถ access ได้หมด  (add listener)
    ex.1
    ```
    <body>
        <div id="app">
            <p>{{message}}</p>
        </div>
    </body>
    <script>
        const app = new Vue({
            el: '#app',
            beforeCreate() {
                console.log('Vue ::beforeCreated::');
            },
            created() {
                console.log('Vue ::created::');
            },
            beforeMount() {
                console.log('Vue ::beforeMount::');
            },
            mounted() {
                console.log('Vue ::mounted::');
            }
        })
    </script>
    ```

- เมื่อมีการเปลี่ยนค่า 
    - beforeUpdate -> เมื่อ DOM จะ re-render เปลี่ยนค่าได้นะ
    - updated -> เมื่อ DOM จะ re-render แล้ว ยังเปลี่ยนค่าได้นะ

    ex.1
    ```
    <body>
        <div id="app">
            <p>{{message}}</p>
        </div>
    </body>
    <script>
        const app = new Vue({
            el: '#app',
            beforeCreate() {
                console.log('Vue ::beforeCreated::');
            },
            created() {
                console.log('Vue ::created::');
            },
            beforeMount() {
                console.log('Vue ::beforeMount::');
            },
            mounted() {
                console.log('Vue ::mounted::');
            },
            beforeUpdate() {
                console.log('Vue ::beforeUpdate::');
            },
            updated() {
                console.log('Vue ::updated::');
            },
        })
    </script>
    ``` 
- ก่อนที่จะถูกทำลาย
    - beforeDestroy (remove listener)
    - destroyed (app.$destroy())
    ex.1
    ```
    <body>
        <div id="app">
            <p>{{message}}</p>
        </div>
    </body>
    <script>
        const app = new Vue({
            el: '#app',
            beforeCreate() {
                console.log('Vue ::beforeCreated::');
            },
            created() {
                console.log('Vue ::created::');
            },
            beforeMount() {
                console.log('Vue ::beforeMount::');
            },
            mounted() {
                console.log('Vue ::mounted::');
            },
            beforeUpdate() {
                console.log('Vue ::beforeUpdate::');
            },
            updated() {
                console.log('Vue ::updated::');
            },
            beforeDestroy() {
                console.log('Vue ::beforeDestroy::');
            },
            destroyed() {
                console.log('Vue ::destroyed::');
            },
        })
    </script>
    ``` 