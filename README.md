# polycast
I am following through Polycasts from Rob Dodson

### Polycast #14 (01)

### Polycast #15 (02) - Type Extension Element

### Polycast #16 (03) - Element API

### Polycast #17 (04) - Theming Elements
**::shadow and /deep/**
1. Break encapsulation (need specific `ids` to target elements)
2. Nerf potential perf. gains

### Polycast #18-19, #52 (05) - Polymer Starter Kit
[Material Palette](https://www.materialpalette.com)
[Offline Cookbook](https://jakearchibald.com/2014/offline-cookbook/)[intro to Service Worker](https://developers.google.com/web/fundamentals/getting-started/primers/service-workers)
```bash
polymer init
# choose starter-kit

polymer build # generate bundled/unbundled versions
# Bundled: gather all html files into one html file. Sharded using web components shard.
# Unbundled: seperate the source files. More bleeding edge folks.
# Vulganized html is a reduced HTML file and its dependent HTML Imports into one file


polymer serve build/bundled # run bundled version

npm install -g generator-polymer-init-custom-build # install a custom build element

# Follow [guide](https://github.com/gulpjs/gulp/blob/master/docs/getting-started.md)
npm install --global gulp-cli
npm install --save-dev gulp-uglify # minify all the static files


```

### Polycast #28, #30, #32, #35 - Data Binding & Observers

```html

<!--Observers-->
<div>Manage: {{user.manager}}</div>
<button on-tap="changeManager">Change Manager</button>

<script>
    Polymer({
        is: 'employee-record',
        properties: {
            user: {
                type: Object,
                value: () => { name: 'Stephen', manager: 'Johnny' };
            }
        },
        changeManager: () => { 
            /*
                these approaches are much less expensive  than doing:
                this.user = { ... };
                Only set a specific attribute
            */
            this.set('user.manager', 'James');
            //alternatively, you can do this.
            //this.user.manager = 'James';
            //this.notifyPath('user.manager');
        }
    })

</script>

<!-- Handing Objects -->
<div>Manage: {{user.manager}}</div>
<paper-input value="{{user.manager}}">Change Manager</paper-input>

<script>
    Polymer({
        is: 'employee-record',
        properties: {
            user: {
                type: Object,
                value: () => { name: 'Stephen', manager: 'Johnny' };
            }
        },
    })
</script>


<script>
    // Observers
    polymer({
        is: 'slee-unicorn',
        properties: {
            barks: {
                type: Number,
                observer: 'barksChanged'
            }
        },
        barksChanged: () => {
            // do something
        }
    });
</script>

<div><span>{{blah}} by: {{pop}}</span></div>
<script>
    polymer({
        is: 'zombie-controller',
        properties: {
            zombies: Object,
            shovels: Number,
            bio: {
                type: Object,
                value: () => { name: 'Monster', maker: 'Shannel', poop: 'horse' };
            }
        },
        observers: [
            'inventoryChanged(zombies, shovels)',
            'bioChanged(bio.*)'
        ],
        inventoryChanged: (zombies, shovels) => {
            // if (zombies > shovels), do sth
        },
        bioChanged: (changeRecord) => {
            switch(changeRecord.path) {
                case 'bio.maker':
                    this.blah = this.bio.maker;
                    break; 
                case 'bio.name':
                    this.pop = this.bio.name;
                    break; 
                case 'bio.poop':
                    this.what = this.bio.poop;
                default:
                    console.log('write something.');
            }
            if (changeRecord.path == 'bio.maker') {
                this.blah = this.bio.maker;
            } else if (changeRecord.path == 'bio.name') {
                this.pop = this.bio.name;
            }
        }
    });
</script>

<!--Binding to Arrays-->
<h1>1st Place: {{firstUser}}</h1>
<h1>1st Place: {{computeUser(users.*, 0)}}</h1>
<script>
    Polymer({
        is: 'high-score',
        properties: {
            users: {
                type: Array,
                value: () => (['James', 'John', 'Peter']);
            }
        },
        observers: ['usersChanged(users.*, 0)'],
        usersChanged: (changeRecord, index) {
            this.firstUser = changeRecord.base[index];
        },
        computeUser: (changeRecord, index) {
            return changeRecord.base[index];
        }
    })
</script>
```

### Polycast #36 - Unit Testing with Web Component Tester
```bash
npm install -g web-component-tester
bower install -g web-component-tester
wct # run unit tests
wct -l chrome
```

[install Safari Webdriver](http://selenium-release.storage.googleapis.com/index.html?path=2.48/)

[installation guide](http://elementalselenium.com/tips/69-safari)
**Make sure to `enable automation` in Safari**

```html 
```
