---
title: 处理 UMDF 驱动程序中的中断
description: 处理中断
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb50351f407d67dcde9e104b2147a3781202e783
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814741"
---
# <a name="handling-interrupts-in-umdf-drivers"></a>处理 UMDF 驱动程序中的中断


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

从 UMDF 版本1.11 开始，UMDF 驱动程序可以处理硬件中断。 UMDF 同时支持基于行的 (，同时触发级别和边缘触发的) 以及消息信号的 (MSI) 中断。

从 Windows 8 开始提供基于行的、级别触发的中断。 在 UMDF 1.11 支持的所有操作系统上，都可以使用 MSI 和基于行的边缘触发的中断。

基于框架的驱动程序使用框架中断对象管理硬件中断。

## <a name="in-this-section"></a>在本节中


-   [创建中断对象](creating-an-interrupt-object-umdf.md)
-   [启用和禁用中断](enabling-and-disabling-interrupts-umdf.md)
-   [为中断提供服务](servicing-an-interrupt-umdf.md)
-   [使用工作项](using-workitems.md)
-   [同步中断代码](synchronizing-interrupt-code-umdf.md)
-   [删除中断对象](deleting-an-interrupt-object.md)

 

 





