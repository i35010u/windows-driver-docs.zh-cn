---
title: C28167
description: 警告 C28167 函数更改的 IRQL，并在退出之前不会还原 IRQL。 它应添加批注以反映此更改或 IRQL 应还原。
ms.assetid: 289bb3c9-f9b2-4e7f-a406-22e365e5316a
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28167
ms.openlocfilehash: 790a0e6c241e043c31994e6d4ed12dc3c30131fd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561961"
---
# <a name="c28167"></a>C28167


警告 C28167:该函数更改的 IRQL，并在退出之前不会还原 IRQL。 它应添加批注以反映此更改或 IRQL 应还原。

此警告指示下列条件为 true:

-   函数将更改的 IRQL 在其中运行驱动程序。

-   没有通过不会函数退出时，通过将 irql 恢复到原始的 IRQL 驱动程序运行在函数入口函数至少一个路径。

IRQL 在函数上的批注是必需的但不存在时，会出现此警告。

若要避免此警告，该驱动程序必须正确保存 IRQL 初始值并还原相同的 IRQL 值在函数退出时，如果它不想更改的 IRQL。

有意将 IRQL 更改为不同的驱动程序已运行位于函数入口 IRQL 值的函数应批注以指示此行为。 例如，可以使用 **\_IRQL\_引发\_**(*irql*) 批注以指示该函数从的 IRQL 更改的 IRQL 在函数调用了。 也可以保存和还原的 IRQL 值并应用相应批注 (**\_IRQL\_保存\_**，  **\_IRQL\_还原\_**). 批注将取消显示此警告。 有关详细信息，请参阅[驱动程序的 IRQL 批注](irql-annotations-for-drivers.md)。 应修复错误地更改的 IRQL 的函数。

 

 





