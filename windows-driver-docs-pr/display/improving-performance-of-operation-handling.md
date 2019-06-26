---
title: 改进操作处理的性能
description: 改进操作处理的性能
ms.assetid: 14b5aa90-15ee-40c6-8f5b-e776b07932ab
keywords:
- Direct3D WDK Windows 2000 显示，操作代码
- 操作代码 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1675253e8379b11b4041b6b20e599d9e978413ce
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383933"
---
# <a name="improving-performance-of-operation-handling"></a>改进操作处理的性能


## <span id="ddk_improving_performance_of_operation_handling_gg"></span><span id="DDK_IMPROVING_PERFORMANCE_OF_OPERATION_HANDLING_GG"></span>


若要提高显示器驱动程序的性能，应实现您的驱动程序来呈现图形基元和处理状态更改时观察以下项：

-   DirectX 运行时筛选冗余请求来设置呈现状态参数。 也就是说，如果应用程序调用**IDirect3DDevice8::SetRenderState**方法多次来设置相同的设备呈现状态参数之前它将呈现一个场景，运行时，筛选出的冗余调用，并且您的驱动程序的[**D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)函数只能接收一个请求以将此特定的呈现状态参数设置。 因此，无需实现您的驱动程序执行此筛选操作。

-   它只是绘制基元之前并不每当它收到操作请求，您的驱动程序应只写入到呈现状态寄存器 ([**D3DHAL\_DP2OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ne-d3dhal-_d3dhal_dp2operation))。

有关详细信息**IDirect3DDevice8::SetRenderState**，请参阅 Direct3D SDK 文档。

 

 





