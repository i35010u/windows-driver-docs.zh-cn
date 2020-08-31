---
title: 访问非驻留分配
description: GPU 访问非常驻分配是非法的，将导致为生成错误的应用程序删除设备。
ms.assetid: 698ECD53-861A-4750-B33C-DF0611B87829
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f8c12e95508698c4eed28fd07e1cf8ec6078a65
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063196"
---
# <a name="span-iddisplayaccess_to_non-resident_allocationspanaccess-to-non-resident-allocation"></a><span id="display.access_to_non-resident_allocation"></span>访问非驻留分配


图形处理单元 (GPU) 访问非常驻分配是非法的，将导致为生成错误的应用程序删除设备。

处理此类无效访问的两种不同模型依赖于出错引擎是否支持 GPU 虚拟寻址：

-   对于不支持 GPU 虚拟寻址的引擎，并使用 "分配和修补程序位置" 列表修补内存引用，当用户模式驱动程序提交的分配列表引用了不在设备上的分配时，将发生无效的访问 (即，用户模式驱动程序没有在该分配) 上调用 [*MakeResidentCb*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_makeresidentcb) 。 出现这种情况时，图形内核会将出错的上下文/设备置于错误中。
-   对于支持 GPU 虚拟寻址但访问无效的 GPU 虚拟地址的引擎，因为在虚拟地址之后没有分配，或者没有有效的分配，但尚未进行驻留，所以 GPU 应以中断的形式引发不可恢复的页错误。 发生页面故障中断时，内核模式驱动程序将需要通过新的页面错误通知将错误转发到图形内核。 收到此通知后，图形内核会在发生错误的引擎上启动引擎重置，并使错误的上下文/设备出错。 如果引擎重置失败，则图形内核会将错误提升为完整的适配器范围超时检测和恢复 (TDR) 。

 

