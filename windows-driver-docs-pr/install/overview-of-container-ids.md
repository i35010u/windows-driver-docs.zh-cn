---
title: 容器 ID 概述
description: 容器 ID 概述
ms.assetid: fb7a4a31-01f9-4f7e-a35c-9076c7d73a29
keywords:
- 容器 Id WDK，关于
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3ca4c823eeb57be16b15bb94eee1326045a37e8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330259"
---
# <a name="overview-of-container-ids"></a>容器 ID 概述


在 Windows 系列操作系统，设备基本上是通信的其中的每个表示功能的终结点，使某种形式的与设备功能的设备实例的集合。

术语*设备节点*(*devnode*) 是指*驱动程序堆栈*对于此类功能终结点，以及描述终结点的属性并将其关联的状态。 例如，多功能设备支持打印机、 扫描仪和传真功能，可以有多个 devnodes，一个用于在设备中每个功能终结点。

在 Windows 7 之前每个功能的终结点必须与之相关联 devnode。 Windows 平台组件和第三方应用程序可查询 devnodes 设备状态和信息，并且可以与设备硬件通信但功能的终结点公开的接口。

对于单函数设备，单个 devnode 包含与设备的功能的终结点相关的所有信息。 同样，多功能设备有多个 devnodes 与每个设备的功能的终结点相关联。 但是，Windows 无法识别的 devnodes 一组来自同一个物理设备。 每个 devnode 属于同一个多功能设备不包括任何，插 (PnP) 管理器进行几个 devnodes 分组为单个设备的标识信息。 因此，不可能有设备并在单个物理设备提供的函数的整体视图。

操作系统从 Windows 7 开始，使用新的 ID (*容器 ID*) 进行分组源自的一个或多个 devnodes 以及属于特定的物理设备的每个实例。 容器 ID 是每个 devnode 的属性，指定通过全局唯一标识符 (*GUID*) 值。

在计算机中安装的物理设备的每个实例都是唯一的容器 id。 表示该实例的物理设备上的函数的所有 devnodes 都共享相同的容器 id。 下图显示了该关系的一个示例。

![关系图多功能设备的 devnodes 演示容器的 id](images/containerid-1.png)

还有一个容器 ID 为总线驱动程序的特殊含义：它被定义为 NULL_GUID: {00000000-0000-0000-0000-000000000000}。

一般情况下，不会返回 NULL_GUID 作为默认情况下时报告的容器 id。 相反，是否处理 IRP_MN_QUERY_ID BusQueryContainerIDs 用例并由 PnP 应用其默认逻辑。

当返回 NULL_GUID 作为容器 ID，总线驱动程序声明到即插即用设备必须不是任何容器，因此返回 NULL_GUID 适合仅在非常特殊的情况下的一部分。 例如， *devnode*例如卷设备可能跨多个容器中的多个磁盘，但不是属于任何容器。 此类设备将出现[ **DEVPKEY_Device_BaseContainerId** ](https://msdn.microsoft.com/library/windows/hardware/ff542360)等于 NULL_GUID，并且它不会有[ **DEVPKEY_Device_ContainerId** ](https://msdn.microsoft.com/library/windows/hardware/ff542400)根本。

除了非常特殊的情况下，总线驱动程序应永远不会返回 NULL_GUID 时报告的硬件设备和总线驱动程序应防止报告 NULL_GUID 值从其总线的硬件故障。 在这些情况下总线驱动程序应威胁这作为设备错误，或者将它视为像设备未报告的值。

 

 





