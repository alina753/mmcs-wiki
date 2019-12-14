## PascalABC.NET
 PascalABC.NET — язык программирования Паскаль нового поколения, включающий классический Паскаль, большинство возможностей языка [Delphi](https://ru.wikipedia.org/wiki/Delphi_(язык_программирования)), а также ряд собственных расширений. Он реализован на платформе [Microsoft.NET](https://ru.wikipedia.org/wiki/.NET_Framework) и содержит все современные языковые средства: классы, перегрузку операций, интерфейсы, обработку исключений, обобщенные классы и подпрограммы, сборку мусора, лямбда-выражения, средства параллельного программирования.

PascalABC.NET является мультипарадигменным языком: на нём можно программировать в [структурном](https://ru.wikipedia.org/wiki/Структурное_программирование), [объектно-ориентированном](https://ru.wikipedia.org/wiki/Объектно-ориентированное_программирование) и [функциональном стилях](https://ru.wikipedia.org/wiki/Функциональное_программирование).

##### PascalABC.NET - компилируемый язык.
Это позволяет достичь высокой скорости выполнения программ.
Сравним скрость выполнения программы на Python и PascalABC.NET:

`parallel.py`
```
from multiprocessing import Pool, cpu_count
from datetime import datetime


def isprime(x):
    for i in range(2, x):
        if not x % i:
            return False
    return True


if __name__ == '__main__':
    start = datetime.now()
    pool = Pool(cpu_count())
    r = pool.map(isprime, range(2, 40000)).count(True)
    pool.close()
    pool.join()
    print(r)
    stop = datetime.now()
    print(f'{(stop - start).total_seconds() * 1000:.3f} ms')

```

`parallel.pas`
```
function isprime(x: integer): boolean;
begin
  result := True;
  for var i := 2 to x-1 do
    if x mod i = 0 then
      begin
      result := False;
      exit;
      end;
end;
begin
  Range(2, 40000).AsParallel.Where(x -> isprime(x)).Count.Println;
  MillisecondsDelta.Print;
end.
```
##### Результаты бенчмарков:
`Cpython 3.7 - 2008.091 ms`

`PascalABC.NET - 331 ms`
##### Однако:
`Pypy3 - 623.356 ms`
