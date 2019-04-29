---
title: 使用数据包标记
description: 使用数据包标记
ms.assetid: a151256b-d69f-4abb-bf68-644f157dfdd7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec219e75870164c7a5810431868525d0b174302c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323327"
---
# <a name="using-packet-tagging"></a>使用数据包标记


标注驱动程序可以标记感兴趣的数据包，并接收到标记的数据包会发生的事件的通知。 Windows 7 和更高版本的 Windows 中支持数据包标记。

若要使用数据包标记，标注驱动程序必须实现[ *FWPS\_NET\_缓冲区\_列表\_通知\_FN0* ](https://msdn.microsoft.com/library/windows/hardware/ff552406)或[*FWPS\_NET\_缓冲区\_列表\_通知\_FN1* ](https://msdn.microsoft.com/library/windows/hardware/hh451260)回调函数。 此函数将接收所有标记的数据包的状态通知。 标注驱动程序可以标记单个数据包之前，必须通过调用获取的特殊上下文标记[ **FwpsNetBufferListGetTagForContext0**](https://msdn.microsoft.com/library/windows/hardware/ff551192)。 标注驱动程序可以使用相同的上下文标记的某些或全部有标记的数据包。 例如，标注驱动程序可能会区分使用不同的上下文标记的标记数据包的类型。

对数据包进行标记，标注驱动程序使用[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构。 标注驱动程序会调用[ **FwpsNetBufferListAssociateContext0** ](https://msdn.microsoft.com/library/windows/hardware/ff551191)到单个标记**NET\_缓冲区\_列表**结构。 标注驱动程序将与包相关联的上下文是一个任意的无符号的 64 位值。 当触发事件时， [ *FWPS\_NET\_缓冲区\_列表\_通知\_FN0* ](https://msdn.microsoft.com/library/windows/hardware/ff552406)或[ *FWPS\_NET\_缓冲区\_列表\_通知\_FN1* ](https://msdn.microsoft.com/library/windows/hardware/hh451260)回调将上下文传递作为输入参数，以便可以标注驱动程序标识单个标记的数据包。 不使用或由筛选引擎计算上下文。 它是仅传递给该回调用于标注驱动程序。

上下文是从有标记的数据包后自动删除数据包将保留堆栈。 但是，如果数据包永远不会进入 TCP/IP 堆栈 — 例如，对于 NDIS 筛选驱动程序 — 上下文将需要手动删除通过调用[ **FwpsNetBufferListRemoveContext0** ](https://msdn.microsoft.com/library/windows/hardware/ff551194)与*netBufferList*参数设置为**NULL**。

如果一个标注需要提前中止标记操作，可以通过调用删除上下文[ **FwpsNetBufferListRemoveContext0**](https://msdn.microsoft.com/library/windows/hardware/ff551194)。 移除上下文通常会触发**FWPS\_NET\_缓冲区\_列表\_上下文\_已删除**事件。 有关可以触发的事件的详细信息，请参阅[ **FWPS\_NET\_缓冲区\_列表\_事件\_TYPE0** ](https://msdn.microsoft.com/library/windows/hardware/ff552403)枚举。 在某些情况下不会触发事件，例如数据包永远不会进入时的 TCP/IP 堆栈进行处理。

当克隆带标记的数据包时，标注驱动程序可以移动或复制到克隆数据包的上下文。 若要移动的上下文 （如果克隆），标注驱动程序必须调用[ **FwpsNetBufferListRetrieveContext0** ](https://msdn.microsoft.com/library/windows/hardware/ff551196)与*removeContext*参数设置为 **，则返回 TRUE**。 然后上下文可以是与新的数据包相关联。 复制 （在情况下重复） 的上下文的过程是相同，只不过*removeContext*的参数**FwpsNetBufferListRetrieveContext0**必须设置为**FALSE**.

可以从检索标记来自 TCP/IP 层数据包[NDIS 筛选器驱动程序](ndis-filter-drivers2.md)。 反过来也是如此。 不可用来自除数据段指定的任何数据包的流层数据包标记。

标注驱动程序可以检索的上下文之外的数据包[ *FWPS\_NET\_缓冲区\_列表\_通知\_FN0* ](https://msdn.microsoft.com/library/windows/hardware/ff552406)或[ *FWPS\_NET\_缓冲区\_列表\_通知\_FN1* ](https://msdn.microsoft.com/library/windows/hardware/hh451260)函数通过调用[ **FwpsNetBufferListRetrieveContext0**](https://msdn.microsoft.com/library/windows/hardware/ff551196)。 通常情况下，标注驱动程序将检索的上下文中其[classifyFn](https://msdn.microsoft.com/library/windows/hardware/ff544887)回调。

## <a name="related-topics"></a>相关主题


[classifyFn](https://msdn.microsoft.com/library/windows/hardware/ff544887)

[**FWPS\_NET\_BUFFER\_LIST\_EVENT\_TYPE0**](https://msdn.microsoft.com/library/windows/hardware/ff552403)

[*FWPS\_NET\_BUFFER\_LIST\_NOTIFY\_FN0*](https://msdn.microsoft.com/library/windows/hardware/ff552406)

[*FWPS\_NET\_BUFFER\_LIST\_NOTIFY\_FN1*](https://msdn.microsoft.com/library/windows/hardware/hh451260)

[**FwpsNetBufferListAssociateContext0**](https://msdn.microsoft.com/library/windows/hardware/ff551191)

[**FwpsNetBufferListGetTagForContext0**](https://msdn.microsoft.com/library/windows/hardware/ff551192)

[**FwpsNetBufferListRemoveContext0**](https://msdn.microsoft.com/library/windows/hardware/ff551194)

[**FwpsNetBufferListRetrieveContext0**](https://msdn.microsoft.com/library/windows/hardware/ff551196)

[**NET\_BUFFER\_LIST**](https://msdn.microsoft.com/library/windows/hardware/ff568388)

[NDIS 筛选器驱动程序](ndis-filter-drivers2.md)

 

 






