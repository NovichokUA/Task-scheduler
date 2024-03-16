# React + Vite

This template provides a minimal setup to get React working in Vite with HMR and some ESLint rules.

Currently, two official plugins are available:

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react/README.md) uses [Babel](https://babeljs.io/) for Fast Refresh
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react-swc) uses [SWC](https://swc.rs/) for Fast Refresh

стор

createStore(reducer, preloadedState, enhancer)

**_reducer_** - функція із логікою зміни стану Redux. **Обов'язковий параметр.**
**_preloadedState_** - початковий стан програми. Це має бути об'єкт тієї ж форми, що й, як мінімум, частина стану. Необов'язковий параметр.
**_enhancer_** - функція розширення можливостей стору. Необов'язковий параметр.

Після створення стору необхідно зв'язати його з компонентами React, щоб вони могли отримувати доступ до стору та його методів. Для цього у бібліотеці React Redux є компонент **_Provider_**, котрий чекає однойменний пропс store. Для того щоб будь-який компонент у додатку міг використовувати стор, обертаємо Provider все дерево компонентів.

import React from 'react';
import ReactDOM from 'react-dom/client';
import { App } from './components/App';
import { store } from "./redux/store";

ReactDOM.createRoot(document.getElementById('root')).render(
<React.StrictMode>
<Provider store={store}>
<App />
</Provider>
</React.StrictMode>
);

Далі встановлюємо бібліотеку, яка дозволить ініціалізувати логіку Redux DevTools та зв'язати її з розширенням в інструментах розробника.

**_npm install @redux-devtools/extension_**

**_Підписка на стор_**

Щоб отримати дані зі стору, компоненти повинні підписатися на необхідні їм частини стану Redux. Для цього у бібліотеці React Redux є хук useSelector(selector). Аргументом він приймає функцію, яка оголошує один параметр state - весь об'єкт стану Redux, який буде автоматично переданий функції хуком useSelector. Ця функція називається селектором і повинна повернути тільки ту частину стану, яка необхідна компоненту.

**_Екшени_** - це об'єкти, які передають дані з компонентів у стор, тим самим сигналізуючи про те, яка подія сталася в інтерфейсі. Вони являються єдиним джерелом інформації для стору.

const action = {
type: "Action type",
payload: "Payload value",
};

Екшени повинні мати обов'язкову властивість type - рядок який описує тип події в інтерфейсі. Крім властивості type структура об'єкта може бути довільною, проте, дані зазвичай передають у необов'язковій властивості payload. Даними екшену може бути будь-яке значення крім функцій та класів.

**_Відправлення екшенів_**

Для того щоб сповістити сторінку про те, що в інтерфейсі відбулася якась подія, необхідно відправити екшен. Для цього у бібліотеці React Redux є хук useDispatch(), який повертає посилання на функцію надсилання екшенів dispatch з об'єкта створеного нами раніше стора Redux.

// Імпортуємо хук
import { useDispatch } from "react-redux";

const MyComponent = () => {
// Отримуємо посилання на функцію відправки екшенів
const dispatch = useDispatch();
};

**_Редюсер (reducer) _**- це функція, яка приймає поточний стан та екшен як аргументи і повертає новий стан. Редюсер визначає, як змінюється стан програми у відповідь на екшени, надіслані на стор. Пам'ятайте, що екшени описують тільки те, що сталося, а не як змінюється стан програми.

(state, action) => nextState

**_Кореневий редюсер_**

У додатку завжди буде лише один кореневий редюсер, який потрібно передати до createStore під час створення стора. Цей редюсер відповідає за обробку всіх відправлених екшенів та обчислення нового стану.
