---
title: 访问非驻留分配
description: GPU 访问不是常驻分配是非法的并会导致生成错误的应用程序中删除的设备。
ms.assetid: 698ECD53-861A-4750-B33C-DF0611B87829
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e04cdf46f6401eeb871296783540e178451b1375
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373597"
---
# <a name="span-iddisplayaccesstonon-residentallocationspanaccess-to-non-resident-allocation"></a><span id="display.access_to_non-resident_allocation"></span>对非驻留分配的访问


图形处理单元 (GPU) 访问不是常驻分配是非法的并会导致生成错误的应用程序中删除的设备。

有两个不同的模型的处理取决于是否出错的引擎支持 GPU 虚拟寻址或不访问此类无效：

-   对于引擎，它不支持 GPU 虚拟寻址，使用的分配和修补程序修补程序内存引用到的位置列表，无效的访问发生在用户模式驱动程序提交的分配列表引用分配，这不是驻留在设备 (即称为用户模式驱动程序尚未[ *MakeResidentCb* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_makeresidentcb)在该分配)。 此操作时，图形内核会以错误放置有故障的上下文/设备。
-   对于执行支持 GPU 虚拟寻址，但访问无效的 GPU 虚拟地址的引擎，或者因为后面的虚拟地址未分配或没有有效分配但尚未进行其常驻，GPU 应引发形式的中断发生了不可恢复的页面错误。 当发生页面故障中断时，内核模式驱动程序将需要转发到图形内核通过新的页错误通知错误。 在接收时此类通知，图形内核将启动一个引擎重置上出错引擎并将有故障的上下文/设备置于错误。 如果引擎重置失败，图形内核将升级到完整适配器宽超时检测和恢复 (TDR) 错误。

 

 





