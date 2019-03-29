---
title: 处理停止 IRP（Windows 2000 和更高版本）
description: 处理停止 IRP（Windows 2000 和更高版本）
ms.assetid: 5148ca15-07f0-4a93-aa65-45b13184184b
keywords:
- 停止 Irp WDK 即插即用
- WDK PnP Irp
- I/O 请求数据包 WDK 即插即用
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76f3e916fb18ec21eadfc22b1e179c85524384a9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562212"
---
# <a name="handling-stop-irps-windows-2000-and-later"></a>处理停止 IRP（Windows 2000 和更高版本）





运行仅在 Windows 2000 和更高版本的 Windows 的驱动程序 (WDM 版本 0x10 及更高版本) 接收 Irp 仅当停止即插即用管理器重新平衡资源。 以下部分介绍了此类驱动程序应使用在处理停止 Irp 的技术：

[处理 IRP\_MN\_查询\_停止\_设备请求 (Windows 2000 及更高版本)](handling-an-irp-mn-query-stop-device-request--windows-2000-and-later-.md)

[处理 IRP\_MN\_停止\_设备请求 (Windows 2000 及更高版本)](handling-an-irp-mn-stop-device-request--windows-2000-and-later-.md)

[处理 IRP\_MN\_取消\_停止\_设备请求 (Windows 2000 及更高版本)](handling-an-irp-mn-cancel-stop-device-request--windows-2000-and-later-.md)

[暂停设备时保存传入 Irp](holding-incoming-irps-when-a-device-is-paused.md)

WDM 驱动程序，也在运行 Windows 98/我必须以不同方式处理这些 Irp。 请参阅[处理停止 Irp (Windows 98 / 我)](handling-stop-irps--windows-98-me-.md)有关详细信息。

 

 




