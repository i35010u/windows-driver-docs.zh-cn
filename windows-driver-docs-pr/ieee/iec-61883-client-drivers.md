---
title: IEC-61883 客户端驱动程序
description: IEC-61883 客户端驱动程序
ms.assetid: 2a3f62d0-c1f2-4978-8f89-3ed800d697f4
keywords:
- IEC 61883 客户端驱动程序 WDK IEEE 1394 总线
- 61883 WDK IEEE 1394 总线
- IEEE 1394 WDK 总线，IEC 61883 客户端驱动程序
- 1394 WDK 总线，IEC 61883 客户端驱动程序
- 协议 WDK 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6396d63a2992d6c90449ca8253303ce0dddadec7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564889"
---
# <a name="iec-61883-client-drivers"></a>IEC-61883 客户端驱动程序





IEC 61883 是 IEEE 1394 音频和视频设备所使用的标准通信和控制接口。 在 Windows 98 SE、 Windows 2000 和更早的操作系统，61883 功能作为 Microsoft 数字视频 (MSDV) 摄像机驱动程序的一部分实现*msdv.sys*。 在 Windows Me，、 Windows XP 和更高版本的操作系统，61883 功能已移到单独的驱动程序，专用于 61883 支持。 供应商提供 IEC 61883 客户端驱动程序将请求发送到系统提供[IEC 61883 协议驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff537191)(*是 61883.sys*) 与他们的设备进行通信。

IEC 61883 规范定义的许多使用者电子音频和视频设备可以相互连接起来的协议。 这些规范包括常规数据格式、 数据流和视听信息的连接方案的定义。 IEC 61883 协议驱动程序支持符合以下认可 IEC 61883 规范的设备：

-   IEC 61883 1:常规

-   IEC 61883 2:SD VCR 数据传输

-   IEC 61883 3:HD VCR 数据传输

-   IEC 61883 4:MPEG2-TS 数据传输

-   IEC 61883 5:SDL DVCR 数据传输

-   IEC 61883 6:音频和音乐数据传输协议

本部分包括：

[IEC 61883 协议驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff537191)
[IEC 61883 协议在客户端驱动程序堆栈中的驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff537193)
 

 




