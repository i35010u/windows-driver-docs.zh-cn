---
title: IEC-61883 客户端驱动程序
description: IEC-61883 客户端驱动程序
keywords:
- IEC-61883 客户端驱动程序 WDK IEEE 1394 总线
- 61883 WDK IEEE 1394 总线
- IEEE 1394 WDK 总线，IEC-61883 客户端驱动程序
- 1394 WDK 总线，IEC-61883 客户端驱动程序
- 协议 WDK 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15ef80935ea3dc8bbb1223579957daba0d246406
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808841"
---
# <a name="iec-61883-client-drivers"></a>IEC-61883 客户端驱动程序





IEC-61883 是 IEEE 1394 音频和视频设备使用的标准通信和控制接口。 在 Windows 98 SE、Windows 2000 及更早版本的操作系统中，61883功能作为 Microsoft 数字视频 (MSDV) 摄像机驱动程序的一部分实现， *msdv.sys*。 在 Windows Me、Windows XP 和更高版本的操作系统中，61883功能已移至专用于61883支持的单独驱动程序。 供应商提供的 IEC-61883 客户端驱动程序将请求发送到系统提供的 [iec-61883 协议驱动程序](./iec-61883-protocol-driver.md) ， (*61883.sys*) 与设备通信。

IEC-61883 规范定义了许多使用者电子音频和视频设备可以互连的协议。 这些规范包括一般数据格式的定义、数据流和视听信息的连接方案。 IEC-61883 协议驱动程序支持符合以下批准的 IEC-61883 规范的设备：

-   IEC-61883-1：常规

-   IEC-61883-2： SD-VCR 数据传输

-   IEC-61883-3： HD-VCR 数据传输

-   IEC-61883-4： MPEG2-TS 数据传输

-   IEC-61883-5： DVCR 数据传输

-   IEC-61883-6：音频和音乐数据传输协议

本节包括：

[IEC-61883 协议驱动程序](./iec-61883-protocol-driver.md) 
[客户端驱动程序堆栈中的 IEC-61883 协议驱动程序](./iec-61883-protocol-driver-in-a-client-driver-stack.md)
 

