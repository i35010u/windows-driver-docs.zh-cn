---
title: 处理 UMDF 驱动程序中的中断
description: 处理中断
ms.assetid: 5C8CB68A-EAE6-4AF9-8B10-F8B73B50DEB2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a50ceb50c4efb3d224a49c6aeebc498d0c7f08da
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209927"
---
# <a name="handling-interrupts-in-umdf-drivers"></a>处理 UMDF 驱动程序中的中断


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

从 UMDF 版本1.11 开始，UMDF 驱动程序可以处理硬件中断。 UMDF 同时支持基于行（由级别触发和边缘触发）和消息发出（MSI）中断。

从 Windows 8 开始提供基于行的、级别触发的中断。 在 UMDF 1.11 支持的所有操作系统上，都可以使用 MSI 和基于行的边缘触发的中断。

基于框架的驱动程序使用框架中断对象管理硬件中断。

## <a name="in-this-section"></a>本部分内容


-   [创建中断对象](creating-an-interrupt-object-umdf.md)
-   [启用和禁用中断](enabling-and-disabling-interrupts-umdf.md)
-   [为中断提供服务](servicing-an-interrupt-umdf.md)
-   [使用工作项](using-workitems.md)
-   [正在同步中断代码](synchronizing-interrupt-code-umdf.md)
-   [删除中断对象](deleting-an-interrupt-object.md)

 

 





