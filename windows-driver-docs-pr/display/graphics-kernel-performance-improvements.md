---
title: 图形内核性能改进
description: 为了帮助评估图形硬件性能，Windows 显示驱动程序模型 (WDDM) 1.3 和更高版本的驱动程序都可以选择提供 GPU 处理的 API 调用的准确的计时信息。 此功能是从 Windows 8.1 新增功能。
ms.assetid: 8A2E1392-F0B4-4F5F-AFD9-DE8C6F3C2147
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec999bf2141e3683cd8cb206f236e6d41f140e64
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323809"
---
# <a name="graphics-kernel-performance-improvements"></a>图形内核性能改进


为了帮助评估图形硬件性能，Windows 显示驱动程序模型 (WDDM) 1.3 和更高版本的驱动程序都可以选择提供 GPU 处理的 API 调用的准确的计时信息。 此功能是从 Windows 8.1 新增功能。

## <a name="span-idkernelperformancereferencespanspan-idkernelperformancereferencespanspan-idkernelperformancereferencespankernel-performance-reference"></a><span id="Kernel_performance_reference"></span><span id="kernel_performance_reference"></span><span id="KERNEL_PERFORMANCE_REFERENCE"></span>内核性能参考


这些参考主题介绍如何在您的显示微型端口驱动程序和用户模式显示驱动程序中实现此功能：

-   [*DxgkDdiCalibrateGpuClock*](https://msdn.microsoft.com/library/windows/hardware/dn467321)
-   [*DxgkDdiFormatHistoryBuffer*](https://msdn.microsoft.com/library/windows/hardware/dn439360)
-   [**DXGK\_历史记录\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/dn439361)
-   [**DXGK\_历史记录\_缓冲区\_标头**](https://msdn.microsoft.com/library/windows/hardware/dn439362)
-   [**DXGKARG\_CALIBRATEGPUCLOCK**](https://msdn.microsoft.com/library/windows/hardware/dn467320)
-   [**DXGKARG\_FORMATHISTORYBUFFER**](https://msdn.microsoft.com/library/windows/hardware/dn439358)
-   [**DXGKARG\_HISTORYBUFFERPRECISION**](https://msdn.microsoft.com/library/windows/hardware/dn439359)
-   [**驱动程序\_初始化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff556169) (新**DxgkDdiCalibrateGpuClock**并**DxgkDdiFormatHistoryBuffer**成员)
-   [**DXGK\_ALLOCATIONINFOFLAGS** ](https://msdn.microsoft.com/library/windows/hardware/ff560966) (新**HistoryBuffer**成员)
-   [**DXGK\_QUERYADAPTERINFOTYPE** ](https://msdn.microsoft.com/library/windows/hardware/ff562010) (新**DXGKQAITYPE\_HISTORYBUFFERPRECISION**常量值)
-   [*DxgkDdiCreateAllocation* ](https://msdn.microsoft.com/library/windows/hardware/ff559606) （请参见备注中的"Allocating 历史记录缓冲区"）

 

 





