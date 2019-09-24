---
ms.openlocfilehash: 733bfb4740f3f274ba9ebb396749d313907d5fa6
ms.sourcegitcommit: 1bb00d2f4343e73ae8d58668f02297a3cf10a4c1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63870373"
---
Начиная с версии .NET Framework 4.7 этот метод выполняет проверку подлинности с помощью <xref:System.Security.Authentication.SslProtocols.None>, что позволяет операционной системе выбрать наилучший протокол для использования и блокирования протоколов, которые не являются безопасными. В .NET Framework 4.6 (и .NET Framework 4.5 с последними обновлениями безопасности) допустимы версии протокола TLS/SSL 1.0, 1.1 и 1.2 (если только вы не отключите надежное шифрование в реестре Windows).
