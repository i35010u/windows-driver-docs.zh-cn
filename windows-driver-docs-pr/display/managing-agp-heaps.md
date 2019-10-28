---
title: 管理 AGP 堆
description: 管理 AGP 堆
ms.assetid: edeed3bc-c107-4286-9d5a-7fdef89cc4e1
keywords:
- 堆 WDK DirectDraw
- 显示内存 WDK DirectDraw，堆
- 非本地显示内存 WDK DirectDraw，堆
- AGP WDK DirectDraw，堆
- 绘制 AGP 支持 WDK DirectDraw，堆
- DirectDraw AGP 支持 WDK Windows 2000 显示，堆
- 内存 WDK DirectDraw AGP、堆
- GetDriverInfo2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb4e562657bf9cf299c47fc183959ccc29f84912
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840584"
---
# <a name="managing-agp-heaps"></a>管理 AGP 堆


## <span id="ddk_managing_agp_heaps_gg"></span><span id="DDK_MANAGING_AGP_HEAPS_GG"></span>


**本主题仅适用于基于 Windows NT 的操作系统。**

驱动程序可以使用它从 DirectX 运行时接收的通知来管理 AGP 堆。 驱动程序接收来自运行时的通知， **GetDriverInfo2**请求使用以下值：

-   D3DGDI2\_类型\_推迟\_AGP\_感知

-   D3DGDI2\_类型\_\_延迟\_AGP

-   D3DGDI2\_类型\_推迟\_AGP\_释放

有关**GetDriverInfo2**请求的详细信息，请参阅[支持 GetDriverInfo2](supporting-getdriverinfo2.md)。

当创建显示设备时，显示驱动程序将接收具有 D3DGDI2\_类型的**GetDriverInfo2**请求\_延迟\_AGP\_感知通知，驱动程序将使用该通知来确定是否应禁用其他处理 AGP 堆并改为使用 D3DGDI2\_类型的机制\_免费\_延迟\_AGP 和 D3DGDI2\_类型\_延迟\_AGP\_释放运行时随后发送的通知。 在 D3DGDI2 中\_键入\_推迟\_AGP\_感知通知，DirectX 运行时提供指向[**DD\_延迟\_AGP\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_dd_deferred_agp_aware_data) **的指针，\_在**[**DD\_GETDRIVERINFODATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_getdriverinfodata)数据结构。

该驱动程序有时会接收具有 D3DGDI2\_类型的**GetDriverInfo2**请求\_延迟\_AGP\_在显示模式发生变化之前释放通知。 仅当运行时执行显示模式更改时，DirectX 运行时才会发送此通知。 驱动程序应检查进程的进程标识符（PID），该进程会根据创建该图面的进程来销毁该图面。 如果 Pid 不同，驱动程序不应销毁 AGP 内存的用户模式映射，因为应用程序可能仍在使用内存。

当进程中的所有显示设备使用表面、纹理、顶点缓冲区和索引缓冲区停止时，驱动程序将接收具有 D3DGDI2\_类型的**GetDriverInfo2**请求\_免费\_延迟\_AGP 通知在显示模式发生更改时锁定。 通知会通知驱动程序，它可以安全地销毁 AGP 内存的所有用户模式映射。

在 D3DGDI2 中\_键入\_推迟\_AGP\_释放和 D3DGDI2\_类型\_\_免费\_AGP 通知，运行时提供指向[**DD\_免费\_延迟 @no__** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_dd_free_deferred_agp_data)在 DD\_GETDRIVERINFODATA 数据结构的**lpvData**成员中 T_12_ AGP\_数据结构。 DD\_免费\_的**dwProcessId**成员\_AGP\_数据指定销毁 AGP 内存的进程的 PID。

请注意，应用程序可以终止，而不会在运行时向驱动程序发送 D3DGDI2\_类型\_免费\_延迟\_AGP 通知。 因此，当驱动程序收到对其[**D3dDestroyDDLocal**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_destroyddlocal)函数的调用时，该驱动程序应释放 AGP 内存的所有用户模式映射。

 

 





