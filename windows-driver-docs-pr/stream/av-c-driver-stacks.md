---
title: AV/C 驱动程序堆栈
description: AV/C 驱动程序堆栈
ms.assetid: 7745c466-d16e-4af3-be09-7af01777b033
keywords:
- AV/C WDK，驱动程序堆栈
- 驱动程序堆栈 WDK AV/C
- 堆栈 WDK AV/C
- Avc.sys 功能驱动程序 WDK，驱动程序堆栈
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e2bb1dbb60b82b71b1f971efc250810cde13899
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554282"
---
# <a name="avc-driver-stacks"></a>AV/C 驱动程序堆栈





添加到和从 IEEE 1394 总线删除 AV/C 的设备时，插管理器加载和卸载相应的子单元驱动程序。 供应商实现 AV/C 子单元的独特功能通过编写一个子单元驱动程序，Windows 将加载到上面的 IEEE 1394 堆栈*Avc.sys*。 *Avc.sys*使用提供的基础的 IEEE 1394 和 IEC 61883 驱动程序功能来控制设备，还可以连接并管理插入。 有关这些基础驱动程序堆栈的详细信息，请参阅[的 IEEE 1394 驱动程序堆栈](https://msdn.microsoft.com/library/windows/hardware/ff538867)并[IEC 61883 客户端驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff537188)。

对等方驱动程序堆栈为外部 C AV/设备上的子单元连接。 与此相反，虚拟驱动程序堆栈是公开到其他 AV/C 连接设备的 IEEE 1394 总线上的 AV/C 设备的计算机的单独的驱动程序堆栈。 下图演示了两个不同*Avc.sys*堆栈。

![说明的单独的对等子单元和虚拟子单元堆栈的关系图](images/avcdiag.gif)

在驱动程序的堆栈都*1394ohci.sys*并*1394bus.sys*。 这些驱动程序提供基本的 IEEE 1394 总线基础结构支持。 在系统中有这些驱动程序为每个物理的 IEEE 1394 适配器的实例。

堆叠在其上面*1394ohci.sys*并*1394bus.sys*是*是 61883.sys*。 实例*是 61883.sys* IEEE 1394 总线上每个 IEC 61883 启用节点。 在驱动程序*是 61883.sys* IEC 61883 协议提供了以下支持：

-   连接管理协议 (CMP) IEC 61883 1

-   常见同步数据包 (CIP) IEC 61883 1

-   函数控制协议 (FCP) IEC 61883 1

之上堆积*是 61883.sys*是*Avc.sys*、 它支持 AV/C 协议，每个 AV/C 在设备上，活动的子单元连接插枚举和 AV/C 子单元插入的连接管理和控制。 有关即插即用连接和格式管理的详细信息，请参阅[AV/C 子单元插入连接和格式管理](av-c-subunit-plug-connection-and-format-management.md)。

子单元驱动程序堆叠在其上面*Avc.sys*。 这是供应商在其中实施仅适用于其 AV/C 子单元的功能的层。 通常，对于 AV/C 子单元每个物理实例，则该子单元的驱动程序的相应实例。 也就是说，每个设备标识符 (ID) 表示的实例*Avc.sys*。 但是， *Avc.sys*允许重写此行为基于***供应商***和/或***模型***AV/C 单元的设备标识符的字段。 有关详细信息***供应商***，***模型***， ***SubunitType***，以及***SubunitID***设备标识符字符串生成的字段通过*Avc.sys*请参阅[AV/C 设备 Id](av-c-device-identifiers.md)。

 

 




