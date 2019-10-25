---
title: 其他事务接口
description: 其他事务接口
ms.assetid: cbd88c96-6445-436b-8e02-09dd9cf40d77
keywords:
- 事务 WDK KTM，非 KTM 接口
- 事务性接口 WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 325221049233093e0ca88ea86a8c9234f74da01e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837240"
---
# <a name="additional-transactional-interfaces"></a>其他事务接口


除了可通过访问 KTM 而使用的事务接口外，Microsoft 还提供了几个附加的事务接口，其中包括：

-   对于文件系统微筛选器驱动程序，[筛选器管理](https://docs.microsoft.com/windows-hardware/drivers/ifs/filter-manager-and-minifilter-driver-architecture)器提供使微筛选器驱动程序在事务中登记、接收有关事务状态更改的通知以及将上下文附加到事务的例程。 有关这些功能的详细信息，请参阅[**FltEnlistInTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltenlistintransaction)。

-   从 Windows Vista 开始，NTFS 文件系统和注册表作为支持事务操作的资源管理器实现。 有关事务性 NTFS 和事务性注册表功能的详细信息，请参阅 Microsoft Windows SDK。

-   分布式事务处理协调器（DTC）通过**IKernelTransaction**接口提供与 KTM 的互操作性。 有关**IKernelTransaction**接口的详细信息，请参阅 Microsoft Windows SDK。

-   .NET Framework 支持**system.object**命名空间。 有关此命名空间的详细信息，请参阅[Microsoft 开发人员网站](https://go.microsoft.com/fwlink/p/?linkid=8714)。

 

 




