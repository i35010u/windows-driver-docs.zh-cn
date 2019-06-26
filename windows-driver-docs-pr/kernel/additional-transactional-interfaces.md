---
title: 其他事务接口
description: 其他事务接口
ms.assetid: cbd88c96-6445-436b-8e02-09dd9cf40d77
keywords:
- 事务 WDK KTM，非 KTM 接口
- 事务性接口 WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 381f4e9ca14aebdce12dc4360bf2201270dfe3c4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369990"
---
# <a name="additional-transactional-interfaces"></a>其他事务接口


除了可以使用通过访问 KTM 的事务接口，Microsoft 还提供多个其他的事务接口，其中包括：

-   文件系统微筛选器驱动程序，请[筛选器管理器](https://docs.microsoft.com/windows-hardware/drivers/ifs/filter-manager-and-minifilter-driver-architecture)提供例程，使微筛选器驱动程序，以在事务中登记接收通知的事务状态更改，并将上下文附加到事务。 有关这些功能的详细信息，请参阅[ **FltEnlistInTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltenlistintransaction)。

-   从 Windows Vista 开始，NTFS 文件系统和注册表实现为支持事务性操作的资源管理器。 有关事务性 NTFS 和事务性注册表功能的详细信息，请参阅 Microsoft Windows SDK。

-   分布式事务处理协调器 (DTC) 提供了与 KTM 通过互操作性**IKernelTransaction**接口。 有关详细信息**IKernelTransaction**接口，请参阅 Microsoft Windows SDK。

-   .NET Framework 支持**System.Transactions**命名空间。 有关此命名空间的详细信息，请参阅[Microsoft 开发人员网站](https://go.microsoft.com/fwlink/p/?linkid=8714)。

 

 




