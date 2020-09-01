---
title: 驱动程序中的访问控制
description: 驱动程序通过访问控制保护自身免受不正当的访问。
ms.assetid: 7f87276f-4014-4b37-b051-4bf02acbf575
keywords:
- 安全 WDK 文件系统，最大限度地减少威胁
- access control WDK 文件系统
- access 验证 WDK 文件系统
- 验证安全 WDK 文件系统
- 检查安全性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83479adf592748087011db9cb15f5fb12f6e0d9e
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066256"
---
# <a name="access-control-in-a-driver"></a>驱动程序中的访问控制

为了防止对自身进行不当访问，大多数驱动程序依赖于 i/o 管理器针对其设备对象应用的默认访问控制。 驱动程序可以使用其他机制。 通常，最简单的驱动程序是在安装其驱动程序时应用显式安全描述符。 后面的部分将介绍将安全描述符应用到设备对象的示例。

实现其自己的安全策略的驱动程序可以依赖标准 Windows Api 来帮助管理安全访问。 在这种情况下，驱动程序将管理安全描述符的存储，并负责调用安全引用监视器例程来验证安全性。 其中包括多个例程，如下所示：

- [**SeAccessCheck**](/windows-hardware/drivers/ddi/wdm/nf-wdm-seaccesscheck)-此例程比较安全描述符和调用方的安全凭据。

- [**SePrivilegeCheck**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-seprivilegecheck)--此例程确定是否为调用方启用了给定的权限。

- [**SeSinglePrivilegeCheck**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-sesingleprivilegecheck)--此例程确定是否为调用方启用了特定权限。

- [**SeAuditingFileOrGlobalEvents**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-seauditingfileorglobalevents)--此例程指示系统是否已启用审核。

- [**SeOpenObjectAuditAlarm**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-seopenobjectauditalarm)--此例程审核打开对象事件。

此列表不完整，但它描述了许多可在驱动程序中用来执行访问验证的关键功能。