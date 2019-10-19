# API

## 1. Get specific style field on page
| Method | URL | Body |
| ------ |:---:|:----:|
| GET | /api/fields/facade | { "source": "https://loukaskotas.com", "fields": [ "font-family" ] } |

## 2. Get specific style fields of specific tags on page
| Method | URL | Body |
| ------ |:---:|:----:|
| GET | /api/fields/tags/facade | { "source": "http://loukaskotas.com", "fields": [ "font-family", "color", "background-color", "border" ], "tags": [ "h1" ] } |

## 3. Get screenshot of specific element on page
| Method | URL | Body |
| ------ |:---:|:----:|
| GET | /api/screenshots/element/facade | { "source": "https://loukaskotas.com",  "elementId": "experience" } |

## 4. Get Screenshot of whole page 
| Method | URL | Body |
| ------ |:---:|:----:|
| GET | /api/screenshots/domain/facade | { "source": "http://loukaskotas.com" } |

## 5. Get all fonts from page
| Method | URL | Body |
| ------ |:---:|:----:|
| GET | /api/fonts/facade | { "source": "http://loukaskotas.com" } |

## 6. Compare Two Screenshots
| Method | URL | Body |
| ------ |:---:|:----:|
| GET | /api/screenshots/compare/facade | { "source": "http://loukaskotas.com", "elementId": "experience" } |


## 7. Get specific style fields of specific class on page (not implemented yet)
| Method | URL | Body |
| ------ |:---:|:----:|
| GET | /api/fields/class/facade | { "source": "http://loukaskotas.com", "fields": [ "font-family", "color", "background-color", "border" ], "class": "section" } |
