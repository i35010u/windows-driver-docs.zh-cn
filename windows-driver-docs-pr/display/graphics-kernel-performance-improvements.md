---
title: 图形内核性能改进
description: 为了帮助评估图形硬件性能，Windows 显示驱动程序模型 (WDDM) 1.3 和更高版本的驱动程序都可以选择提供 GPU 处理的 API 调用的准确的计时信息。 此功能是从 Windows 8.1 新增功能。
ms.assetid: 8A2E1392-F0B4-4F5F-AFD9-DE8C6F3C2147
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8a984f3052b84b9c5aa5b2787b280151b7c4af2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379929"
---
# <a name="graphics-kernel-performance-improvements"></a>图形内核性能改进


为了帮助评估图形硬件性能，Windows 显示驱动程序模型 (WDDM) 1.3 和更高版本的驱动程序都可以选择提供 GPU 处理的 API 调用的准确的计时信息。 此功能是从 Windows 8.1 新增功能。

## <a name="span-idkernelperformancereferencespanspan-idkernelperformancereferencespanspan-idkernelperformancereferencespankernel-performance-reference"></a><span id="Kernel_performance_reference"></span><span id="kernel_performance_reference"></span><span id="KERNEL_PERFORMANCE_REFERENCE"></span>内核性能参考


这些参考主题介绍如何在您的显示微型端口驱动程序和用户模式显示驱动程序中实现此功能：

-   [*DxgkDdiCalibrateGpuClock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_calibrategpuclock)
-   [*DxgkDdiFormatHistoryBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_formathistorybuffer)
-   [**DXGK\_历史记录\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_history_buffer)
-   [**DXGK\_历史记录\_缓冲区\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_history_buffer_header)
-   [**DXGKARG\_CALIBRATEGPUCLOCK**](https://docs.microsoft.com/windows-hardware/drivers/display/)
-   [**DXGKARG\_FORMATHISTORYBUFFER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_formathistorybuffer)
-   [**DXGKARG\_HISTORYBUFFERPRECISION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_historybufferprecision)
-   [**驱动程序\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_driver_initialization_data) (新**DxgkDdiCalibrateGpuClock**并**DxgkDdiFormatHistoryBuffer**成员)
-   [**DXGK\_ALLOCATIONINFOFLAGS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfoflags) (新**HistoryBuffer**成员)
-   [**DXGK\_QUERYADAPTERINFOTYPE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ne-d3dkmddi-_dxgk_queryadapterinfotype) (新**DXGKQAITYPE\_HISTORYBUFFERPRECISION**常量值)
-   [*DxgkDdiCreateAllocation* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation) （请参见备注中的"Allocating 历史记录缓冲区"）

 

 





