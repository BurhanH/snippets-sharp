# Random .Net 8

## Shuffle

```c-sharp
int[] numbers = [1, 2, 3, 4];

Random.Shared.Shuffle(numbers.AsSpan());
```

## Random collection

```c-sharp
int[] numbers = [0, 1, 3, 4, 5, 6, 7, 8, 9];

var rndNumbers = Random.Shared.GetItems(numbers, length:50);
```
