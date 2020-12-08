---
title: KMDF 不支持的请求
description: KMDF 不支持的请求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 359ca295a314615dc517f63f9413e917fdf4c279
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821705"
---
# <a name="requests-that-kmdf-does-not-support"></a>KMDF 不支持的请求


\[仅适用于 KMDF\]

Kernel-Mode Driver Framework (KMDF) 不支持具有以下主要 IRP 代码的 i/o 请求：

-   IRP \_ MJ \_ CREATE \_ MAILSLOT

-   IRP \_ MJ \_ 创建 \_ 命名 \_ 管道

-   IRP \_ MJ \_ 设备 \_ 更改

-   [**IRP \_ MJ \_ 目录 \_ 控件**](../ifs/irp-mj-directory-control.md)

-   [**IRP \_ MJ \_ 文件 \_ 系统 \_ 控制**](../kernel/irp-mj-file-system-control.md)

-   [**IRP \_ MJ \_ 刷新 \_ 缓冲区**](../kernel/irp-mj-flush-buffers.md)

-   [**IRP \_ MJ \_ 锁定 \_ 控制**](../ifs/irp-mj-lock-control.md)

-   [**IRP \_ MJ \_ 查询 \_ EA**](../ifs/irp-mj-query-ea.md)

-   [**IRP \_ MJ \_ 查询 \_ 信息**](../kernel/irp-mj-query-information.md)

-   [**IRP \_ MJ \_ 查询 \_ 配额**](../ifs/irp-mj-query-quota.md)

-   [**IRP \_ MJ \_ 查询 \_ 安全性**](../ifs/irp-mj-query-security.md)

-   [**IRP \_ MJ \_ 查询 \_ 卷 \_ 信息**](../ifs/irp-mj-query-volume-information.md)

-   [**IRP \_ MJ \_ 设置 \_ EA**](../ifs/irp-mj-set-ea.md)

-   [**IRP \_ MJ \_ 设置 \_ 信息**](../kernel/irp-mj-set-information.md)

-   [**IRP \_ MJ \_ 设置 \_ 配额**](../ifs/irp-mj-set-quota.md)

-   [**IRP \_ MJ \_ 设置 \_ 安全性**](../ifs/irp-mj-set-security.md)

-   [**IRP \_ MJ \_ 设置 \_ 卷 \_ 信息**](../ifs/irp-mj-set-volume-information.md)

当框架收到此类请求时，其默认操作取决于作为请求目标的设备对象。 对于 FDO 或 PDO，框架使用状态 " \_ 无效设备请求" 完成 IRP \_ \_ 。 对于筛选器，该框架会将 IRP 传递到下一个较低版本的驱动程序。 尽管框架不支持这些请求类型，但 KMDF 驱动程序仍可以处理它们。 有关详细信息，请参阅 [处理框架不支持的 IRP](handling-an-irp-that-the-framework-does-not-support.md)。

 

