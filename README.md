# Задание 1. Вёрстка шаблонов Stories

В этом репозитории находятся материалы тестового задания «Шаблоны Stories» для [17-й Школы разработки интерфейсов](https://yandex.ru/promo/academy/shri) (лето-2021, Москва).

В тестовом задании вы будете работать над приложением, которое позволяет просмотреть информацию о работе команды над проектом в виде stories. Каждый слайд истории визуализирует небольшой объём информации при помощи одного из пяти шаблонов.

## Шаблоны

1. Лидеры спринта — позволяет увидеть участников команды, лидирующих в разных номинациях. Также используется для отображения результатов голосования.
2. Голосование за участника команды — выводит список участников команды постранично и позволяет проголосовать за участника в одной из номинаций.
3. Статистика по спринтам — визуализирует статистику текущего спринта по сравнению с предыдущими спринтами, например показывает количество коммитов в текущем и предыдущих спринтах.
4. Статистика внутри спринта — визуализирует статистику внутри спринта по качественным характеристикам, например размеру коммитов в спринте, и разницу с предыдущим спринтом.
5. Активность участников — визуализирует активность команды в виде тепловой карты по дням и часам.

## Задание

В первом задании необходимо сверстать шаблоны по [макетам](https://www.figma.com/file/0HYYteSLpxex9QeAka6JGr/IDC-2021-test-work?node-id=138%3A1981). В макетах представлена вертикальная ориентация, адаптированная горизонтальная версия и светлая тема приложения. На отдельный арт-борд вынесены [спецификации к макетам](https://www.figma.com/file/0HYYteSLpxex9QeAka6JGr/IDC-2021-test-work?node-id=711%3A12033). Данные для шаблонов представлены в файле `data.json` в каталоге `data`, [описание формата](/data).

Шаблоны должны отображаться на весь экран и соответствовать макетам в представленном размере. Стили, например тени и скругления в шаблоне с круговой диаграммой, могут отличаться от макета. Полное соответствие круговой диаграммы макетам считается дополнительным заданием.

Ваш код должен формировать HTML-разметку шаблонов и содержать функцию шаблонизации `renderTemplate`, которая принимает два параметра: строку с алиасом шаблона `alias` и данные для шаблона `data`. Ожидаемый результат функции `renderTemplate` — строка с HTML-разметкой слайда.

Тема приложения устанавливается при помощи добавления класса `theme_dark` или `theme_light` на родительский элемент, который содержит HTML-разметку, сформированную функцией `renderTemplate`. Например, на тег `body` может быть установлен класс `theme_light`. Если класс темы не задан, по умолчанию шаблон должен отображаться в тёмной теме.

Приложение должно запускаться на локальном хосте командой `npm start` и быть доступным по адресу http://localhost:8080, при переходе по которому в браузере должен отобразиться слайд с индексом 0 из данных. Чтобы при проверке вашего задания мы могли переключаться между слайдами и темой приложения, пожалуйста, добавьте поддержку дополнительных параметров адресной строки:
* `?slide=1` — переключение слайдов с 1 по 11, 1 соответствует индексу 0 в массиве слайдов в файле `data.json`;
* `&theme=light` — тема, `light` или `dark`, без параметра шаблоны должны рендериться в тёмной теме.

## Интерактивность

В этом задании мы не просим реализовать интерактивность в приложении. Голосование и переключение между страницами в шаблоне голосования будет частью третьего задания. Однако мы ждём, что интерактивные элементы будут иметь состояния, соответствующие данным и действиям пользователя.

Для корректной работы интерактивности в третьем задании необходимо правильно разметить атрибуты `data-action` и `data-params` интерактивных элементов. В них будет содержаться информация о действии, которое нужно совершить, если нажать этот элемент. В атрибут `data-action` необходимо установить событие `update`. В атрибут `data-params` необходимо установить сериализованный объект с данными события, в следующем виде:

```
// Событие выбора участника в шаблоне голосования
{
  alias: 'leaders',          // Подставить 'leaders', в этом шаблоне мы отобразим результаты голосования
  data: {
    selectedUserId: 1        // Подставить ID выбранного пользователя
  }
}
```

```
// Событие переключения страницы на предыдущую или следующую в шаблоне голосования
{
  alias: 'vote',             // Подставить 'vote', в этом шаблоне мы отобразим следующую страницу 
  data: {
    offset: 10               // Подставить индекс пользователя, с которого должна начинаться страница
  }
}
```

## Критерии

Мы ожидаем, что вёрстка будет соответствовать макетам в представленном размере. Могут быть незначительные отличия, важно, чтобы вёрстка проходила наши автоматизированные тесты. Приложение должно корректно работать в последних версиях Chrome, Mozilla Firefox, iOS, Android. Также используйте шрифт, приложенный в репозитории.

Макеты представлены в размере 376 × 668, размер iPhone 8 + 1 px. Мы добавили 1 px, чтобы избежать неточностей из-за нечётного количества пикселей. Это позволит вам точно видеть отступы по правому и левому краю. При разработке не забудьте добавить пользовательский размер экрана в средствах разработчика. Также для удобства работы с макетами вы можете отключить мультикурсор в приложении figma.

Мы не задаём фиксированного поведения адаптивности, в спецификации указаны только некоторые характеристики. Мы ожидаем, что макеты при этом отобразятся корректно и на экранах устройств других размеров, а контент будет удобен для пользователя.

При проверке вашего задания мы также будем смотреть вёрстку на размерах 320 × 568, 414 × 736, 768 × 1024 в вертикальной и горизонтальной ориентации и 1366 × 768, 1920 × 1080 в горизонтальной ориентации. Адаптированный интерфейс под десктопное разрешение позволит выводить наши stories на большие экраны, например телевизоры. 

Мы не ограничиваем вас в использовании сторонних инструментов и библиотек, но ждём комментария — что и зачем вы использовали. Опишите в файле `README.md` ход ваших мыслей при выборе, любые другие важные детали о выбранных способах решения. Также, пожалуйста, уделите внимание организации и оформлению кода.

## Выполнение задания

В качестве результата выполнения задания укажите ссылку на репозиторий c исходным кодом и собранными файлами. Обратите внимание: сделайте репозиторий приватным, чтобы другие кандидаты не могли скопировать ваш код. Приложение должно запускаться на локальном хосте командой `npm start` и поддерживать адреса, перечисленные в разделе «Задание». В корне репозитория должен находиться каталог `build` с собранными файлами `stories.css`, `stories.js`, необходимыми изображениями и шрифтами. Размер каждого файла — не более 1 МБ. Собранные версии файлов не должны требовать установки дополнительных зависимостей.
* `stories.css` — содержит стили для всех элементов;
* `stories.js` — содержит код формирования HTML-разметки для шаблонов и функцию шаблонизации `renderTemplate`, которая должна быть доступна глобально, чтобы её можно было подключить в третьем задании. 

