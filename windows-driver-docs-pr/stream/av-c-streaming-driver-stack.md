---
title: AV/C 流式处理驱动程序堆栈
description: AV/C 流式处理驱动程序堆栈
keywords:
- AV/C WDK，流筛选器驱动程序
- 流筛选器驱动程序 WDK AV/C
- Avcstrm.sys 流筛选器驱动程序 WDK，驱动程序堆栈
- 驱动程序堆栈 WDK AV/C 流式处理
- 堆栈 WDK AV/C 流式处理
- 对等驱动程序堆栈 WDK AV/C 流式处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de6ee9dbea0e28e05b057c7ef52e5e295fcab2bd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833989"
---
# <a name="avc-streaming-driver-stack"></a>AV/C 流式处理驱动程序堆栈





Windows (FDO) 和 *)* 创建的 (PDOAvc.sys，在子实体驱动程序的功能设备对象之间加载 *Avcstrm.sys* 。 *Avcstrm.sys* 位于单个子单位驱动程序和函数驱动程序之间， *Avc.sys*。 *Avcstrm.sys* 作为更低级别的筛选器驱动程序安装到子单元驱动程序，以便提供其流式处理服务。 *Avcstrm.sys* 提供的流式处理服务的接口基于 WDM 体系结构所使用的 i/o 请求包 (IRP) 模型，以及 (IOCTL) 函数的支持 i/o 控件列表。 *Avcstrm.sys* 可以为基于 Stream 类或 AVStream 接口的子单位驱动程序服务。 AVStream 驱动程序模型是要使用的首选接口。 下图说明 *Avcstrm.sys* 适合 AV/C 驱动程序堆栈的位置。

![使用 avcstrm.sys 低筛选器驱动程序说明对等 av/c 驱动程序堆栈的关系图](images/avcsdiag.gif)

*Avcstrm.sys* 是可识别格式的。 它必须知道流式处理数据（如 SDDV 或 MPEG2TS）的数据格式，以便在源和目标设备之间建立正确的同步连接。 使用给定的格式信息， *Avcstrm.sys* 可以通过61883协议驱动程序通过协议驱动程序与 AV/C 子单位的驱动程序进行交互，以接收或传输数据。 由于 *Avcstrm.sys* 是可识别格式的，因此必须将其更新以添加不同的格式 (例如，Service Pack 或新的操作系统版本) 。 目前，只有 SDDV 和 MPEG2TS 格式实现了格式。

将来， *Avcstrm.sys* 可能会扩展到：

-   查询数据格式

-    (在两个 pin 之间协商数据格式来执行数据交集) 

-   是时钟提供商

-   获取和设置流式处理属性

目前，每个子单位驱动程序必须实现前面的操作。

AV/C 流式处理筛选器驱动程序此时没有时间戳数据。 时钟提供程序需要提供数据的时间戳，并提供当前的流时间。 如果数据为时钟提供程序，则子单位驱动程序必须将数据时间戳。

 

 




