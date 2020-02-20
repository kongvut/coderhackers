---
title: Step12 MultiProvider
---

## Goal of this step
- Learn MultiProvider

In this step, in addition to provide **testProviderText**, let's provide **isAuthenticated** state.

To provide multiple value, we need to use: **MultiProvider**
https://pub.dev/packages/provider#multiprovider

#### `lib/main.dart`
```dart {2-6}
Widget build(BuildContext context) {
	return  MultiProvider(
		providers: [
			Provider<String>(create: (context) => testProviderText),
			Provider<bool>(create: (context) => isAuthenticated)
		],
		child: MaterialApp(
			title: 'Flutter Demo',
			theme: ThemeData(
				primarySwatch: Colors.blue,
			),
			initialRoute: '/',
			routes: {
				// When navigating to the "/" route, build the FirstScreen widget.
				'/': (context) => HomePage(isAuthenticated: isAuthenticated),
				'/sign_up': (context) => RegisterPage(),
			},
		),
	);
}
```

## Consume **isAuthenticated** param by using `Provider.of`
### Edit HomePage
#### `lib/pages/home_page.dart`
```dart {1,3}
final bool isAuthenticated = Provider.of<bool>(context);
...
isAuthenticated ? Text('Home Page after login') : Text('Home Page before login')
```

Delete passed props in `main.dart`.
#### `main.dart`
```dart {3}
routes: {
	// When navigating to the "/" route, build the FirstScreen widget.
	'/': (context) => HomePage(),
	'/sign_up': (context) => RegisterPage(),
},
```

### Edit HomeDrawer
#### `lib/widgets/home_drawer.dart`
```dart {6}
...

class HomeDrawer extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
		final bool isAuthenticated = Provider.of<bool>(context);
		...
```

Delete passed props in `lib/pages/home_page.dart`.
#### `lib/pages/home_page.dart`
```dart
...
drawer: HomeDrawer(),
```

## Test it
- Check it works correctly by "sign-in", "sign-out".