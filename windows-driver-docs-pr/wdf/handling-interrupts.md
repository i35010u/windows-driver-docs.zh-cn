---
title: 处理中断在 UMDF 驱动程序
description: 处理中断
ms.assetid: 5C8CB68A-EAE6-4AF9-8B10-F8B73B50DEB2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0297939bbc09e62fdfb219e3b079fb3548b18c5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68229648"
---
# <a name="handling-interrupts-in-umdf-drivers"></a>处理中断在 UMDF 驱动程序


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

从版本 1.11 UMDF，UMDF 驱动程序可以处理硬件中断。 UMDF 支持基于行的 （级别触发和边缘触发） 和消息告知 (MSI) 中断。

从 Windows 8 开始，提供基于行的级别触发中断。 MSI 和基于行的边缘触发中断 UMDF 1.11 支持的所有操作系统上可用。

基于框架的驱动程序通过使用 framework 中断对象管理硬件中断。

## <a name="in-this-section"></a>本节内容


-   [创建一个中断对象](creating-an-interrupt-object-umdf.md)
-   [启用和禁用中断](enabling-and-disabling-interrupts-umdf.md)
-   [服务中断](servicing-an-interrupt-umdf.md)
-   [使用工作项](using-workitems.md)
-   [同步中断代码](synchronizing-interrupt-code-umdf.md)
-   [删除中断对象](deleting-an-interrupt-object.md)

 

 





