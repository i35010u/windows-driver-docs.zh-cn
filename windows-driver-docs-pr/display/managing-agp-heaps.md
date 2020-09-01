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
ms.openlocfilehash: 7ac4d6410890befaf048a26497ab254654cee67a
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065730"
---
# <a name="managing-agp-heaps"></a>管理 AGP 堆


## <span id="ddk_managing_agp_heaps_gg"></span><span id="DDK_MANAGING_AGP_HEAPS_GG"></span>


**本主题仅适用于基于 Windows NT 的操作系统。**

驱动程序可以使用它从 DirectX 运行时接收的通知来管理 AGP 堆。 驱动程序接收来自运行时的通知， **GetDriverInfo2** 请求使用以下值：

-   D3DGDI2 \_ 类型已 \_ 延迟 \_ AGP \_ 识别

-   D3DGDI2 \_ 类型 \_ 免费 \_ 延迟 \_ AGP

-   D3DGDI2 \_ 类型 \_ 延迟 \_ AGP \_ 释放

有关 **GetDriverInfo2** 请求的详细信息，请参阅 [支持 GetDriverInfo2](supporting-getdriverinfo2.md)。

当创建显示设备时，显示驱动程序将收到具有**GetDriverInfo2** D3DGDI2 \_ 类型 "延迟 AGP 感知通知" 的 GetDriverInfo2 请求 \_ \_ \_ ，驱动程序使用该通知来确定它是否应禁用其他处理 AGP 堆的机制，而改用 D3DGDI2 \_ 类型 " \_ 自由 \_ 延迟 agp" 和 "D3DGDI2 类型" " \_ \_ \_ 延迟 \_ agp \_ 释放运行时随后发送的通知"。 在 D3DGDI2 \_ 类型 " \_ 延迟 \_ agp \_ 识别通知" 中，DirectX 运行时提供指向[**Dd \_ GETDRIVERINFODATA**](/windows/desktop/api/ddrawint/ns-ddrawint-_dd_getdriverinfodata)数据结构的**lpvData**成员中[**dd \_ 延迟 \_ AGP \_ 感知 \_ 数据**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_dd_deferred_agp_aware_data)结构的指针。

该驱动程序有时会接收到 D3DGDI2 类型的 **GetDriverInfo2** 请求 \_ \_ \_ \_ 。 仅当运行时执行显示模式更改时，DirectX 运行时才会发送此通知。 驱动程序应检查进程标识符 (PID) ，该进程会根据创建该图面的进程对其进行销毁。 如果 Pid 不同，驱动程序不应销毁 AGP 内存的用户模式映射，因为应用程序可能仍在使用内存。

**GetDriverInfo2** \_ \_ \_ \_ 当进程内的所有显示设备使用在显示模式发生更改时锁定的图面、纹理、顶点缓冲区和索引缓冲区时，驱动程序将收到 D3DGDI2 类型 "免费延迟 AGP 通知" 的 GetDriverInfo2 请求。 通知会通知驱动程序，它可以安全地销毁 AGP 内存的所有用户模式映射。

在 D3DGDI2 \_ 类型 " \_ 延迟 \_ agp \_ 释放" 和 "D3DGDI2 \_ \_ \_ \_ " "免费延迟 agp 通知" 中，运行时提供指向 Dd GETDRIVERINFODATA 数据结构的**lpvData**成员中[**dd \_ FREE \_ 延迟 \_ agp \_ 数据**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_dd_free_deferred_agp_data)结构的指针 \_ 。 DD **dwProcessId** \_ FREE \_ 递延 agp 数据的 DWPROCESSID \_ 成员 \_ 指定销毁 agp 内存的进程的 PID。

请注意，应用程序可以在没有运行时 \_ \_ 向驱动程序发送 D3DGDI2 类型免费 \_ 延迟 \_ AGP 通知的情况下终止。 因此，当驱动程序收到对其 [**D3dDestroyDDLocal**](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_destroyddlocal) 函数的调用时，该驱动程序应释放 AGP 内存的所有用户模式映射。

 

