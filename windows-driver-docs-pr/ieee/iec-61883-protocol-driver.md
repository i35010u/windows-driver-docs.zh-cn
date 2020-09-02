---
title: IEC-61883 协议驱动程序
description: IEC-61883 协议驱动程序
ms.assetid: d1e639f0-a22f-4005-86a7-fdbfe509265b
keywords:
- IEC-61883 客户端驱动程序 WDK IEEE 1394 总线
- 61883 WDK IEEE 1394 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2aa0430372576c0959459aeacab8a611841cb01d
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382233"
---
# <a name="iec-61883-protocol-driver"></a>IEC-61883 协议驱动程序





IEC-61883 协议驱动程序 *61883.sys*支持函数控制协议 (FCP) 、常见的同步数据包 (CIP) 格式和连接管理过程 (CMP) ，如 IEC 61883-1 规范中所定义。 协议驱动程序将数据包标头从请求中提取出，支持散点/集合，并限制缓冲区副本以有效地移动大量的数据。

若要将 IEC-61883 命令发出到连接到 IEEE 1394 总线的设备，IEC-61883 客户端驱动程序包括*61883* ，并向 i/o 控制代码[**IOCTL \_ 61883 \_ 类**](/windows-hardware/drivers/ddi/61883/ni-61883-ioctl_61883_class)发出[**irp \_ MJ \_ 内部 \_ 设备 \_ 控制**](../kernel/irp-mj-internal-device-control.md)IRP。 客户端驱动程序将 [**AV \_ 61883 \_ 请求**](/windows-hardware/drivers/ddi/61883/ns-61883-_av_61883_request) 结构中的参数打包，并在参数中将其指向它的指针。 **其他.** IRP 的 Argument1 成员。 AV **Function** \_ 61883 请求结构的函数成员 \_ 确定操作的类型。 AV \_ 61883 \_ 请求结构包含数据结构联合中特定于请求的参数，每个请求类型一个。

 

