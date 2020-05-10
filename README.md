# Vue 101
 ใช้ MVVM pattern

# Install 
- สามารถใช้ cdn ได้
```html
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```
- vue cli `(Recommended)`

# App
```html
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
```html
<body>
    <div id="app">
        <p>Hello: getReverse()</p>
    </div>
</body>
<script>
    const app = new Vue({
        el: '#app',
        data: {
            message: 'Hello Angular'
        },
        methods: {
            getReverse: function() {
                return this.message.split('').reverse().join('')
            }
        }
    })
</script>
```
ex.2
```html
<body>
    <div id="app">
        <p>Hello: getReverse()</p>
    </div>
</body>
<script>
    const app = new Vue({
        el: '#app',
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
    })
</script>
```
ex.3 event
```html
<body>
    <div id="app">
        <p>Count: {{count}}</p>
        <button v-on:click="addCounter">add</button>
    </div>
</body>
<script>
    const app = new Vue({
        el: '#app',
        data: {
            count: 0
        },
        methods: {
            addCounter: function(event) {
                this.count += 1;
            }
        }
    })
</script>
```
ex.4 value
```html
<body>
    <div id="app">
        <p>Count: {{count}}</p>
        <button v-on:click="addCounter(1)">add</button>
    </div>
</body>
<script>
    const app = new Vue({
        el: '#app',
        data: {
            count: 0
        },
        methods: {
            addCounter: function(value) {
                this.count += value;
            }
        }
    })
</script>
```
ex.4 value + event
```html
<body>
    <div id="app">
        <p>Count: {{count}}</p>
        <button v-on:click="addCounter(1, $event)">add</button>
    </div>
</body>
<script>
    const app = new Vue({
        el: '#app',
        data: {
            count: 0
        },
        methods: {
            addCounter: function(value, event) {
                this.count += value;
            }
        }
    })
</script>
```

# Forms

ex.1 show value
```html
<body>
    <div id="app">
        <p>Message: {{message}}</p>
        <input :value="message"/>
    </div>
</body>
<script>
    const app = new Vue({
        el: '#app',
        data: {
            message: 'Hello Angular'
        }
    })
</script>
```
ex.2 checkbox
```html
<body>
    <div id="app">
        <p>Message: {{message}}</p>
        <input :value="message"/>
        <label for="checkbox">{{checked}}</label>
        <input type="checkbox" id="checkbox" v-model="checked">
    </div>
</body>
<script>
    const app = new Vue({
        el: '#app',
        data: {
            message: 'Hello Angular',
            checked: false
        }
    })
</script>
```
ex.3 v-model+value -> checkbox value 
```html
<body>
    <div id="app">
        <p>Message: {{message}}</p>
        <input :value="message"/>
        <label for="checkbox">{{checked}}</label>
        <input type="checkbox" id="checkbox" v-model="checked" true-value="yes" false-value="no">
    </div>
</body>
<script>
    const app = new Vue({
        el: '#app',
        data: {
            message: 'Hello Angular',
            checked: 'no'
        }
    })
</script>
```

ex.4 select v-bind
```html
<body>
    <div id="app">
        <select v-model="selected">
            <option v-bind:value="{number: 1}">1</option>
            <option v-bind:value="{number: 2}">2</option>
        </select>
    </div>
</body>
<script>
    const app = new Vue({
        el: '#app',
        data: {
            selected: null
        }
    })
</script>
```
ex.5 input number แปลง เป็นให้
```html
<body>
    <div id="app">
        <input v-model.number="price" type="number"/>
    </div>
</body>
<script>
    const app = new Vue({
        el: '#app',
        data: {
            price: 0
        }
    })
</script>
```

# Watchers 
    observe ตัวแปล เพื่อจะทำอะไรสักอย่าง

ex.1
```html
<body>
    <div id="app">
        <p>{{messageUpper}}</p>
        <input v-model="message"/>
    </div>
</body>
<script>
    const app = new Vue({
        el: '#app',
        data: {
            message: '',
            messageUpper: ''
        },
        watch: {
            message: function() {
                this.messageUpper = this.message.toUpperCase()
            }
        }
    })
</script>
```
ex.2 auto complete
หลีกเลี่ยง การใช้ arrow function ใน callback `(Recommended)`
```html
<body>
    <div id="app">
        <p>{{messageUpper}}</p>
        <input v-model="message"/>
    </div>
</body>
<script>
    const app = new Vue({
        el: '#app',
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
    })
