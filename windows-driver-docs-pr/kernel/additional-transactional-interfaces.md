---
title: 其他事务接口
description: 其他事务接口
ms.assetid: cbd88c96-6445-436b-8e02-09dd9cf40d77
keywords:
- 事务 WDK KTM，非 KTM 接口
- 事务性接口 WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44c6b4ffd8c2186362479fa573e7102ad22be02c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562043"
---
# <a name="additional-transactional-interfaces"></a>其他事务接口


除了可以使用通过访问 KTM 的事务接口，Microsoft 还提供多个其他的事务接口，其中包括：

-   文件系统微筛选器驱动程序，请[筛选器管理器](https://msdn.microsoft.com/library/windows/hardware/ff541591)提供例程，使微筛选器驱动程序，以在事务中登记接收通知的事务状态更改，并将上下文附加到事务。 有关这些功能的详细信息，请参阅[ **FltEnlistInTransaction**](https://msdn.microsoft.com/library/windows/hardware/ff542053)。

-   从 Windows Vista 开始，NTFS 文件系统和注册表实现为支持事务性操作的资源管理器。 有关事务性 NTFS 和事务性注册表功能的详细信息，请参阅 Microsoft Windows SDK。

-   分布式事务处理协调器 (DTC) 提供了与 KTM 通过互操作性**IKernelTransaction**接口。 有关详细信息**IKernelTransaction**接口，请参阅 Microsoft Windows SDK。

-   .NET Framework 支持**System.Transactions**命名空间。 有关此命名空间的详细信息，请参阅[Microsoft 开发人员网站](https://go.microsoft.com/fwlink/p/?linkid=8714)。

 

 




