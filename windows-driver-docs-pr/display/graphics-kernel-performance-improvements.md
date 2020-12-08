---
title: 图形内核性能改进
description: 为帮助评估图形硬件性能，Windows 显示驱动程序模型 (WDDM) 1.3 及更高版本的驱动程序可以选择为 GPU 处理的 API 调用提供准确的计时信息。 此功能是从 Windows 8.1 开始的新功能。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76bf61ba53e2939114ca58b5fbb2d12270c03307
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827303"
---
# <a name="graphics-kernel-performance-improvements"></a>图形内核性能改进


为帮助评估图形硬件性能，Windows 显示驱动程序模型 (WDDM) 1.3 及更高版本的驱动程序可以选择为 GPU 处理的 API 调用提供准确的计时信息。 此功能是从 Windows 8.1 开始的新功能。

## <a name="span-idkernel_performance_referencespanspan-idkernel_performance_referencespanspan-idkernel_performance_referencespankernel-performance-reference"></a><span id="Kernel_performance_reference"></span><span id="kernel_performance_reference"></span><span id="KERNEL_PERFORMANCE_REFERENCE"></span>内核性能参考


以下参考主题介绍如何在显示微型端口驱动程序和用户模式显示驱动程序中实现此功能：

-   [*DxgkDdiCalibrateGpuClock*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_calibrategpuclock)
-   [*DxgkDdiFormatHistoryBuffer*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_formathistorybuffer)
-   [**DXGK \_ 历史记录 \_ 缓冲区**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_history_buffer)
-   [**DXGK \_ 历史记录 \_ 缓冲区 \_ 标头**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_history_buffer_header)
-   [**DXGKARG \_ CALIBRATEGPUCLOCK**](./index.md)
-   [**DXGKARG \_ FORMATHISTORYBUFFER**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_formathistorybuffer)
-   [**DXGKARG \_ HISTORYBUFFERPRECISION**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_historybufferprecision)
-   [**驱动程序 \_ (\_**](/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_driver_initialization_data) 新的 **DxgkDdiCalibrateGpuClock** 和 **DxgkDdiFormatHistoryBuffer** 成员的初始化数据) 
-   [**DXGK \_ALLOCATIONINFOFLAGS**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfoflags) (New **HistoryBuffer** 成员) 
-   [**DXGK \_QUERYADAPTERINFOTYPE**](/windows-hardware/drivers/ddi/d3dkmddi/ne-d3dkmddi-_dxgk_queryadapterinfotype) (New **DXGKQAITYPE \_ HISTORYBUFFERPRECISION** 常数值) 
-   [*DxgkDdiCreateAllocation*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation) (参阅 "备注" 中的 "分配历史缓冲区") 

 

