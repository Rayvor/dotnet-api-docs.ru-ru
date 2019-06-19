---
ms.openlocfilehash: 903ac4ecb57e3a8e02a4f65ecfa6f9e77a552f45
ms.sourcegitcommit: 1bb00d2f4343e73ae8d58668f02297a3cf10a4c1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63872204"
---
<span data-ttu-id="028a3-101">Индексирование на основе символов со свойством <xref:System.Text.StringBuilder.Chars%2A> может работать очень медленно при следующих условиях:</span><span class="sxs-lookup"><span data-stu-id="028a3-101">Using character-based indexing with the <xref:System.Text.StringBuilder.Chars%2A> property can be extremely slow under the following conditions:</span></span>

- <span data-ttu-id="028a3-102">Экземпляр <xref:System.Text.StringBuilder> очень большой (например, состоит из нескольких десятков тысяч символов).</span><span class="sxs-lookup"><span data-stu-id="028a3-102">The <xref:System.Text.StringBuilder> instance is large (for example, it consists of several tens of thousands of characters).</span></span>
- <span data-ttu-id="028a3-103"><xref:System.Text.StringBuilder> имеет блоки.</span><span class="sxs-lookup"><span data-stu-id="028a3-103">The <xref:System.Text.StringBuilder> is "chunky."</span></span> <span data-ttu-id="028a3-104">То есть повторные вызовы методов, например <xref:System.Text.StringBuilder.Append%2A?displayProperty=nameWithType>, автоматически расширили свойство <xref:System.Text.StringBuilder.Capacity%2A?displayProperty=nameWithType> объекта и выделили для него новые блоки памяти.</span><span class="sxs-lookup"><span data-stu-id="028a3-104">That is, repeated calls to methods such as <xref:System.Text.StringBuilder.Append%2A?displayProperty=nameWithType> have automatically expanded the object's <xref:System.Text.StringBuilder.Capacity%2A?displayProperty=nameWithType> property and allocated new chunks of memory to it.</span></span>

<span data-ttu-id="028a3-105">Это значительно влияет на производительность, поскольку при каждом доступе к символу проходится весь связанный список блоков с целью найти правильный буфер для индексации.</span><span class="sxs-lookup"><span data-stu-id="028a3-105">Performance is severely impacted because each character access walks the entire linked list of chunks to find the correct buffer to index into.</span></span>

> [!NOTE]
>  <span data-ttu-id="028a3-106">Даже когда большой объект <xref:System.Text.StringBuilder> с блоками использует свойство <xref:System.Text.StringBuilder.Chars%2A> для доступа на основе индекса к одному символу или небольшому количеству символов, это оказывает незначительное влияние на производительность. Как правило, это операция **0(n)** .</span><span class="sxs-lookup"><span data-stu-id="028a3-106">Even for a large "chunky" <xref:System.Text.StringBuilder> object, using the <xref:System.Text.StringBuilder.Chars%2A> property for index-based access to one or a small number of characters has a negligible performance impact; typically, it is an **0(n)** operation.</span></span> <span data-ttu-id="028a3-107">Производительность серьезно снижается во время итерации символов в объекте <xref:System.Text.StringBuilder> — операция **O(n^2)** .</span><span class="sxs-lookup"><span data-stu-id="028a3-107">The significant performance impact occurs when iterating the characters in the <xref:System.Text.StringBuilder> object, which is an **O(n^2)** operation.</span></span> 

<span data-ttu-id="028a3-108">Если возникают проблемы с производительностью при использовании символьного индексирования с объектами <xref:System.Text.StringBuilder>, попробуйте выполнить одно из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="028a3-108">If you encounter performance issues when using character-based indexing with <xref:System.Text.StringBuilder> objects, you can use any of the following workarounds:</span></span>

- <span data-ttu-id="028a3-109">Преобразуйте экземпляр <xref:System.Text.StringBuilder> в <xref:System.String> путем вызова метода <xref:System.Text.StringBuilder.ToString%2A>, а затем получите доступ к символам в строке.</span><span class="sxs-lookup"><span data-stu-id="028a3-109">Convert the <xref:System.Text.StringBuilder> instance to a <xref:System.String> by calling the <xref:System.Text.StringBuilder.ToString%2A> method, then access the characters in the string.</span></span>

- <span data-ttu-id="028a3-110">Скопируйте содержимое существующего объекта <xref:System.Text.StringBuilder> в новый объект <xref:System.Text.StringBuilder> с заданным размером.</span><span class="sxs-lookup"><span data-stu-id="028a3-110">Copy the contents of the existing <xref:System.Text.StringBuilder> object to a new pre-sized <xref:System.Text.StringBuilder> object.</span></span> <span data-ttu-id="028a3-111">Производительность повышается, так как новый объект <xref:System.Text.StringBuilder> не содержит блоков.</span><span class="sxs-lookup"><span data-stu-id="028a3-111">Performance improves because the new <xref:System.Text.StringBuilder> object is not chunky.</span></span> <span data-ttu-id="028a3-112">Например:</span><span class="sxs-lookup"><span data-stu-id="028a3-112">For example:</span></span>

   ```csharp
   // sbOriginal is the existing StringBuilder object
   var sbNew = new StringBuilder(sbOriginal.ToString(), sbOriginal.Length);
   ```
   ```vb
   ' sbOriginal is the existing StringBuilder object
   Dim sbNew = New StringBuilder(sbOriginal.ToString(), sbOriginal.Length)
   ```
- <span data-ttu-id="028a3-113">Установите для начальной вместимости объекта <xref:System.Text.StringBuilder> значение, примерно равное максимальному ожидаемому размеру, путем вызова конструктора <xref:System.Text.StringBuilder.%23ctor(System.Int32)>.</span><span class="sxs-lookup"><span data-stu-id="028a3-113">Set the initial capacity of the <xref:System.Text.StringBuilder> object to a value that is approximately equal to its maximum expected size by calling the <xref:System.Text.StringBuilder.%23ctor(System.Int32)> constructor.</span></span> <span data-ttu-id="028a3-114">Имейте в виду, что будет выделен целый блок памяти, даже если <xref:System.Text.StringBuilder> редко достигает своего максимального размера.</span><span class="sxs-lookup"><span data-stu-id="028a3-114">Note that this allocates the entire block of memory even if the <xref:System.Text.StringBuilder> rarely reaches its maximum capacity.</span></span>
