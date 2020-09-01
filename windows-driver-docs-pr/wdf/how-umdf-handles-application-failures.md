---
title: UMDF 如何处理应用程序故障
description: 描述在应用程序失败时，用户模式驱动程序框架 (UMDF) 和操作系统执行的操作。 它适用于 UMDF 版本1和2。
ms.assetid: ac59a5fe-5975-455f-9da3-318c0692bf9c
keywords:
- 用户模式驱动程序框架 WDK，应用程序故障
- UMDF WDK，应用程序故障
- 失败的应用程序 WDK UMDF
- 应用程序故障 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1443bfb97ea01c2999d59e8c819cd10d9cbe4da
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189659"
---
# <a name="how-umdf-handles-application-failures"></a>UMDF 如何处理应用程序故障


本主题介绍在应用程序失败时，用户模式驱动程序框架 (UMDF) 和操作系统执行的操作。 它适用于 UMDF 版本1和2。

当应用程序失败时，将发生以下事件：

-   反射器接收 [**IRP \_ MJ \_ 清理**](../kernel/irp-mj-cleanup.md)。

-   清除请求将发送到 "取消" IPC 通道上的主机进程。

-   主机进程和 UMDF 驱动程序完成挂起的 i/o 请求。

 

