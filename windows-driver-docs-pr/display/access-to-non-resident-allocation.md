---
title: 访问非驻留分配
description: GPU 访问非常驻分配是非法的，将导致为生成错误的应用程序删除设备。
ms.assetid: 698ECD53-861A-4750-B33C-DF0611B87829
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f4961bb11378654c5d1c7219bfe11f900161a9e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839086"
---
# <a name="span-iddisplayaccess_to_non-resident_allocationspanaccess-to-non-resident-allocation"></a><span id="display.access_to_non-resident_allocation"></span>访问非居民分配


图形处理单元（GPU）访问非常驻分配是非法的，将导致为生成错误的应用程序删除设备。

处理此类无效访问的两种不同模型依赖于出错引擎是否支持 GPU 虚拟寻址：

-   对于不支持 GPU 虚拟寻址的引擎，并使用 "分配和修补程序位置" 列表修补内存引用，当用户模式驱动程序提交的分配列表引用了不在设备（即用户模式驱动程序没有在该分配上调用[*MakeResidentCb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_makeresidentcb) ）。 出现这种情况时，图形内核会将出错的上下文/设备置于错误中。
-   对于支持 GPU 虚拟寻址但访问无效的 GPU 虚拟地址的引擎，原因可能是虚拟地址没有分配，或者没有有效的分配，但尚未将其驻留，所以 GPU 应该引发中断形式的不可恢复的页错误。 发生页面故障中断时，内核模式驱动程序将需要通过新的页面错误通知将错误转发到图形内核。 收到此通知后，图形内核会在发生错误的引擎上启动引擎重置，并使错误的上下文/设备出错。 如果引擎重置失败，则图形内核会将错误提升为完整的适配器范围超时检测和恢复（TDR）。

 

 





