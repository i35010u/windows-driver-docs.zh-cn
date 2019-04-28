---
title: 处理停止 IRP (Windows 98/Me)
description: 处理停止 IRP (Windows 98/Me)
ms.assetid: 98eefb69-e321-4cc5-8b4d-79335cd8b06e
keywords:
- 停止 Irp WDK 即插即用
- WDK PnP Irp
- I/O 请求数据包 WDK 即插即用
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1ec33ac2180319cab05bcd7cafddf1d0cfec627
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334048"
---
# <a name="handling-stop-irps-windows-98me"></a>处理停止 IRP (Windows 98/Me)





在 Windows 98 上 / PnP 管理器可以将我，发送停止 Irp，原因如下：

-   若要重新平衡资源时暂停设备

-   当设备管理器禁用它时停用设备

-   若要在失败后停止设备[ **IRP\_MN\_启动\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749)请求

驱动程序无法确定从 IRP 发送的原因。 因此，在 Windows 98 上，运行 WDM 驱动程序/我必须处理所有停止 Irp，因为如果设备已被禁用。 简单地说，这意味着此类驱动程序失败传入 I/O 请求，而不是队列 （作为 Windows 2000 及更高版本）。

以下主题提供有关处理其中每个停止 Irp 的循序渐进的详细信息：

[处理 IRP\_MN\_查询\_停止\_设备请求 (Windows 98 / 我)](handling-an-irp-mn-query-stop-device-request--windows-98-me-.md)

[处理 IRP\_MN\_停止\_设备请求 (Windows 98 / 我)](handling-an-irp-mn-stop-device-request--windows-98-me-.md)

[处理 IRP\_MN\_取消\_停止\_设备请求 (Windows 98 / 我)](handling-an-irp-mn-cancel-stop-device-request--windows-98-me-.md)

 

 




