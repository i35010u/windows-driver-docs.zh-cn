---
title: 其他事务接口
description: 其他事务接口
keywords:
- 事务 WDK KTM，非 KTM 接口
- 事务性接口 WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb6aaa68be03317c739797e3c9c35fada42c2f8a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836953"
---
# <a name="additional-transactional-interfaces"></a>其他事务接口


除了可通过访问 KTM 而使用的事务接口外，Microsoft 还提供了几个附加的事务接口，其中包括：

-   对于文件系统微筛选器驱动程序， [筛选器管理](../ifs/filter-manager-concepts.md) 器提供使微筛选器驱动程序在事务中登记、接收有关事务状态更改的通知以及将上下文附加到事务的例程。 有关这些功能的详细信息，请参阅 [**FltEnlistInTransaction**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltenlistintransaction)。

-   从 Windows Vista 开始，NTFS 文件系统和注册表作为支持事务操作的资源管理器实现。 有关事务性 NTFS 和事务性注册表功能的详细信息，请参阅 Microsoft Windows SDK。

-   分布式事务处理协调器 (DTC) 通过 **IKernelTransaction** 接口提供与 KTM 的互操作性。 有关 **IKernelTransaction** 接口的详细信息，请参阅 Microsoft Windows SDK。

-   .NET Framework 支持 **system.object** 命名空间。 有关此命名空间的详细信息，请参阅 [Microsoft 开发人员网站](https://go.microsoft.com/fwlink/p/?linkid=8714)。

