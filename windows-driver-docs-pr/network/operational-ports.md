---
title: 操作端口
description: 操作端口
ms.assetid: 647EBDFD-A100-46A7-B387-BF11004415EC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1099da8298d00f12290045da7df747c8a8c044c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359140"
---
# <a name="operational-ports"></a>操作端口


从 Windows Server 2012 中的 NDIS 6.30 开始，可扩展交换机接口用于创建托管的可扩展交换机的网络适配器连接的操作端口。 创建可扩展交换机端口时，它被分配端口类型。 创建端口后，在它，则将调用之前，此端口类型将生效。 为端口分配给 HYPER-V 子分区，分区时运行和操作的操作的端口类型一直有效。

操作端口类型定义可以连接到它的可扩展交换机网络适配器的类型。 可扩展交换机接口定义以下操作的端口类型：

<a href="" id="ndisswitchporttypeexternal"></a>**NdisSwitchPortTypeExternal**  
这是配置为连接到可扩展交换机的外部网络适配器的端口。 此适配器的 HYPER-V 父分区中运行管理操作系统中公开。

外部网络适配器提供了与主机上可用的物理网络接口的连接。 可以通过 HYPER-V 父分区和所有子分区访问外部网络适配器。

**请注意**  可扩展交换机支持只能有一个外部网络适配器连接。

 

<a href="" id="ndisswitchporttypeinternal"></a>**NdisSwitchPortTypeInternal**  
这是交换机的配置为连接到内部网络适配器的可扩展端口。 此适配器的 HYPER-V 父分区中运行管理操作系统中公开。

内部网络适配器提供对可扩展交换机的管理操作系统中运行的进程的访问。 这允许这些进程发送或接收通过可扩展交换机的数据包。

**请注意**  可扩展交换机支持只有一个内部网络适配器。

 

<a href="" id="ndisswitchporttypesynthetic"></a>**NdisSwitchPortTypeSynthetic**  
这是配置为连接到的合成网络适配器的端口。 此适配器的 HYPER-V 子分区中运行来宾操作系统中公开。

**请注意**  合成网络适配器是一种虚拟机 (VM) 网络适配器。 此适配器在运行 Windows Vista 或更高版本的 Windows 来宾操作系统中公开。

 

<a href="" id="ndisswitchporttypeemulated"></a>**NdisSwitchPortTypeEmulated**  
此值指定配置为连接到仿真的网络适配器的端口。 在来宾操作系统中公开此适配器。

**请注意**  仿真的网络适配器是一种虚拟机网络适配器。 此适配器可以在来宾操作系统运行的 Windows XP 或非 Windows 操作系统中公开。

 

 

 





