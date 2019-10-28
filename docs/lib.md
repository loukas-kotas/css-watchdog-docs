
# Library 
Library includes all the functionality with the api in form of functions.

## Usage

In order to use the watchdog library, a new class instance should be created.
After that, you can call every available function.

* Note #1

Every function returns a promise. So you need to handle each function call as a promise.
Tip: use async/wait instead of catch/then in every function call.


#### Example

```
    const Watchdog = require('css-watchdog');
    ...
    const watchdog = new Watchdog(); 
    const font-size = watchdog.get_attribute_of_element('https://loukaskotas.com', 'about', 'font-size');

```

## Puppeteer

You can use pure puppeteer functions as it is simply by creating a puppeteer instance through Watchdog Class.

```javascript

const puppeteer = new Watchdog().puppeteer();

```

## Lifecycle Hooks

There are two lifecycle hooks:

1. beforeAll  --> Before every function call is executed

2. beforeEach --> Before each function call is executed

### beforeAll

It executes once with the Watchdog instance creation.
You need to provide it in the constructor while creating a class instance.

### beforeEach

It executes every time before a function call.
You need to provide it in the constructor while creating a class instance.

### Example
```javascript

const watchdog = new Watchdog();
const puppeteer = new Watchdog().puppeteer(); // use original puppeteer functionality
const pathToSave = 'assets'; // exists on root


const beforeAll = function() {

    const browser = await puppeteer.launch();
    const page    = await browser.newPage();
    await page.goto('https://example-page.com');
    await page.type('#usename', 'my-username', {delay: 10}) // select item with id=username and type 'my-username'.
    await page.type('#password', 'my-password', {delay: 10}) // select item with id=password and type 'my-password'.
    await page.click('#login-button'); // login on item with id=login-button.
    await page.waitFor(2000); // wait for page to load.
    const cookies = await page.cookies(); // get cookies after successful for later use.
    jsonfile.writeFileSync('./assets/cookies.json', {data: cookies}); // write cookies on file for later use.
    return browser; // browser will be used in beforeEach to keep the same session live.


}

const beforeEach = function() {

      const cookies = jsonfile.readFileSync('./assets/cookies.json').data; // read cookies that have been set from beforeAll().
      const page    = await browser.newPage(); 
      await page.setCookie(...cookies); // set cookies on new page to avoid further login.
      return page; // page will be used from every function of Watchdog Class

}

```


## Attributes


### 1. Get specific attributes of every element in source 

**Parameters**

| Parameter | Description |
| --------- | ----------- |
| source: String    | url to be used |
| attributes: Array [String] | Array of attribute names |

**Syntax**

```javascript
get_attributes(source, attributes)
```

**Example**

```javascript
const watchdog = new Watchdog();
const result = await watchdog.get_attributes('https://loukaskotas.com', ['font-size', 'background-color']);
```

### 2. Get specific attributes of elements by class name 

**Parameters**

| Parameter | Description |
| --------- | ----------- |
| source: String    | url to be used |
| attributes: Array [String] | Array of attribute names |
| className: String | Class Name to filter out elements  |

**Syntax**

```javascript
get_class(source, attributes, classname)
```

**Example**

```javascript
const watchdog = new Watchdog();
const result = await watchdog.get_attributes('https://loukaskotas.com', ['font-size', 'background-color'], '.about-block');
```


### 3. Get specific attribute of element by ID 

**Parameters**

| Parameter | Description |
| --------- | ----------- |
| source: String    | url to be used |
| elementId: String | ID of element as being displayed on the page  |
| attribute: String | Desired Attribute's value  |

**Syntax**

```javascript
get_attribute_of_element(source, elementId, attribute)
```

**Example**

```javascript
const watchdog = new Watchdog();
const result = await watchdog.get_attribute_of_element('https://loukaskotas.com', 'about', 'font-size');
```

### 4. Get specific attribute of element by Tag name 

**Parameters**

