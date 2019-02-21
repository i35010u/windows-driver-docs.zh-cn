---
title: 使用第 2 层筛选
description: 使用第 2 层筛选
ms.assetid: 679E6DE2-4EFB-44F6-936D-2BF611BC9726
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e3a1f9f4266ac5db031fcc78704879305ee30d6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524755"
---
# <a name="using-layer-2-filtering"></a>使用第 2 层筛选

Windows 8 和更高版本的 Windows 中支持第 2 层筛选。

此 WFP 功能允许对第 2 层 MAC 标头的字段进行筛选。 这些层调用发送或接收的主机计算机的所有数据包的每个数据包基础上。 层上的入站的路径和之后的出站路径上的数据包分段的数据包重组之前调用。 这些层从 NDIS 轻型筛选器 (LWF) 驱动程序访问。

> [!NOTE]
> 如果它还没有相应的筛选器在该图层，标注应不会插入在层的数据包。 注入[NET\_缓冲区\_列表](net-buffer-list-structure.md)结构应为与筛选器添加和删除协同使用，以确保存在相应的层中的筛选器时，才执行注入。 此外，提供程序不应删除属于其他提供程序的筛选器。 

本部分包括以下主题：

-   [注入 MAC 帧](#injecting-mac-frames)
-   [对链接的网络缓冲区列表进行分类](#classifying-chained-network-buffer-lists)
-   [WFP 第 2 层层和字段](#wfp-layer-2-layers-and-fields)

## <a name="injecting-mac-frames"></a>注入 MAC 帧

回调驱动程序调用[ **FwpsInjectMacReceiveAsync0** ](https://msdn.microsoft.com/library/windows/hardware/hh439588)函数以返回到第 2 层入站的数据路径，或为已截获 reinject 以前吸收的 MAC 帧 （或帧的克隆）注入的入站的数据路径中的自创新的 MAC 帧。

回调驱动程序调用[ **FwpsInjectMacSendAsync0** ](https://msdn.microsoft.com/library/windows/hardware/hh439593)函数以返回到第 2 层出站数据路径，或为已截获 reinject 以前吸收的 MAC 帧 （或帧的克隆）注入自创新的 MAC 帧中的出站数据路径。

*NetBufferLists*参数可以是[NET\_缓冲区\_列表](net-buffer-list-structure.md)链。 但是完成调用该函数，可以多次每完成一个段 (或单个 NET\_缓冲区\_列表) 的链。

插入的框架无法获取再次分类，如果最初分类的相同筛选器匹配的数据包。 因此，与在 IP 层上的标注，第 2 层标注必须还防止无限数据包检查通过调用[ **FwpsQueryPacketInjectionState0**](https://msdn.microsoft.com/library/windows/hardware/ff551202)。

此外，在其中注入的层必须有标注。 否则为您注入[NET\_缓冲区\_列表](net-buffer-list-structure.md)不会完成向完成函数中和 NET\_缓冲区\_列表将进一步在堆栈中向上。 在这种情况下，该行为不确定，因为 NDIS 将尝试进行传递注入的 NET\_缓冲区\_到堆栈中的下一个组件的列表。

[NET\_缓冲区\_列表](net-buffer-list-structure.md)**状态**成员包含堆栈注入状态结果。 堆栈注入状态结果是在 NET 中放入堆栈的状态\_缓冲区\_WFP 注入函数返回后列出**状态\_成功**。 应使用**NT\_成功**宏，以查看堆栈注入状态**状态**成员。 如果**状态**值是**状态\_成功**，注入成功，但任何进一步的信息。 **状态**成员值大于**状态\_成功**意味着注入成功，但可能存在有关应视为注入的详细信息。 **状态**成员的值小于**状态\_成功**注入失败的原因中指定的平均值**状态**成员。

## <a name="classifying-chained-network-buffer-lists"></a>对链接的网络缓冲区列表进行分类

默认情况下，标注驱动程序可以仅分类网络缓冲区列表分别。 但是，标注驱动程序可以对分类[NET\_缓冲区\_列表](net-buffer-list-structure.md)链接为提高性能，如果是这样以下两个：

-   指定**FWP\_标注\_标志\_允许\_L2\_批处理\_分类**标志中**标志**的成员[ **FWPS\_CALLOUT2** ](https://msdn.microsoft.com/library/windows/hardware/hh439700)结构。
-   注册[ *classifyFn2* ](https://msdn.microsoft.com/library/windows/hardware/hh439337)函数可以对分类[NET\_缓冲区\_列表](net-buffer-list-structure.md)链。

> [!WARNING]
> 但是，如果未设置标注驱动程序**FWP_CALLOUT_FLAG_ALLOW_L2_BATCH_CLASSIFY**标志，它无法使用以下函数来修改 NET_BUFFER_LISTs。
> 
> - [FwpsReferenceNetBufferList0](https://msdn.microsoft.com/library/windows/hardware/ff551206)
> - [FwpsDereferenceNetBufferList0](https://msdn.microsoft.com/library/windows/hardware/ff551159)
> - [FwpsAllocateCloneNetBufferList0](https://msdn.microsoft.com/library/windows/hardware/ff551134)
> - [FwpsFreeCloneNetBufferList0](https://msdn.microsoft.com/library/windows/hardware/ff551170)
>
> 设置此标志， **FwpsAllocateCloneNetBufferList0**将始终返回**INVALID_PARAMETER**错误。 这可能会意外导致第三方标注驱动程序无法进行管理的引用计数的 NET\_缓冲区\_列表，从而导致发送和接收操作停止。

## <a name="wfp-layer-2-layers-and-fields"></a>WFP 第 2 层层和字段

运行时筛选层标识符的虚拟交换机筛选包括：

**FWPS\_LAYER\_INBOUND\_MAC\_FRAME\_ETHERNET**

**FWPS\_LAYER\_OUTBOUND\_MAC\_FRAME\_ETHERNET**

**FWPS\_LAYER\_INBOUND\_MAC\_FRAME\_NATIVE**

**FWPS\_LAYER\_OUTBOUND\_MAC\_FRAME\_NATIVE**

虚拟交换机筛选的数据字段标识符包括：

[**FWPS\_FIELDS\_INBOUND\_MAC\_FRAME\_ETHERNET**](https://msdn.microsoft.com/library/windows/hardware/ff551291)

[**FWPS\_FIELDS\_OUTBOUND\_MAC\_FRAME\_ETHERNET**](https://msdn.microsoft.com/library/windows/hardware/ff551334)

[**FWPS\_FIELDS\_INBOUND\_MAC\_FRAME\_NATIVE**](https://msdn.microsoft.com/library/windows/hardware/hh439728)

[**FWPS\_FIELDS\_OUTBOUND\_MAC\_FRAME\_NATIVE**](https://msdn.microsoft.com/library/windows/hardware/hh439757)

 

 





