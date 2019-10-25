---
title: IEC-61883 协议驱动程序
description: IEC-61883 协议驱动程序
ms.assetid: d1e639f0-a22f-4005-86a7-fdbfe509265b
keywords:
- IEC-61883 客户端驱动程序 WDK IEEE 1394 总线
- 61883 WDK IEEE 1394 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d18dcea1667af8def5ae437e283d7ec6f9048077
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841539"
---
# <a name="iec-61883-protocol-driver"></a>IEC-61883 协议驱动程序





IEC-61883 协议驱动程序*61883*支持函数控制协议（FCP）、常见的同步数据包（CIP）格式和连接管理过程（CMP），如 iec 61883-1 规范中所定义。 协议驱动程序将数据包标头从请求中提取出，支持散点/集合，并限制缓冲区副本以有效地移动大量的数据。

若要将 IEC-61883 命令发出到连接到 IEEE 1394 总线的设备，IEC-61883 客户端驱动程序包括*61883* ，并颁发[**IRP\_MJ\_内部\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)IRP 与 i/o 控制代码[**IOCTL\_61883\_类**](https://docs.microsoft.com/windows-hardware/drivers/ddi/61883/ni-61883-ioctl_61883_class)。 客户端驱动程序将[**AV\_61883\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/61883/ns-61883-_av_61883_request)结构中的参数打包，并在参数中传递指向它的指针。 **Argument1 的其他**成员。 AV\_61883\_请求结构的**函数**成员确定操作的类型。 AV\_61883\_请求结构包含数据结构联合中特定于请求的参数，每个请求类型一个。

 

 




