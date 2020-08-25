---
title: WIA 驱动程序的安全问题
description: WIA 驱动程序的安全问题
ms.assetid: 5d8fc015-cbf5-43a3-8f65-3ebb17754417
ms.date: 08/25/2020
ms.localizationpriority: medium
ms.openlocfilehash: 24f0c18280b35340b09743d2e12ca7922f216864
ms.sourcegitcommit: d9a9925f790271f4ca2c8377d551d96e8d1e62c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88850225"
---
# <a name="security-issues-for-wia-drivers"></a>WIA 驱动程序的安全问题

在 **localsystem** 帐户下运行服务可能很危险，因为 **localsystem** 本质上是管理员，因此可以访问计算机上的几乎任何资源。 在 **LocalSystem** 下运行的服务中设计缺陷或错误代码可能会导致破坏性用户的权限提升。 Windows XP 引入了两个新的内置服务帐户 **LocalService** 和 **NetworkService**，旨在减轻服务泄露的后果。 除了 "作为服务登录" 之外，这两个新帐户都是受限用户帐户，没有任何特殊权限。

在遵守此安全计划后，WIA 服务将在 Microsoft Windows Server 2003 及更高版本的操作系统版本中的 **LocalService** 帐户下运行。

在 Windows Server 2003 之前，将在 WIA 服务和 WIA 驱动程序的假设下开发它们，它们将在 **LocalSystem**下运行。 此更改随 Windows Server 2003 而变化，并具有驱动程序开发人员需要了解的几个后果。 本部分包含 WIA 驱动程序开发人员可能遇到的常见问题列表，其中包括解决这些问题的可能方法。

按照本文档中所述的做法，可以确保开发的 WIA 驱动程序在 Windows XP、Windows Server 2003 或更高版本的操作系统版本上运行时可以正常工作。

[常见的 WIA 安全问题](common-wia-security-problems.md)

[WIA 安全最佳做法](wia-security-best-practices.md)

有关设备驱动程序安全的其他信息，请参阅 [创建安全设备安装](https://docs.microsoft.com/windows-hardware/drivers/install/creating-secure-device-installations)。
