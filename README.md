
## Оглавление

  1. [Основные правила](#basic-rules)
  1. [Component против PureComponent против компонента без состояния (stateless)](#component-vs-purecomponent-vs-stateless)
  1. [Именование](#naming)
  1. [Выравнивание](#alignment)
  1. [Кавычки](#quotes)
  1. [Пробелы](#spacing)
  1. [Свойства (Props)](#props)
  1. [Ссылки (Refs)](#refs)
  1. [Круглые скобки](#parentheses)
  1. [Теги](#tags)
  1. [Методы](#methods)
  1. [Последовательность](#ordering)

## <a name="basic-rules">Основные правила</a>

  - Включайте только один React компонент в файл.
    - Однако, разрешается несколько компонентов без состояний или PureComponent в файле.
  - Всегда используйте JSX синтаксис.

## <a name="#component-vs-purecomponent-vs-stateless">Component против PureComponent против компонента без состояния (stateless)</a>

  - Если у вас нет состояния (`state`) или ссылок (`refs`), но есть вспомогательные методы,
  отдавайте предпочтение PureComponent:

    ```tsx
    // плохо
    class Listing extends React.Component {
      conponentDidMount() {
        console.log(this.props.hello);
      }
      render() {
        return <Text>{this.props.hello}</Text>;
      }
    }

    // хорошо
    class Listing extends React.PureComponent {
      conponentDidMount() {
        console.log(this.props.hello);
      }
      render() {
        return <Text>{this.props.hello}</Text>;
      }
    }
    ```

  - Если у вас нет состояния (`state`) или ссылок (`refs`) и вспомогательных методов,
  отдавайте предпочтение функциям над классами:

    ```tsx
    // плохо
    class Listing extends React.Component {
      render() {
        return <Text>{this.props.hello}</Text>;
      }
    }

      // плохо
    class Listing extends React.PureComponent {
      render() {
        return <Text>{this.props.hello}</Text>;
      }
    }

    // хорошо
    const Listing = ({ hello }) => (
      <Text>{hello}</Text>
    );
    ```

## <a name="naming">Именование</a>

  - **Расширения**: Используйте расширение `.tsx` для компонентов React.
  - **Имя файла**: Используйте `PascalCase` для названий файлов с компонентов React, например, `ReservationCard.tsx`. Используйте `kebab-case` для названий файлов без компонентов React.
  - **Имя папки**: Используйте `snake_case` для назваинй папок.
  - **Именование переменной**: Используйте `PascalCase` для компонентов React и `camelCase` для их экземпляров. eslint: [`react/jsx-pascal-case`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-pascal-case.md)

    ```tsx
    // плохо
    import reservationCard from './ReservationCard';

    // хорошо
    import ReservationCard from './ReservationCard';

    // плохо
    const ReservationItem = <ReservationCard />;

    // хорошо
    const reservationItem = <ReservationCard />;
    ```

  - **Именование компонента**: Называйте файлы так же как и компоненты. Например, `ReservationCard.tsx` должен содержать внутри компонент `ReservationCard`.
  - **Названия свойств**: Избегайте использования стандартных названий свойств компонента для других целей.

    > Почему? Люди ожидают, что такие свойства как `style` и `className` имеют одно определённое значение. Изменение этого API в вашем приложении ухудшает читабельность и поддержку кода, что может приводить к ошибкам.

    ```tsx
    // плохо
    <MyComponent style="fancy" />

    // плохо
    <MyComponent className="fancy" />

    // хорошо
    <MyComponent variant="fancy" />
    ```

## <a name="alignment">Выравнивание</a>

  - Следуйте приведённым ниже стилям для TSX-синтаксиса.

    ```tsx
    // плохо
    <Foo superLongParam="bar"
         anotherSuperLongParam="baz" />

    // хорошо
    <Foo
      superLongParam="bar"
      anotherSuperLongParam="baz"
    />

    // если свойства помещаются на одну строку, оставляйте их на одной строке
    <Foo bar="bar" />

    // отступ у дочерних элементов задается как обычно
    <Foo
      superLongParam="bar"
      anotherSuperLongParam="baz"
    >
      <Quux />
    </Foo>

    // плохо
    {showButton &&
      <Button />
    }

    // плохо
    {
      showButton &&
        <Button />
    }

    // хорошо
    {showButton && (
      <Button />
    )}

    // хорошо
    {showButton && <Button />}
    ```

## <a name="quotes">Кавычки</a>

  - Всегда используйте двойные кавычки (`"`) для TSX-атрибутов, а одинарные кавычки (`'`) для всего остального TS.

    > Почему? Для стандартных HTML-атрибутов обычно используются двойные кавычки, а не одинарные, и TSX-атрибуты тоже следуют этому соглашению.

    ```tsx
    // плохо
    <Foo bar='bar' />

    // хорошо
    <Foo bar="bar" />

    // хорошо
    <Foo bar={'bar'} />

    // плохо
    <Foo style={{ left: "20px" }} />

    // хорошо
    <Foo style={{ left: '20px' }} />
    ```

## <a name="spacing">Пробелы</a>

  - Всегда вставляйте один пробел в ваш самозакрывающийся тег.

    ```tsx
    // плохо
    <Foo/>

    // очень плохо
    <Foo                 />

    // плохо
    <Foo
     />

    // хорошо
    <Foo />
    ```

  - Не отделяйте фигурные скобки пробелами в JSX.

    ```tsx
    // плохо
    <Foo bar={ baz } />

    // хорошо
    <Foo bar={baz} />
    ```

## <a name="props">Свойства (Props)</a>

  - Всегда используйте `camelCase` для названий свойств.

    ```tsx
    // плохо
    <Foo
      UserName="hello"
      phone_number={12345678}
    />

    // хорошо
    <Foo
      userName="hello"
      phoneNumber={12345678}
    />
    ```

  - Не указывайте значение свойства, когда оно явно `true`.

    ```tsx
    // плохо
    <Foo
      hidden={true}
    />

    // хорошо
    <Foo
      hidden
    />

    // хорошо
    <Foo hidden />
    ```

  - Не используйте индексы элементов массива в качестве свойства `key`.
    > Почему? Неиспользование стабильного ID [является антипаттерном](https://medium.com/@robinpokorny/index-as-a-key-is-an-anti-pattern-e0349aece318), потому что это может негативно повлиять на производительность компонента и вызвать проблемы с его состоянием.

    Мы не рекомендуем использовать индексы для ключей, если порядок элементов может измениться.

    ```tsx
    // плохо
    {todos.map((todo, index) =>
      <Todo
        {...todo}
        key={index}
      />
    )}

    // хорошо
    {todos.map(todo => (
      <Todo
        {...todo}
        key={todo.id}
      />
    ))}
    ```

## <a name="refs">Ссылки (Refs)</a>

  - Всегда используйте функции обратного вызова.

    ```tsx
    // плохо
    <Foo
      ref="myRef"
    />

    // хорошо
    <Foo
      ref={(ref) => { this.myRef = ref; }}
    />
    ```

## <a name="parentheses">Круглые скобки</a>

  - Оборачивайте в скобки TSX теги, когда они занимают больше одной строки.

    ```jsx
    // плохо
    render() {
      return <MyComponent variant="long body" foo="bar">
               <MyChild />
             </MyComponent>;
    }

    // хорошо
    render() {
      return (
        <MyComponent variant="long body" foo="bar">
          <MyChild />
        </MyComponent>
      );
    }

    // хорошо, когда одна строка
    render() {
      const body = <View>hello</View>;
      return <MyComponent>{body}</MyComponent>;
    }
    ```

## <a name="tags">Теги</a>

  - Всегда используйте самозакрывающиеся теги, если у элемента нет дочерних элементов. eslint: [`react/self-closing-comp`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/self-closing-comp.md)

    ```tsx
    // плохо
    <Foo variant="stuff"></Foo>

    // хорошо
    <Foo variant="stuff" />
    ```

  - Если ваш компонент имеет множество свойств, которые располагаются на нескольких строчках, то закрывайте тег на новой строке.

    ```tsx
    // плохо
    <Foo
      bar="bar"
      baz="baz" />

    // хорошо
    <Foo
      bar="bar"
      baz="baz"
    />
    ```

## <a name="methods">Методы</a>

  - Используйте стрелочные функции для замыкания локальных переменных. Это удобно, когда вам нужно передать дополнительные данные в обработчик событий. Однако, убедитесь, что они не сильно вредят производительности. В частности, могут быть ненужные перерисовки каждый раз, когда они будут передаваться PureComponent.

    ```tsx
    const ItemList = (props) => {
      return (
        <View>
          {props.items.map((item, index) => (
            <Item
              key={item.key}
              onClick={(event) => { doSomethingWith(event, item.name, index); }}
            />
          ))}
        </View>
      );
    }
    ```

  - Привязывайте обработчики событий для метода `render` в конструкторе.

    > Почему? Вызов `bind` в методе `render` создаёт новую функцию при каждой перерисовке. Не используйте стрелочные функции в полях класса, поскольку это делает их сложными для тестирования и отладки, и может негативно повлиять на производительность. К тому же концептуально поля класса предназначены для данных, а не для логики.

    ```tsx
    // плохо
    class MyComponent extends React.Component {
      onClickDiv() {
        // ...
      }

      render() {
        return <Button onClick={this.onClickDiv.bind(this)} />;
      }
    }

    // очень плохо
    class MyComponent extends React.Component {
      onClickDiv = () => {
        // ...
      }
      render() {
        return <Button onClick={this.onClickDiv} />
      }
    }

    // хорошо
    class MyComponent extends React.Component {
      constructor(props) {
        super(props);

        this.onClickDiv = this.onClickDiv.bind(this);
      }

      onClickDiv() {
        // ...
      }

      render() {
        return <Button onClick={this.onClickDiv} />;
      }
    }
    ```

  - Не используйте префикс подчёркивания для именования внутренних методов React компонента.

    ```tsx
    // плохо
    React.createClass({
      _onClickSubmit() {
        // ...
      },

      // ...
    });

    // хорошо
    class extends React.Component {
      onClickSubmit() {
        // ...
      }

      // ...
    }
    ```

  - Всегда возвращайте значение в методах `render`.

    ```tsx
    // плохо
    render() {
      (<View />);
    }

    // хорошо
    render() {
      return (<View />);
    }
    ```

## <a name="ordering">Последовательность</a>

  - Последовательность для `class extends React.Component` и `class extends React.PureComponent`:

  1. произвольные `static` методы
  1. `constructor`
  1. `getChildContext`
  1. `componentWillMount`
  1. `componentDidMount`
  1. `componentWillReceiveProps`
  1. `shouldComponentUpdate`
  1. `componentWillUpdate`
  1. `componentDidUpdate`
  1. `componentWillUnmount`
  1. *обработчики кликов или событий*, такие как `onClickSubmit()` или `onChangeDescription()`
  1. *getter методы для `render`*, такие как `getSelectReason()` или `getFooterContent()`
  1. *произвольные render методы*, такие как `renderNavigation()` или `renderProfilePicture()`
  1. `render`

**[⬆ к оглавлению](#Оглавление)**
