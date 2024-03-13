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
