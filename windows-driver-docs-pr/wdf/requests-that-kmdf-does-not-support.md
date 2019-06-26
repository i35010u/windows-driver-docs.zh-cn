---
title: KMDF 不支持的请求
description: KMDF 不支持的请求
ms.assetid: 1C23BD32-FD55-4D35-B23D-0B320E3DEDF3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f1938f30ed97cd304ea076197ce9a6c81180a0d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376279"
---
# <a name="requests-that-kmdf-does-not-support"></a>KMDF 不支持的请求


\[仅适用于 KMDF\]

内核模式驱动程序框架 (KMDF) 不支持具有以下主要 IRP 代码的 I/O 请求：

-   IRP\_MJ\_CREATE\_MAILSLOT

-   IRP\_MJ\_CREATE\_NAMED\_PIPE

-   IRP\_MJ\_DEVICE\_CHANGE

-   [**IRP\_MJ\_DIRECTORY\_控件**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-directory-control)

-   [**IRP\_MJ\_文件\_系统\_控件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-file-system-control)

-   [**IRP\_MJ\_刷新\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-flush-buffers)

-   [**IRP\_MJ\_锁\_控件**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-lock-control)

-   [**IRP\_MJ\_查询\_EA**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-ea)

-   [**IRP\_MJ\_查询\_信息**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-query-information)

-   [**IRP\_MJ\_查询\_配额**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-quota)

-   [**IRP\_MJ\_QUERY\_SECURITY**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-security)

-   [**IRP\_MJ\_查询\_卷\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-query-volume-information)

-   [**IRP\_MJ\_SET\_EA**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-ea)

-   [**IRP\_MJ\_SET\_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-set-information)

-   [**IRP\_MJ\_SET\_QUOTA**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-quota)

-   [**IRP\_MJ\_SET\_SECURITY**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-security)

-   [**IRP\_MJ\_设置\_卷\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-set-volume-information)

当框架收到此类请求时，其默认操作取决于所请求的目标的设备对象。 对于 FDO 或 PDO，由框架完成状态的状态与 IRP\_无效\_设备\_请求。 对于筛选器的执行，该框架将 IRP 传递给下一个较低的驱动程序。 框架不支持这些请求类型，尽管 KMDF 驱动程序仍可以处理它们。 有关详细信息，请参阅[处理 IRP 框架不支持](handling-an-irp-that-the-framework-does-not-support.md)。

 

 





