---
title: 图形内核性能改进
description: 为了帮助评估图形硬件性能，Windows 显示驱动程序模型（WDDM）1.3 和更高版本的驱动程序可以选择为 GPU 处理的 API 调用提供准确的计时信息。 此功能是从 Windows 8.1 开始的新功能。
ms.assetid: 8A2E1392-F0B4-4F5F-AFD9-DE8C6F3C2147
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c10f6e4516b1861964f8f5e9a179353eb41ffd9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839672"
---
# <a name="graphics-kernel-performance-improvements"></a>图形内核性能改进


为了帮助评估图形硬件性能，Windows 显示驱动程序模型（WDDM）1.3 和更高版本的驱动程序可以选择为 GPU 处理的 API 调用提供准确的计时信息。 此功能是从 Windows 8.1 开始的新功能。

## <a name="span-idkernel_performance_referencespanspan-idkernel_performance_referencespanspan-idkernel_performance_referencespankernel-performance-reference"></a><span id="Kernel_performance_reference"></span><span id="kernel_performance_reference"></span><span id="KERNEL_PERFORMANCE_REFERENCE"></span>内核性能参考


以下参考主题介绍如何在显示微型端口驱动程序和用户模式显示驱动程序中实现此功能：

-   [*DxgkDdiCalibrateGpuClock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_calibrategpuclock)
-   [*DxgkDdiFormatHistoryBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_formathistorybuffer)
-   [**DXGK\_历史记录\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_history_buffer)
-   [**DXGK\_HISTORY\_缓冲器\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_history_buffer_header)
-   [**DXGKARG\_CALIBRATEGPUCLOCK**](https://docs.microsoft.com/windows-hardware/drivers/display/)
-   [**DXGKARG\_FORMATHISTORYBUFFER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_formathistorybuffer)
-   [**DXGKARG\_HISTORYBUFFERPRECISION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_historybufferprecision)
-   [**驱动\_\_数据初始化的驱动程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_driver_initialization_data)（new **DxgkDdiCalibrateGpuClock**和**DxgkDdiFormatHistoryBuffer**成员）
-   [**DXGK\_ALLOCATIONINFOFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfoflags) （new **HistoryBuffer**成员）
-   [**DXGK\_QUERYADAPTERINFOTYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ne-d3dkmddi-_dxgk_queryadapterinfotype) （new **DXGKQAITYPE\_HISTORYBUFFERPRECISION**常数值）
-   [*DxgkDdiCreateAllocation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation) （请参阅 "备注" 中的 "分配历史缓冲区"）

 

 





