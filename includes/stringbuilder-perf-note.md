---
ms.openlocfilehash: 903ac4ecb57e3a8e02a4f65ecfa6f9e77a552f45
ms.sourcegitcommit: 1bb00d2f4343e73ae8d58668f02297a3cf10a4c1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63872204"
---
Индексирование на основе символов со свойством <xref:System.Text.StringBuilder.Chars%2A> может работать очень медленно при следующих условиях:

- Экземпляр <xref:System.Text.StringBuilder> очень большой (например, состоит из нескольких десятков тысяч символов).
- <xref:System.Text.StringBuilder> имеет блоки. То есть повторные вызовы методов, например <xref:System.Text.StringBuilder.Append%2A?displayProperty=nameWithType>, автоматически расширили свойство <xref:System.Text.StringBuilder.Capacity%2A?displayProperty=nameWithType> объекта и выделили для него новые блоки памяти.

Это значительно влияет на производительность, поскольку при каждом доступе к символу проходится весь связанный список блоков с целью найти правильный буфер для индексации.

> [!NOTE]
>  Даже когда большой объект <xref:System.Text.StringBuilder> с блоками использует свойство <xref:System.Text.StringBuilder.Chars%2A> для доступа на основе индекса к одному символу или небольшому количеству символов, это оказывает незначительное влияние на производительность. Как правило, это операция **0(n)** . Производительность серьезно снижается во время итерации символов в объекте <xref:System.Text.StringBuilder> — операция **O(n^2)** . 

Если возникают проблемы с производительностью при использовании символьного индексирования с объектами <xref:System.Text.StringBuilder>, попробуйте выполнить одно из следующих действий:

- Преобразуйте экземпляр <xref:System.Text.StringBuilder> в <xref:System.String> путем вызова метода <xref:System.Text.StringBuilder.ToString%2A>, а затем получите доступ к символам в строке.

- Скопируйте содержимое существующего объекта <xref:System.Text.StringBuilder> в новый объект <xref:System.Text.StringBuilder> с заданным размером. Производительность повышается, так как новый объект <xref:System.Text.StringBuilder> не содержит блоков. Например:

   ```csharp
   // sbOriginal is the existing StringBuilder object
   var sbNew = new StringBuilder(sbOriginal.ToString(), sbOriginal.Length);
   ```
   ```vb
   ' sbOriginal is the existing StringBuilder object
   Dim sbNew = New StringBuilder(sbOriginal.ToString(), sbOriginal.Length)
   ```
- Установите для начальной вместимости объекта <xref:System.Text.StringBuilder> значение, примерно равное максимальному ожидаемому размеру, путем вызова конструктора <xref:System.Text.StringBuilder.%23ctor(System.Int32)>. Имейте в виду, что будет выделен целый блок памяти, даже если <xref:System.Text.StringBuilder> редко достигает своего максимального размера.
