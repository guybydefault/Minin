# Автор
Минин Александр
# Описание работы

Приложение реализовал на базе Model-View-ViewModel паттерна.
Все GIF загружаются с раздела TOP (/top/{page}?json=true).
GIF отображаются по центру экрана. Под GIF находятся кнопки prev/next. Когда пользователь находится на самой первой GIF, кнопка prev отключена (clickable = false).

При нажатии кнопки next/prev отображается ProgressBar, который может находиться в двух состояниях: loading image info (во время выполнения запроса к API на получение GIF URL и метаинформации о GIF) и downloading GIF (во время непосредственной загрузки изображения). После успешного завершения этих состояний GIF отображается на экране пользователя.

В работе использовал: 
1) Kotlin
2) Coroutines для асинхронных запросов, чтобы предотвратить фризы UI, и избежать нагромождений из коллбэков. Все корутины привязаны к жизненному циклу ViewModel (запускаются с viewModelScope).
3) Retrofit2 для доступа к API (RxJava2CallAdapterFactory для работы с корутинами, GsonConverter для десериализации из JSON)
4) Glide для загрузки и кэширования изображений (использую DiskCacheStrategy.DATA - сохраняю все изображения в оригинале локально, поэтому при внезапном отключении интернета все еще можно свайпать изображения, которые уже были загружены ранее)

# Что еще нужно сделать

В силу того, что время ограничено (тороплюсь на поезд =D), с корутинами я работал впервые, не успел сделать все, что хотел:
1) Более детализированные сообщения об ошибках (отсутствие интернета, связи с хостом, ошибках сервера и др.). В данный момент вся обработка ошибок заключается в отображении Toast с общим для всех ошибок текстом ошибки.
2) Верстку макета в хорошем качестве
3) Отображение Gif с разных разделов сайта
4) Unit-тесты
5) Анимация

# Демонстрация работы приложения
![Демо](Demo.gif)