| Parameter | Description |
| --------- | ----------- |
| source: String    | url to be used |
| attributes: Array[String] | Desired attributes from every tag |
| tags: Array[String] | Tags to select from page |

**Syntax**

```javascript
get_tags(source, attributes, tags)
```

**Example**

```javascript
const watchdog = new Watchdog();
const result = await watchdog.get_tags('https://loukaskotas.com', ['font-size', 'background-color'], ['h1', 'section', 'p']);
```


## Visual Regression

### 1. Get screenshot of whole page 

**Parameters**

| Parameter | Description |
| --------- | ----------- |
| source: String    | url to be used |
| pathToSave: String | Path to export **Careful! Only middle backslashes allowed. e.g myproject/assets/images/ --> assets/images** |

**Syntax**

```javascript
screenshot_whole_page(source, pathToSave)
```

**Example**

```javascript
const watchdog = new Watchdog();
const result = await watchdog.screenshot_whole_page('https://loukaskotas.com', 'assets');
```

### 2. Get screenshot of specific part at page 

**Parameters**

| Parameter | Description | 
| --------- | ----------- |
| source: String    | url to be used |
| pathToSave: String | Path to export **Careful! Only middle backslashes allowed. e.g /myproject/assets/images/ --> assets/images** |
| x0: Number    | starting point x-axis |
| y0: Number    | starting point y-axis |
| x1: Number    | ending point x-axis |
| y1: Number    | ending point y-axis |

**Syntax**

```javascript
screenshot_part_page(source, pathToSave, x0, y0, x1, y1)
```

**Example**

```javascript
const watchdog = new Watchdog();
const result = await watchdog.screenshot_part_page('https://loukaskotas.com', 'assets', 0, 0, 100, 100);
```


### 3. Get screenshot of specific element 

**Parameters**

| Parameter | Description | 
| --------- | ----------- |
| source: String    | url to be used |
| pathToSave: String | Path to export **Careful! Only middle backslashes allowed. e.g /myproject/assets/images/ --> assets/images** |
| elementId: String | ID of element to screenshot |

**Syntax**

```javascript
screenshot_element(source, pathToSave, elementId)
```

**Example**

```javascript
const watchdog = new Watchdog();
const result = await watchdog.screenshot_element('https://loukaskotas.com', 'assets', 'experience');
```

### 4. Compare two images (pixel-to-pixel) 

**Parameters**

| Parameter | Description | 
| --------- | ----------- |
| sourceImagePath: String | path of source image (prefer relative) |
| targetImagePath: String | path of target image (prefer relative) |
| pathToSave: String | Path to export **Careful! Only middle backslashes allowed. e.g /myproject/assets/images/ --> assets/images** |

**Syntax**

```javascript
compare_images(sourceImagePath, targetImagePath, pathToSave)
```

**Example**

```javascript
const watchdog = new Watchdog();
const result = await watchdog.compare_images('./assets/images/source.png', './assets/images/target.png', 'assets');
```


### 5. Compare two domains 

**Parameters**

| Parameter | Description | 
| --------- | ----------- |
| sourceDomain: String | url of source domain |
| targetDomain: String | url of target domain |
| pathToSave: String | Path to export **Careful! Only middle backslashes allowed. e.g /myproject/assets/images/ --> assets/images** |


**Syntax**

```javascript
compare_domains(sourceDomain, targetDomain, pathToSave)
```

**Example**

```javascript
const watchdog = new Watchdog();
const result = await watchdog.compare_domains('https://mysite.dev.com', 'https://mysite.prod.com', 'assets');
```


### 6. Get specific element's position 

**Parameters**

| Parameter | Description | 
| --------- | ----------- |
| source: String | url of source domain |
| elementID: String | ID of element |

**Syntax**

```javascript
get_element_position(source, elementID)
```

**Example**

```javascript
const watchdog = new Watchdog();
const result = await watchdog.get_element_position('https://loukaskotas.com', 'about');
```