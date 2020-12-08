---
title: 处理停止 IRP（Windows 2000 和更高版本）
description: 处理停止 IRP（Windows 2000 和更高版本）
keywords:
- 停止 Irp WDK PnP
- Irp WDK PnP
- I/o 请求数据包 WDK PnP
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f16fec154b003781a3ead2a07bf63a1e1b13f3a5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837717"
---
# <a name="handling-stop-irps-windows-2000-and-later"></a>处理停止 IRP（Windows 2000 和更高版本）





仅在 Windows 2000 和更高版本的 Windows 上运行 (WDM 版本0x10 和) 更高版本的驱动程序才会在 PnP 管理器间重新平衡资源时接收停止 Irp。 以下部分介绍此类驱动程序在处理停止 Irp 时应使用的技术：

[处理 IRP \_ MN \_ 查询 \_ 停止 \_ 设备请求 (Windows 2000 和更高版本) ](handling-an-irp-mn-query-stop-device-request--windows-2000-and-later-.md)

[处理 IRP \_ MN \_ 停止 \_ 设备请求 (Windows 2000 和更高版本) ](handling-an-irp-mn-stop-device-request--windows-2000-and-later-.md)

[处理 IRP \_ MN \_ CANCEL \_ 停止 \_ 设备请求 (Windows 2000 和更高版本) ](handling-an-irp-mn-cancel-stop-device-request--windows-2000-and-later-.md)

[设备暂停时保持传入的 IRP](holding-incoming-irps-when-a-device-is-paused.md)


 

 