</script>
```

# Computed `(Recommended)`
    มองสิ่งที่เปลี่ยนแปลงใน scope, สามารถ watch ได้หลายตัว

ex.1
```html
<body>
    <div id="app">
        <p>Message : {{message}}</p>
        <p>Reverse Message : {{reverseMessage}}</p>
        <p>{{date}}</p>
        <input v-model="message"/>
    </div>
</body>
<script>
    const app = new Vue({
        el: '#app',
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
    })
</script>
```
ex.2 getter setter
```html
<body>
    <div id="app">
        <p>First Name : {{firstName}}</p>
        <p>Last Name : {{lastName}}</p>
        <p>Full Name : {{fullName}}</p>
    </div>
</body>
<script>
    const app = new Vue({
        el: '#app',
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
    })
</script>
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
- ก่อนที่ Vue จะ compile DOM
    - beforeMount - มีของใน `data`, `methods`, `computed` แล้วสามารถ access ได้
- หลังจากที่ Vue compile DOM
    - mounted - มีของใน `data`, `methods`, `computed` แล้วสามารถ access ได้หมด  (add listener)
- เมื่อมีการเปลี่ยนค่า 
    - beforeUpdate -> เมื่อ DOM จะ re-render เปลี่ยนค่าได้นะ
    - updated -> เมื่อ DOM จะ re-render แล้วยังเปลี่ยนค่าได้นะ
- ก่อนที่ Vue จะถูกทำลาย
    - beforeDestroy (remove listener)
    - destroyed `app.$destroy()`

ex
```html
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


# Components
    React -> virtual DOM <div> <span> <p>
    Vue -> virtual DOM <div> <span> <p>
    Angular -> shadow DOM <app-angular>

```html
Vue.component(name, { data: function() {}, template: 'html template' });
```
- `component`, data
ex
```html
<body>
    <div id="app">
        <box-title></box-title>
        <box-message></box-message>
    </div>
</body>
<script>
    Vue.component('box-title', {
        data: function() {
            return {
                count: 0
            }
        },
        template: `
            <button v-on:click="count++">Count {{count}}</button>
        `
    });
    Vue.component('box-message', {
        data: function() {
            return {
                message: 'Hello',
            }
        },
        template: `
            <div>
                <p>{{message}}</p>
                <input v-bind="message"/>
            </div>
        `
    });
    const app = new Vue({
        el: '#app'
    })
</script>
```

- `props` คือ data ที่ถูกส่งเข้าไปใน component
```html
<body>
    <div id="app">
        <box-title v-bind:count="count"></box-title>
        <box-message></box-message>
    </div>
</body>
<script>
    Vue.component('box-title', {
        props: ['count'],
        data: function() {
            rawCount: this.count
        },
        template: `
            <button v-on:click="count++">Count {{rawCount}}</button>
        `
    });
    Vue.component('box-message', {
        props: {
            message: {
                type: 'string',
                default: function() {
                    return 'Hello'
                }
            }
        },
        data: function() {
            return {
                rawMessage: 'Hello',
            }
        },
        template: `
            <div>
                <p>{{rawMessage}}</p>
                <input v-bind="rawMessage"/>
            </div>
        `
    });
    const app = new Vue({
        el: '#app',
        data: {
            count: 0
        }
    })
</script>
```

- `emitting` คือ การส่ง data จากลูกไปหาแม่
ex.1
```html
<body>
    <div id="app">
        {{count}}
        <box-title v-bind:count="count" v-on:target-click="count+1"></box-title>
    </div>
</body>
<script>
    Vue.component('box-title', {
        props: ['count'],
        data: function() {
            rawCount: this.count
        },
        template: `
            <button v-on:click="$emit('target-click')">Count {{rawCount}}</button>
        `
    });
    const app = new Vue({
        el: '#app',
        data: {
            count: 0
        }
    })
</script>
```
ex.2 emit + value
```html
<body>
    <div id="app">
        {{count}}
        <box-title v-bind:count="count" v-on:target-click="count+$event"></box-title>
    </div>
</body>
<script>
    Vue.component('box-title', {
        props: ['count'],
        template: `
            <button v-on:click="$emit('target-click', count + 1)">Count {{count}}</button>
        `
    });
    const app = new Vue({
        el: '#app',
        data: {
            count: 0
        }
    })
</script>
```

ex.3 to methods emit + value
```html
<body>
    <div id="app">
        {{count}}
        <box-title v-bind:count="count" v-on:target-click="onAdd($event)"></box-title>
    </div>
</body>
<script>
    Vue.component('box-title', {
        props: ['count'],
        methods: {
            onClick: function() {
                this.$emit('target-click', this.count + 1)
            }
        }
        template: `
            <button v-on:click="onClick">Count {{rawCount}}</button>
        `
    });
    const app = new Vue({
        el: '#app',
        data: {
            count: 0
        },
        methods: {
            onAdd: function(event) {
                this.count += event;
            }
        }
    })
