---
title: UMDF 如何处理应用程序故障
description: 描述在应用程序失败时 User-Mode Driver Framework (UMDF) 和操作系统的操作。 它适用于 UMDF 版本1和2。
keywords:
- User-Mode Driver Framework WDK，应用程序故障
- UMDF WDK，应用程序故障
- 失败的应用程序 WDK UMDF
- 应用程序故障 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10ffd508adbe95b16ed4f94180934f657c996341
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815611"
---
# <a name="how-umdf-handles-application-failures"></a>UMDF 如何处理应用程序故障


本主题介绍在应用程序失败时 User-Mode Driver Framework (UMDF) 和操作系统的操作。 它适用于 UMDF 版本1和2。

当应用程序失败时，将发生以下事件：

-   反射器接收 [**IRP \_ MJ \_ 清理**](../kernel/irp-mj-cleanup.md)。

-   清除请求将发送到 "取消" IPC 通道上的主机进程。

-   主机进程和 UMDF 驱动程序完成挂起的 i/o 请求。

 

