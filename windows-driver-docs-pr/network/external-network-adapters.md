---
title: 外部网络适配器
description: 外部网络适配器
ms.assetid: 4029437C-97EA-4F21-A3F0-3B29DC650233
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0be2ec56d6a62996590d1cde869781622c2d692
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540408"
---
# <a name="external-network-adapters"></a>外部网络适配器


在 HYPER-V 父分区中运行管理操作系统中公开的外部网络适配器。 外部网络适配器提供了与 HYPER-V 外部网络的连接。 通过主机的物理网络接口，此网络将转发数据包流量。

由 HYPER-V 父分区和已连接到可扩展交换机的所有子分区访问外部网络。 可扩展交换机的每个实例支持多个外部网络适配器连接。

外部网络适配器是主机上的基础物理网络适配器的虚拟表示形式。 外部网络适配器转发数据包、 对象标识符 (Oid) 请求和从一个或多个基础物理网络适配器与的 NDIS 状态指示。

在内部，外部网络适配器将绑定到的基础物理网络适配器的各种配置。 每个这些配置提供对外部网络接口通过一个或多个物理网络适配器的访问。 有关这些物理适配器配置的详细信息，请参阅[的物理网络适配器配置的类型](types-of-physical-network-adapter-configurations.md)。

如果可扩展交换机配置为提供的外部网络适配器连接，在启动开关时，会发生以下步骤：

1.  可扩展交换机的协议边缘发出的一个对象标识符 (OID) 组请求[OID\_切换\_端口\_创建](https://msdn.microsoft.com/library/windows/hardware/hh598272)向下可扩展交换机驱动程序堆栈。 此 OID 请求通知的基础的可扩展交换机扩展外部网络适配器创建一个端口。

2.  可扩展交换机的协议边缘颁发的 OID 集请求[OID\_切换\_NIC\_创建](https://msdn.microsoft.com/library/windows/hardware/hh598272)向下可扩展交换机驱动程序堆栈。 此 OID 请求通知的基础的可扩展交换机扩展先前创建的端口创建的外部网络适配器的网络连接。

3.  可扩展交换机的协议边缘颁发的 OID 集请求[OID\_切换\_NIC\_CONNECT](https://msdn.microsoft.com/library/windows/hardware/hh598272)向下可扩展交换机驱动程序堆栈。 此 OID 请求通知的基础的可扩展交换机扩展的外部网络适配器的网络连接已连接并且正常运行。 此时，该扩展可以检查、 注入，并将数据包转发到已连接到外部网络适配器的端口。

停止与外部网络适配器连接的可扩展交换机时，将执行以下步骤：

1.  可扩展交换机的协议边缘颁发的 OID 集请求[OID\_切换\_NIC\_断开连接](https://msdn.microsoft.com/library/windows/hardware/hh598265)向下可扩展交换机驱动程序堆栈。 此 OID 请求通知到外部网络适配器的连接，则正在将调用的基础可扩展交换机扩展。

2.  完成所有数据包流量和目标网络连接的 OID 请求后，可扩展交换机的协议边缘颁发的 OID 集请求[OID\_切换\_NIC\_删除](https://msdn.microsoft.com/library/windows/hardware/hh598272)向下可扩展交换机驱动程序堆栈。 此 OID 请求通知的基础的可扩展交换机扩展，与外部网络适配器的连接已适当地销毁并删除。

3.  可扩展交换机的协议边缘颁发的 OID 集请求[OID\_切换\_端口\_拆卸](https://msdn.microsoft.com/library/windows/hardware/hh598279)向下可扩展交换机驱动程序堆栈。 此 OID 请求通知所用的外部网络适配器连接的端口，则在将调用的基础可扩展交换机扩展。

4.  可扩展交换机的协议边缘颁发的 OID 集请求[OID\_切换\_端口\_删除](https://msdn.microsoft.com/library/windows/hardware/hh598273)向下可扩展交换机驱动程序堆栈。 此 OID 请求所用的外部网络适配器连接的端口已在拆解和删除通知的基础的可扩展交换机扩展。

 

 





