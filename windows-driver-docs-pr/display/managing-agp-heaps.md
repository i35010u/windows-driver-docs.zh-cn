---
title: 管理 AGP 堆
description: 管理 AGP 堆
ms.assetid: edeed3bc-c107-4286-9d5a-7fdef89cc4e1
keywords:
- 堆 WDK DirectDraw
- 显示内存 WDK DirectDraw 堆
- 非本地显示内存 WDK DirectDraw 堆
- AGP WDK DirectDraw 堆
- 绘制 AGP 支持 WDK DirectDraw，堆
- DirectDraw AGP 支持 WDK Windows 2000 显示堆
- WDK DirectDraw AGP，堆内存
- GetDriverInfo2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 237a030332369aed342e70f139cb8398a569a054
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379018"
---
# <a name="managing-agp-heaps"></a>管理 AGP 堆


## <span id="ddk_managing_agp_heaps_gg"></span><span id="DDK_MANAGING_AGP_HEAPS_GG"></span>


**本主题仅适用于基于 Windows NT 的操作系统。**

驱动程序可以管理 AGP 堆使用 DirectX 运行时从其接收的通知。 该驱动程序从作为运行时接收通知**GetDriverInfo2**请求使用以下值：

-   D3DGDI2\_TYPE\_DEFERRED\_AGP\_AWARE

-   D3DGDI2\_TYPE\_FREE\_DEFERRED\_AGP

-   D3DGDI2\_TYPE\_DEFER\_AGP\_FREES

有关详细信息**GetDriverInfo2**请求，请参阅[支持 GetDriverInfo2](supporting-getdriverinfo2.md)。

显示驱动程序创建的显示设备时，接收**GetDriverInfo2** D3DGDI2 请求\_类型\_已推迟\_AGP\_注意通知其驱动程序用于确定是否它应禁用其其他机制处理 AGP 堆并改为使用 D3DGDI2\_类型\_免费\_延期\_AGP 和 D3DGDI2\_类型\_DEFER\_AGP\_FREES 随后会在运行时发送的通知。 在 D3DGDI2\_类型\_延期\_AGP\_注意通知 DirectX 运行时提供一个指针指向[ **DD\_已推迟\_AGP\_注意\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_dd_deferred_agp_aware_data)结构**lpvData**隶属[ **DD\_GETDRIVERINFODATA** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_getdriverinfodata)数据结构。

驱动程序有时会收到**GetDriverInfo2**请求 D3DGDI2\_类型\_DEFER\_AGP\_FREES 通知显示模式下更改发生之前。 DirectX 运行时仅发送此通知，如果运行时执行显示模式更改。 该驱动程序应检查销毁面针对创建表面的进程的进程的进程标识符 (PID)。 如果 Pid 不同，该驱动程序不应销毁 AGP 内存的用户模式下映射，因为应用程序可能仍使用的内存。

驱动程序收到**GetDriverInfo2**请求 D3DGDI2\_类型\_免费\_已推迟\_AGP 通知时所有显示进程停止使用图面中的设备纹理、 顶点缓冲区和索引缓冲区时的显示模式下更改而被锁定。 此通知告诉驱动程序，它可以安全地销毁的所有用户模式下的 AGP 内存映射。

在 D3DGDI2\_类型\_DEFER\_AGP\_FREES 和 D3DGDI2\_类型\_免费\_已推迟\_AGP 通知运行时提供一个指针指向[ **DD\_免费\_已推迟\_AGP\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_dd_free_deferred_agp_data)结构**lpvData** DD 的成员\_GETDRIVERINFODATA 数据结构。 **DwProcessId** DD 成员\_免费\_已推迟\_AGP\_数据指定销毁 AGP 内存的进程的 PID。

请注意应用程序可以终止而无需运行时发送 D3DGDI2\_类型\_免费\_延期\_AGP 通知给驱动程序。 因此，驱动程序应释放的所有用户模式下映射的 AGP 内存时接收调用其[ **D3dDestroyDDLocal** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_destroyddlocal)函数。

 

 





