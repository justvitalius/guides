# Стиль написания на ReactJS

## <a name='TOC'>Оглавление</a>

  1. [Порядок объявления методов внутри React компонента](#named_position)
  1. [Наименование обработчиков `handleEventName`](#handle_event_name)
  1. [JSX и шаблонизация](#xsx_or_not_jsx)

## <a name='named_position'>Порядок объявления методов внутри React компонента</a>
- Указывайте стандартные методы из `React Workflow` всегда вверху компонента. Последовательность объявления стандартных методов очень проста: следуйте порядку следования методов в `workflow`. 
- Все дополнительные методы объявляйте под методом `render`.

```javascript
React.createClass({
    mixins : [],
    displayName: ''
    propTypes: {},
    
    getDefaultProps: getDefaultProps,
    getInitialState: getInitialState,

    componentWillMount : componentWillMount,
    componentWillReceiveProps: componentWillReceiveProps,
    componentWillUnmount : fomponentWillUnmount,

    render : render,

    _parseData : f_parseData,
    _handleSelect : _handleSelect,

})

function getDefaultProps(){}
function getInitialState(){}
function componentWillMount(){}
function omponentWillReceiveProps(){}
function render(){}
function _parseData(){}
function _onSelect(){}
```


## <a name='handle_event_name'>Наименование обработчиков `handleEventName`</a>
- Начинайте имя хэндлера со слова `handle`. Дело в том, что стандартные обработчики внутри react именуются по правилу начиная с `on...`. Чтобы выделить собтвенные методы и не вызвать коллизий, лучше не использовать префикс `on` в именовании методов обработки событий.
- Именуйте обработчики по событию, которое они обрабатывают, а не по функции, которые они выполняют.

```javascript
// плохо
function render(){
  return select({onSelect: this._onSelect, onChange: this.changeHandler, onDrag: this.justDoIt}, []);
} 

function _onSelect(){
  alert('плоховато');
}

function changeHandler(){
  alert('тоже плохо, одни Handler');
}

function justDoIt(){
  alert('Это вообще ни в какие ворота не лезет');
}


// хорошо
function render(){
  return select({onSelect: this.handleSelect, onChange: this.handleChange, onDrag: this.handleDrag}, []);
} 

function handleSelect(){
  alert('выбрал хорошо');
}

function handleChange(){
  alert('и изменил хорошо');
}

function handleDrag(){
  alert('переместил тоже хорошо');
}

```

## <a name='jsx_or_not_jsx'>JSX и шаблонизация</a>
- Старайтесь использовать нативный javascript для шаблонизации вместо JSX нотации. Любой ваш js файл будет валидным и никакие дополнительные обработки не понадобятся, чтобы запустить его. К тому же это не сильно усложняет верстку.

```javascript
// плохо
return (
        <div>
            <h1>hello world</h1>
        </div>
    );


// хорошо
return div(null, 
            h1(null, 'hello world')
          );

``` 

- Не пишите длинные конструкции в `return`. В начале метода `render` можно создать несколько переменных и далее уже их содержимое перечислять в `return` словно конструктор. Это разделит описательную и исполнительную часть.
```javascript
// плохо
function render(){
  return div(null, [this.data.map(function(elem){
        return h1(null, elem);
      }), this.digits.map(function(digit){
        return span(digit);
      }),
      select(null, this.options.map(option){
        return option(null, option.title);
      }),
      span(null, 'the end');
  ]);
}

// хорошо
function render(){
  var headers, options, digits, footer;
  headers = this.data.map(function(elem){
        return h1(null, elem);
      });
  options = select(null, this.options.map(option){
        return option(null, option.title);
      });
  digits = this.digits.map(function(digit){
        return span(digit);
      });
  footer = span(null, 'the end');

  return div(null, [
    headers,
    options,
    digits,
    footer
  ]);
}

``` 
