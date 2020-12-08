---
title: 改进操作处理的性能
description: 改进操作处理的性能
keywords:
- Direct3D WDK Windows 2000 显示，操作代码
- 操作代码 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 629b5055c973329cc29e6a61cd2c2e7aba3f4c16
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839313"
---
# <a name="improving-performance-of-operation-handling"></a>改进操作处理的性能


## <span id="ddk_improving_performance_of_operation_handling_gg"></span><span id="DDK_IMPROVING_PERFORMANCE_OF_OPERATION_HANDLING_GG"></span>


若要改善显示器驱动程序的性能，你应该在实现驱动程序以呈现图形基元和处理状态更改时看到以下各项：

-   DirectX 运行时筛选冗余请求，以设置呈现状态参数。 也就是说，如果应用程序多次调用 **IDirect3DDevice8：： SetRenderState** 方法以在呈现场景之前设置相同的设备呈现器状态参数，则运行时将筛选出冗余调用，并且驱动程序的 [**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) 函数只接收一个设置此特定呈现状态参数的请求。 因此，您无需实现您的驱动程序即可执行此筛选操作。

-   你的驱动程序只应在绘制基元之前写入呈现状态寄存器，而不会在每次收到 ([**D3DHAL \_ DP2OPERATION**](/windows-hardware/drivers/ddi/d3dhal/ne-d3dhal-_d3dhal_dp2operation)) 的操作请求时进行写入。

有关 **IDirect3DDevice8：： SetRenderState** 的详细信息，请参阅 Direct3D SDK 文档。

 

