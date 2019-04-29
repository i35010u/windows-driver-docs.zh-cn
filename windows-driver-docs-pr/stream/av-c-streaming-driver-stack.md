---
title: AV/C 流式处理驱动程序堆栈
description: AV/C 流式处理驱动程序堆栈
ms.assetid: 2584c74c-ddd6-43cc-9a8c-cd7f43802c4c
keywords:
- AV/C WDK，Stream 筛选器驱动程序
- Stream 筛选器驱动程序 WDK AV/C
- Avcstrm.sys 流式处理筛选器驱动程序 WDK，驱动程序堆栈
- 驱动程序堆栈 WDK AV/C 流式处理
- 堆栈 WDK AV/C 流式处理
- 对等互连驱动程序堆栈 WDK AV/C 的流式处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f1eadd02bc0876658d4b0d1aae2522a1e60c191
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323548"
---
# <a name="avc-streaming-driver-stack"></a>AV/C 流式处理驱动程序堆栈





Windows 将加载*Avcstrm.sys*子单元驱动程序的功能的设备对象 (FDO) 和创建相应的物理设备对象 (PDO) 之间*Avc.sys*。 *Avcstrm.sys*之间的单个子单元驱动程序和功能驱动程序，驻留*Avc.sys*。 *Avcstrm.sys*作为子单元驱动程序的较低级别筛选器驱动程序进行安装，以便提供其流式处理服务。 提供的流式处理服务的接口*Avcstrm.sys* WDM 体系结构的支持的 I/O 控制 (IOCTL) 函数的列表，使用的 I/O 请求数据包 (IRP) 模型为基础。 *Avcstrm.sys*可以提供服务基于 Stream 类或 AVStream 接口的子单元驱动程序。 AVStream 驱动程序模型是要使用的首选的接口。 下图说明了在何处*Avcstrm.sys*适合 AV/C 驱动程序堆栈。

![说明使用 avcstrm.sys 低筛选器驱动程序的对等方 av/c 驱动程序堆栈的关系图](images/avcsdiag.gif)

*Avcstrm.sys*格式识别。 它必须知道的数据格式的流式处理的数据，例如 SDDV 或 MPEG2TS，才能正确同步之间建立连接的源和目标设备。 使用给定的格式信息*Avcstrm.sys*然后可与 AV/C 子单元的驱动程序通过 61883 协议驱动程序将接收或传输数据。 因为*Avcstrm.sys*格式识别，它必须经过更新以添加不同的格式 （例如，服务包或新操作系统系统版本）。 目前，SDDV 和 MPEG2TS 格式是实现的唯一格式。

在将来*Avcstrm.sys*可能会扩展到：

-   查询数据格式

-   执行数据交集 （协商两个插针之间的数据格式）

-   是时钟的访问接口

-   获取和设置流式处理属性

目前，每个子单元驱动程序必须实现上述操作。

AV/C 流式处理筛选器驱动程序执行这一次不是时间戳数据。 时钟提供程序需要的时间戳的数据，以及提供当前流的时间。 如果它是一个时钟提供程序，则子单元驱动程序必须时间戳数据。

 

 




