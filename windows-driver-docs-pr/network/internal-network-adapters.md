---
title: 内部网络适配器
description: 内部网络适配器
ms.assetid: 4E4B0EC9-8E4C-47FC-B608-EC6D18367A79
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1dbd371ab4a6b7599675e0afb1ccd6a5135d39a7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362918"
---
# <a name="internal-network-adapters"></a>内部网络适配器


内部网络适配器运行在 HYPER-V 父分区中管理操作系统中公开。 此类型的网络适配器提供对可扩展交换机的管理操作系统中运行的进程的访问。 这允许这些进程发送或接收通过可扩展交换机的数据包。

如果可扩展交换机配置为提供的内部网络适配器连接，在启动开关时，会发生以下步骤：

1.  可扩展交换机的协议边缘发出的一个对象标识符 (OID) 组请求[OID\_切换\_端口\_创建](https://msdn.microsoft.com/library/windows/hardware/hh598272)向下可扩展交换机驱动程序堆栈。 此 OID 请求通知的基础的可扩展交换机扩展内部网络适配器创建端口

2.  可扩展交换机的协议边缘颁发的 OID 集请求[OID\_切换\_NIC\_创建](https://msdn.microsoft.com/library/windows/hardware/hh598272)向下可扩展交换机驱动程序堆栈。 此 OID 请求通知的基础的可扩展交换机扩展先前创建的端口创建内部网络适配器的网络连接。

3.  可扩展交换机的协议边缘颁发的 OID 集请求[OID\_切换\_NIC\_CONNECT](https://msdn.microsoft.com/library/windows/hardware/hh598272)向下可扩展交换机驱动程序堆栈。 此 OID 请求通知的基础的可扩展交换机扩展的内部网络适配器的网络连接已连接并且正常运行。 此时，该扩展可以检查、 注入，并将数据包转发到已连接到内部网络适配器的端口。

停止与内部网络适配器连接的可扩展交换机时，将执行以下步骤：

1.  可扩展交换机的协议边缘颁发的 OID 集请求[OID\_切换\_NIC\_断开连接](https://msdn.microsoft.com/library/windows/hardware/hh598265)向下可扩展交换机驱动程序堆栈。 此 OID 请求通知到外部网络适配器的连接，则正在将调用的基础可扩展交换机扩展。

2.  完成所有数据包流量和目标网络连接的 OID 请求后，可扩展交换机的协议边缘颁发的 OID 集请求[OID\_切换\_NIC\_删除](https://msdn.microsoft.com/library/windows/hardware/hh598272)向下可扩展交换机驱动程序堆栈。 此 OID 请求通知的基础的可扩展交换机扩展，与外部网络适配器的连接已适当地销毁并删除。

3.  可扩展交换机的协议边缘颁发的 OID 集请求[OID\_切换\_端口\_拆卸](https://msdn.microsoft.com/library/windows/hardware/hh598279)向下可扩展交换机驱动程序堆栈。 此 OID 请求通知所用的外部网络适配器连接的端口，则在将调用的基础可扩展交换机扩展。

4.  可扩展交换机的协议边缘颁发的 OID 集请求[OID\_切换\_端口\_删除](https://msdn.microsoft.com/library/windows/hardware/hh598273)向下可扩展交换机驱动程序堆栈。 此 OID 请求通知的基础的可扩展交换机扩展用于内部网络适配器连接的端口已在拆解和删除。

 

 





