---
title: 操作端口
description: 操作端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b43c1d1a463c396bbc4cda6c0b1f844f4f58017
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829209"
---
# <a name="operational-ports"></a>操作端口


从 Windows Server 2012 中的 NDIS 6.30 开始，可扩展交换机接口创建一个可用于承载可扩展交换机网络适配器连接的操作端口。 创建可扩展交换机端口时，将为其分配端口类型。 此端口类型在创建端口之后和被破坏之前有效。 对于分配给 Hyper-v 子分区的端口，操作端口类型在分区运行和运行时保持有效。

操作端口类型定义可连接到的可扩展交换机网络适配器的类型。 可扩展交换机接口定义以下操作端口类型：

<a href="" id="ndisswitchporttypeexternal"></a>**NdisSwitchPortTypeExternal**  
这是配置为连接到可扩展交换机的外部网络适配器的端口。 此适配器在 Hyper-v 父分区中运行的管理操作系统中公开。

外部网络适配器提供主机上的物理网络接口的连接。 Hyper-v 父分区和所有子分区都可以访问外部网络适配器。

**注意**  可扩展交换机仅支持一个外部网络适配器连接。

 

<a href="" id="ndisswitchporttypeinternal"></a>**NdisSwitchPortTypeInternal**  
这是配置为连接到可扩展交换机的内部网络适配器的端口。 此适配器在 Hyper-v 父分区中运行的管理操作系统中公开。

内部网络适配器提供对在管理操作系统中运行的进程的可扩展交换机的访问。 这允许这些进程通过可扩展交换机发送或接收数据包。

**注意**  可扩展交换机只支持一个内部网络适配器。

 

<a href="" id="ndisswitchporttypesynthetic"></a>**NdisSwitchPortTypeSynthetic**  
此端口配置为连接到合成网络适配器。 此适配器在 Hyper-v 子分区中运行的来宾操作系统中公开。

**注意**  合成网络适配器是 (VM) 网络适配器的一种虚拟机。 此适配器在运行 Windows Vista 或更高版本的 Windows 的来宾操作系统中公开。

 

<a href="" id="ndisswitchporttypeemulated"></a>**NdisSwitchPortTypeEmulated**  
此值指定配置为连接到仿真网络适配器的端口。 此适配器在来宾操作系统中公开。

**注意**  仿真网络适配器是一种 VM 网络适配器。 此适配器可在运行 Windows XP 或非 Windows 操作系统的来宾操作系统中公开。

 

 

 





