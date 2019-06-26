---
title: WIA 驱动程序的安全问题
description: WIA 驱动程序的安全问题
ms.assetid: 5d8fc015-cbf5-43a3-8f65-3ebb17754417
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2685e61c3dc34d91fed8ba12e35ce04f435547c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363518"
---
# <a name="security-issues-for-wia-drivers"></a>WIA 驱动程序的安全问题





运行下的服务**LocalSystem**帐户可以是很危险，因为**LocalSystem**实质上是管理员，因此，已在计算机上几乎任何资源的访问权限。 设计缺陷或下运行的服务中的错误代码**LocalSystem**可能会导致破坏性的用户的特权提升。 Windows XP 引入了两个新内置服务帐户**LocalService**并**NetworkService**，专门旨在缓解服务受到安全威胁的后果。 这两个新帐户是受限制的用户帐户，而无需任何特殊权限，除"作为服务登录"。

为了保持此安全计划，WIA 运行服务**LocalService** Microsoft Windows Server 2003 和更高版本的操作系统版本中的帐户。

在 Windows Server 2003 之前的 WIA 服务和 WIA 驱动程序以开发的假设，它们将在下运行**LocalSystem**。 此更改与 Windows Server 2003 且具有多个驱动程序开发人员需要注意的后果。 本部分包含一系列常见的问题，可能会遇到 WIA 驱动程序开发人员，包括解决这些问题的可能方法。

按照本文档中概述的实践可以确保开发的 WIA 驱动程序将正常工作，是否在 Windows XP、 Windows Server 2003 或更高版本的操作系统版本上运行。

[常见的 WIA 安全问题](common-wia-security-problems.md)

[WIA 安全最佳方案](wia-security-best-practices.md)

有关设备驱动程序的安全性的其他信息，请参阅[保护设备对象](https://docs.microsoft.com/windows-hardware/drivers/kernel/securing-device-objects)并[创建安全的设备安装](https://docs.microsoft.com/windows-hardware/drivers/install/creating-secure-device-installations)部分。

 

 




