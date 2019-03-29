---
title: KMDF 不支持的请求
description: KMDF 不支持的请求
ms.assetid: 1C23BD32-FD55-4D35-B23D-0B320E3DEDF3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bbae806198afcbe8fad8f43c2367ff86411daf73
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577435"
---
# <a name="requests-that-kmdf-does-not-support"></a>KMDF 不支持的请求


\[仅适用于 KMDF\]

内核模式驱动程序框架 (KMDF) 不支持具有以下主要 IRP 代码的 I/O 请求：

-   IRP\_MJ\_CREATE\_MAILSLOT

-   IRP\_MJ\_CREATE\_NAMED\_PIPE

-   IRP\_MJ\_DEVICE\_CHANGE

-   [**IRP\_MJ\_DIRECTORY\_控件**](https://msdn.microsoft.com/library/windows/hardware/ff548658)

-   [**IRP\_MJ\_文件\_系统\_控件**](https://msdn.microsoft.com/library/windows/hardware/ff550751)

-   [**IRP\_MJ\_刷新\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff550760)

-   [**IRP\_MJ\_锁\_控件**](https://msdn.microsoft.com/library/windows/hardware/ff549251)

-   [**IRP\_MJ\_查询\_EA**](https://msdn.microsoft.com/library/windows/hardware/ff549279)

-   [**IRP\_MJ\_查询\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff550788)

-   [**IRP\_MJ\_查询\_配额**](https://msdn.microsoft.com/library/windows/hardware/ff549293)

-   [**IRP\_MJ\_QUERY\_SECURITY**](https://msdn.microsoft.com/library/windows/hardware/ff549298)

-   [**IRP\_MJ\_查询\_卷\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff549318)

-   [**IRP\_MJ\_SET\_EA**](https://msdn.microsoft.com/library/windows/hardware/ff549346)

-   [**IRP\_MJ\_SET\_INFORMATION**](https://msdn.microsoft.com/library/windows/hardware/ff550799)

-   [**IRP\_MJ\_SET\_QUOTA**](https://msdn.microsoft.com/library/windows/hardware/ff549401)

-   [**IRP\_MJ\_SET\_SECURITY**](https://msdn.microsoft.com/library/windows/hardware/ff549407)

-   [**IRP\_MJ\_设置\_卷\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff549415)

当框架收到此类请求时，其默认操作取决于所请求的目标的设备对象。 对于 FDO 或 PDO，由框架完成状态的状态与 IRP\_无效\_设备\_请求。 对于筛选器的执行，该框架将 IRP 传递给下一个较低的驱动程序。 框架不支持这些请求类型，尽管 KMDF 驱动程序仍可以处理它们。 有关详细信息，请参阅[处理 IRP 框架不支持](handling-an-irp-that-the-framework-does-not-support.md)。

 

 





