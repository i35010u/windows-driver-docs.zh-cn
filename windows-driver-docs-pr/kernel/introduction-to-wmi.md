---
title: WMI 简介
description: WMI 简介
keywords:
- WMI WDK 内核，关于 Windows Management Instrumentation
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef03a0d8429cb85caee03e183a7c1d16c708ca48
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827017"
---
# <a name="introduction-to-wmi"></a>WMI 简介





通过使你的驱动程序成为 WMI 提供程序，你可以：

-   使自定义数据可用于 WMI 使用者。

-   允许 WMI 使用者通过标准接口而不是自定义控制面板应用程序来配置设备。

-   通知驱动程序定义事件的 WMI 使用者，无需使用者轮询或发送 Irp。

-   通过只收集请求的数据并将其发送到单个目标来减少驱动程序开销。

-   用描述性驱动程序定义的类名和可选说明注释数据和事件块，然后 WMI 客户端可以枚举并显示给用户。

 

 




