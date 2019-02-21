---
title: IEC-61883 Protocol Driver
description: IEC-61883 Protocol Driver
ms.assetid: d1e639f0-a22f-4005-86a7-fdbfe509265b
keywords:
- IEC 61883 客户端驱动程序 WDK IEEE 1394 总线
- 61883 WDK IEEE 1394 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60953d981c9fd0e52b2552e782dd62bd23748d35
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543265"
---
# <a name="iec-61883-protocol-driver"></a>IEC-61883 Protocol Driver





IEC 61883 协议驱动程序，*是 61883.sys*，支持 IEC 61883 1 规范中定义的函数控制协议 (FCP)、 常见的同步数据包 (CIP) 格式和连接管理过程 (CMP)。 协议驱动程序中去除流数据包标头与请求、 支持散播-聚集和限制以有效地移动大量数据的缓冲区副本。

若要向设备连接到 IEEE 1394 总线发出 IEC 61883 命令，IEC 61883 客户端驱动程序包含*61883.h* ，并发出[ **IRP\_MJ\_内部\_设备\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550766)使用的 I/O 控制代码的 IRP [ **IOCTL\_61883\_类**](https://msdn.microsoft.com/library/windows/hardware/ff537234)。 客户端驱动程序包中的参数[ **AV\_61883\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff537008)结构，并将指针传递给它在**Parameters.Others.Argument1** IRP 的成员。 **函数**AV 成员\_61883\_结构确定的操作的类型的请求。 AV\_61883\_请求结构包含的数据合并特定于请求的参数结构，每个请求类型之一。

 

 




