<p align="center">
	<img src="https://raw.githubusercontent.com/EdsonBueno/infinite_scroll_pagination/master/assets/logo.png" alt="Package Logo with Flutter Favorite Badge" />
</p>
<p align="center">
	<i>Chosen as a <a href="https://flutter.dev/docs/development/packages-and-plugins/favorites" rel="noopener" target="_blank">Flutter Favorite</a> by the Flutter Ecosystem Committee</i>
</p>
<p align="center">
	<a href="https://pub.dev/packages/infinite_scroll_pagination" rel="noopener" target="_blank"><img src="https://img.shields.io/pub/v/infinite_scroll_pagination.svg" alt="Pub.dev Badge"></a>
	<a href="https://github.com/EdsonBueno/infinite_scroll_pagination/actions" rel="noopener" target="_blank"><img src="https://github.com/EdsonBueno/infinite_scroll_pagination/workflows/build/badge.svg" alt="GitHub Build Badge"></a>
	<a href="https://codecov.io/gh/EdsonBueno/infinite_scroll_pagination" rel="noopener" target="_blank"><img src="https://codecov.io/gh/EdsonBueno/infinite_scroll_pagination/branch/master/graph/badge.svg?token=B0CT995PHU" alt="Code Coverage Badge"></a>
	<a href="https://gitter.im/infinite_scroll_pagination/community" rel="noopener" target="_blank"><img src="https://badges.gitter.im/infinite_scroll_pagination/community.svg" alt="Gitter Badge"></a>
	<a href="https://github.com/tenhobi/effective_dart" rel="noopener" target="_blank"><img src="https://img.shields.io/badge/style-effective_dart-40c4ff.svg" alt="Effective Dart Badge"></a>
	<a href="https://opensource.org/licenses/MIT" rel="noopener" target="_blank"><img src="https://img.shields.io/badge/license-MIT-purple.svg" alt="MIT License Badge"></a>
	<a href="https://github.com/EdsonBueno/infinite_scroll_pagination" rel="noopener" target="_blank"><img src="https://img.shields.io/badge/platform-flutter-ff69b4.svg" alt="Flutter Platform Badge"></a>
</p>

---

# Infinite Scroll Pagination

Unopinionated, extensible and highly customizable package to help you lazily load and display small chunks of items as the user scrolls down the screen – known as infinite scrolling pagination, endless scrolling pagination, auto-pagination, lazy loading pagination, progressive loading pagination, etc.

Designed to feel like part of the Flutter framework.

<img src="https://raw.githubusercontent.com/EdsonBueno/infinite_scroll_pagination/master/assets/demo.gif" alt="Example Project" />

## Tutorial

[By raywenderlich.com (step-by-step, hands-on, in-depth, and illustrated)](https://www.raywenderlich.com/14214369-infinite-scrolling-pagination-in-flutter).

## Usage

```dart
class ListViewScreen extends StatefulWidget {
  const ListViewScreen({super.key});

  @override
  State<ListViewScreen> createState() => _ListViewScreenState();
}

class _ListViewScreenState extends State<ListViewScreen> {
  late final _pagingController = PagingController<int, Photo>(
    getNextPageKey: (state) => state.lastPageIsEmpty ? null : state.nextIntPageKey,
    fetchPage: (pageKey) => RemoteApi.getPhotos(pageKey),
  );

  @override
  void dispose() {
    _pagingController.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) => PagingListener(
    controller: _pagingController,
    builder: (context, state, fetchNextPage) => PagedListView<int, Photo>(
      state: state,
      fetchNextPage: fetchNextPage,
      builderDelegate: PagedChildBuilderDelegate(
        itemBuilder: (context, item, index) => ImageListTile(item: item),
      ),
    ),
  );
}
```

For more usage examples, please take a look at our [cookbook](https://pub.dev/packages/infinite_scroll_pagination/example) or check out the [example project](https://github.com/EdsonBueno/infinite_scroll_pagination/tree/master/example).

## Features

- **Architecture-agnostic**: Works with any state management approach, from [setState](https://flutter.dev/docs/development/data-and-backend/state-mgmt/options#setstate) to [BLoC](https://flutter.dev/docs/development/data-and-backend/state-mgmt/options#bloc--rx). Not even [Future](https://api.flutter.dev/flutter/dart-async/Future-class.html) usage is assumed.

- **Layout-agnostic**: Out-of-the-box widgets corresponding to [GridView](https://pub.dev/documentation/infinite_scroll_pagination/latest/infinite_scroll_pagination/PagedGridView-class.html), [SliverGrid](https://pub.dev/documentation/infinite_scroll_pagination/latest/infinite_scroll_pagination/PagedSliverGrid-class.html), [ListView](https://pub.dev/documentation/infinite_scroll_pagination/latest/infinite_scroll_pagination/PagedListView-class.html) and [SliverList](https://pub.dev/documentation/infinite_scroll_pagination/latest/infinite_scroll_pagination/PagedSliverList-class.html) – including `.separated` constructors. Not enough? You can [easily create a custom layout](https://pub.dev/packages/infinite_scroll_pagination/example#custom-layout).

- **API-agnostic**: By letting you in complete charge of your API calls, **Infinite Scroll Pagination** works with [any pagination strategy](https://nordicapis.com/everything-you-need-to-know-about-api-pagination/).

- **Highly customizable**: [You can change everything](https://pub.dev/packages/infinite_scroll_pagination/example#customizing-indicators). Provide your own progress, error and empty list indicators. Too lazy to change? The defaults will cover you.

- **Extensible**: Seamless integration with [pull-to-refresh](https://pub.dev/packages/infinite_scroll_pagination/example#pull-to-refresh), [searching, filtering and sorting](https://pub.dev/packages/infinite_scroll_pagination/example#searchingfilteringsorting).

- **Listen to state changes**: In addition to displaying widgets to inform the current status, such as progress and error indicators, you can also [use a listener](https://pub.dev/packages/infinite_scroll_pagination/example#listening-to-status-changes) to display dialogs/snackbars/toasts or execute any other action.

## Migration

if you are upgrading the package, please check the [migration guide](https://github.com/EdsonBueno/infinite_scroll_pagination/tree/master/MIGRATION.md) for instructions on how to update your code.

## API Overview

<p align="center">
	<img src="https://raw.githubusercontent.com/EdsonBueno/infinite_scroll_pagination/master/assets/api-diagram.png" alt="API Diagram" />
</p>
