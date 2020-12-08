---
title: C28167
description: 警告 C28167 函数会更改 IRQL，不会在其退出之前还原 IRQL。 应对其进行批注，以反映更改或应还原 IRQL。
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28167
ms.openlocfilehash: 4e50c64093435c40cfc6281c76dd731dd3f7b042
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838161"
---
# <a name="c28167"></a>C28167


警告 C28167：该函数更改 IRQL，不会在其退出之前还原 IRQL。 应对其进行批注，以反映更改或应还原 IRQL。

此警告意味着满足以下条件：

-   函数会更改驱动程序运行时的 IRQL。

-   函数退出时，至少有一个通过函数的路径，将 IRQL 还原到在函数入口运行的原始 IRQL。

当需要函数上的 IRQL 批注，但一个不存在时，会出现此警告。

若要避免此警告，驱动程序必须正确保存初始 IRQL 值，并在函数退出时还原相同的 IRQL 值（如果它不打算更改 IRQL）。

应该对将 IRQL 更改为不同于在函数项中运行驱动程序的 IRQL 值的函数进行批注，以指示这种行为。 例如，您可以使用 **\_ irql \_ 引发 \_** (*irql*) 批注，以指示函数从调用函数的 irql 更改 irql。 你还可以保存和还原 irql 值，并应用相应的批注 (**\_ irql \_ 保存 \_**， **\_ irql \_) \_ 还原**。 批注将禁止显示此警告。 有关详细信息，请参阅 [用于驱动程序的 IRQL 注释](irql-annotations-for-drivers.md)。 应修复按错误更改 IRQL 的函数。

 

 