</script>
```
- slot
 React -> props.children
 Angular -> <ng-content>

ex.1 slot basic
```html
<body>
    <div id="app">
        <box-message>
            <p>Hello Slot</p>
        </box-message>
    </div>
</body>
<script>
    Vue.component('box-message', {
        props: ['message']
        template: `
            <div>
                <slot></slot>
                <p>{{message}}</p>
                <input v-bind="message"/>
            </div>
        `
    });
    const app = new Vue({
        el: '#app'
    })
</script>
```
ex.2 slot title
```html
<body>
    <div id="app">
        <box-message>
            <template v-slot:title>
                <p>Hello Slot title</p>
            </template>
            <p>Hello Slot</p>
        </box-message>
    </div>
</body>
<script>
    Vue.component('box-message', {
        props: ['message'],
        template: `
            <div>
                <slot name="title"></slot>
                <p>{{message}}</p>
                <input v-bind="message"/>
            </div>
        `
    });
    const app = new Vue({
        el: '#app'
    })
</script>
```

ex.3 slot default
```html
<body>
    <div id="app">
        <box-message>
            <template v-slot:title>
                <p>Hello Slot title</p>
            </template>
            <template v-slot:span>
                <p>Hello Slot span</p>
            </template>
            <template v-slot:default>
                <p>Hello Slot default</p>
            </template>
        </box-message>
    </div>
</body>
<script>
    Vue.component('box-message', {
        props: ['message'],
        template: `
            <div>
                <slot name="title"></slot>
                <slot></slot>
                <slot name="span"></slot>
                <p>{{message}}</p>
                <input v-bind="message"/>
            </div>
        `
    });
    const app = new Vue({
        el: '#app'
    });
</script>
```

- dynamic component
ex.1
```html
<body>
    <div id="app">
        <button v-on:click="onSwitch">Switch</button>
        <component v-bind:is="componentBoxTitle"></component>
    </div>
</body>
<script>
    Vue.component('box-title', {
        data: function() {
            return {
                count: 0
            }
        },
        template: `
            <button v-on:click="count++">Count {{count}}</button>
        `
    });
    Vue.component('box-message', {
        props: ['message'],
        template: `
            <div>
                <p>{{message}}</p>
                <input v-bind="message"/>
            </div>
        `
    });
    const app = new Vue({
        el: '#app',
        data: {
            componentBoxTitle: 'box-title'
        },
        methods: {
            onSwitch: function() {
                this.componentBoxTitle = this.componentBoxTitle === 'box-title' ? 'box-message' : 'box-title';
            }
        }
    })
</script>
```
ex.2 <keep-alive>
```html
<body>
    <div id="app">
        <button v-on:click="onSwitch">Switch</button>
        <keep-alive>
        <component v-bind:is="componentBoxTitle"></component>
        </keep-alive>
    </div>
</body>
<script>
    Vue.component('comp-a', {
        template: `
            <div>
                {{new Date()}}
            </div>
        `
    });
    Vue.component('comp-b', {
        template: `
            <div>
                {{new Date()}}
            </div>
        `
    });
    const app = new Vue({
        el: '#app',
        data: {
            componentBoxTitle: 'comp-a'
        },
        methods: {
            onSwitch: function() {
                this.componentBoxTitle = this.componentBoxTitle === 'comp-a' ? 'comp-a' : 'comp-b';
            }
        }
    })
</script>
```
ex.3 props
```html
<body>
    <div id="app">
        <button v-on:click="onSwitch">Switch</button>
        <keep-alive>
        <component v-bind:is="comp" v-bind="currentProps"></component>
        </keep-alive>
    </div>
</body>
<script>
    Vue.component('comp-a', {
         props: ['message'],
        template: `
            <div>
                {{new Date()}}{{message}}
            </div>
        `
    });
    Vue.component('comp-b', {
        props: ['message'],
        template: `
            <div>
                {{new Date()}} {{message}}
            </div>
        `
    });
    const app = new Vue({
        el: '#app',
        data: {
            comp: 'comp-a',
        },
        computed: {
            currentProps: function() {
                if (this.comp === 'comp-a') {
                    return {
                        message: 'Hello A'
                    }
                } else {
                    return {
                        message: 'Hello B'
                    }
                }
            }
        },
        methods: {
            onSwitch: function() {
                this.comp = this.comp === 'comp-a' ? 'comp-b' : 'comp-a';
            }
        }
    })
</script>
```