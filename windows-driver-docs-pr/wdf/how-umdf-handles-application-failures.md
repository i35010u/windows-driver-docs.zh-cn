---
title: UMDF 如何处理应用程序故障
description: 介绍在应用程序失败时，用户模式驱动程序框架 (UMDF) 和操作系统执行的操作。 它适用于这两种 UMDF 版本 1 和 2。
ms.assetid: ac59a5fe-5975-455f-9da3-318c0692bf9c
keywords:
- 用户模式驱动程序框架 WDK，应用程序故障
- UMDF WDK，应用程序故障
- 失败的应用程序 WDK UMDF
- 应用程序故障 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42055756ed9c46efeb91e731a429692fe5ef945a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382829"
---
# <a name="how-umdf-handles-application-failures"></a>UMDF 如何处理应用程序故障


本主题介绍在应用程序失败时，用户模式驱动程序框架 (UMDF) 和操作系统执行的操作。 它适用于这两种 UMDF 版本 1 和 2。

当应用程序失败时，发生以下事件：

-   该发送程序接收[ **IRP\_MJ\_清理**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-cleanup)。

-   清除请求发送到"取消"IPC 信道上的主机进程。

-   主机进程和 UMDF 驱动程序完成的挂起 I/O 请求。

 

 





