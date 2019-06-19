---
ms.openlocfilehash: 92b3aa8ebf6a4c0d6968287fd09d84d4415d47f5
ms.sourcegitcommit: 1bb00d2f4343e73ae8d58668f02297a3cf10a4c1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "63872740"
---
> [!NOTE]
> <span data-ttu-id="bcc3d-101">**Выполнение .NET Core в только в системах Linux и macOS:** При использовании параметров сортировки для языков и региональных параметров C и Posix всегда учитывается регистр, так как в этом случае Юникод не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="bcc3d-101">**.NET Core running on Linux and macOS systems only:** The collation behavior for the C and Posix cultures is always case-sensitive because these cultures do not use the expected Unicode collation order.</span></span> <span data-ttu-id="bcc3d-102">Мы не рекомендуем использовать язык и региональные параметры, выбранные для C или Posix, для выполнения операций сортировки с учетом языка и региональных параметров, но без учета регистра.</span><span class="sxs-lookup"><span data-stu-id="bcc3d-102">We recommend that you use a culture other than C or Posix for performing culture-sensitive, case-insensitive sorting operations.</span></span>  
