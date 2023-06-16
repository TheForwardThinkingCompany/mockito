# Mockito

Contains FT's changes on Mockito:
- Fixed code generation on bound generic argument types.

> Example of breaking code: 
>```dart
>abstract class Worker<T1 extends Worker<T1>> {
>  const Worker();
>}
>
>mixin Workers {
>  // Mock of this suppose to break the generator because of
>  // T1 extends Worker<T1> 
>  void someWork<T1 extends Worker<T1>>() {
>    print('Work on: $T1');
>  }
>}
>
>abstract class Bar<T1 extends Bar<T1>> with Workers {}
>
>class BackgroundWorker extends Worker<BackgroundWorker> {}
>
>class Foo extends Bar<Foo> {
>  void doWork() {
>    someWork<BackgroundWorker>();
>  }
>}
>```

Fork of: https://github.com/dart-lang/mockito/