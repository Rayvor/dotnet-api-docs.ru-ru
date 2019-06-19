---
ms.openlocfilehash: 733bfb4740f3f274ba9ebb396749d313907d5fa6
ms.sourcegitcommit: 1bb00d2f4343e73ae8d58668f02297a3cf10a4c1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63870373"
---
<span data-ttu-id="42fd0-101">Начиная с версии .NET Framework 4.7 этот метод выполняет проверку подлинности с помощью <xref:System.Security.Authentication.SslProtocols.None>, что позволяет операционной системе выбрать наилучший протокол для использования и блокирования протоколов, которые не являются безопасными.</span><span class="sxs-lookup"><span data-stu-id="42fd0-101">Starting with .NET Framework 4.7, this method authenticates using <xref:System.Security.Authentication.SslProtocols.None>, which allows the operating system to choose the best protocol to use, and to block protocols that are not secure.</span></span> <span data-ttu-id="42fd0-102">В .NET Framework 4.6 (и .NET Framework 4.5 с последними обновлениями безопасности) допустимы версии протокола TLS/SSL 1.0, 1.1 и 1.2 (если только вы не отключите надежное шифрование в реестре Windows).</span><span class="sxs-lookup"><span data-stu-id="42fd0-102">In .NET Framework 4.6 (and .NET Framework 4.5 with the latest security patches installed), the allowed TLS/SSL protocols versions are 1.2, 1.1, and 1.0 (unless you disable strong cryptography by editing the Windows Registry).</span></span>
