---
title: 验证私有数据从用户模式下发送到内核模式
description: 验证私有数据从用户模式下发送到内核模式
ms.assetid: 7022af7b-80e7-41a5-bd53-32d7eafc4062
keywords:
- 验证显示 WDK 的专用数据
- 私有数据验证 WDK 显示
- 无效的专用数据 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 996e3a85697f5d7b7b1661be169b21d900a738b8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534813"
---
# <a name="validating-private-data-sent-from-user-mode-to-kernel-mode"></a>验证私有数据从用户模式下发送到内核模式


显示微型端口驱动程序必须验证发送的所有专用数据从用户模式显示驱动程序以防止发生故障，微型端口驱动程序未响应 （挂起） 断言，或如果是无效的私有数据损坏内存。 但是，因为操作系统将重置"挂起"的硬件，显示微型端口驱动程序可以将指令发送到图形处理单元 (GPU)，导致 GPU"挂起"。 私有数据可以包括任何以下各项：

-   命令发送到微型端口驱动程序的缓冲区内容[ **DxgkDdiRender** ](https://msdn.microsoft.com/library/windows/hardware/ff559793)或[ **DxgkDdiRenderKm** ](https://msdn.microsoft.com/library/windows/hardware/ff559800)中函数**pCommand**缓冲区隶属[ **DXGKARG\_呈现**](https://msdn.microsoft.com/library/windows/hardware/ff557648)结构。

-   数据发送到以下的微型端口驱动程序函数：
    -   [ **DxgkDdiCreateAllocation** ](https://msdn.microsoft.com/library/windows/hardware/ff559606)函数，在**pPrivateDriverData**缓冲的成员[ **DXGKARG\_CREATEALLOCATION** ](https://msdn.microsoft.com/library/windows/hardware/ff557559)并[ **DXGK\_ALLOCATIONINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff560960)结构。
    -   [ **DxgkDdiEscape** ](https://msdn.microsoft.com/library/windows/hardware/ff559653)函数，在**pPrivateDriverData**缓冲区隶属[ **DXGKARG\_转义**](https://msdn.microsoft.com/library/windows/hardware/ff557588)结构。
    -   [ **DxgkDdiAcquireSwizzlingRange** ](https://msdn.microsoft.com/library/windows/hardware/ff559582)函数，在**PrivateDriverData**的 32 位成员[ **DXGKARG\_ACQUIRESWIZZLINGRANGE** ](https://msdn.microsoft.com/library/windows/hardware/ff557539)结构。
    -   [ **DxgkDdiReleaseSwizzlingRange** ](https://msdn.microsoft.com/library/windows/hardware/ff559786)函数，在**PrivateDriverData**的 32 位成员[ **DXGKARG\_RELEASESWIZZLINGRANGE** ](https://msdn.microsoft.com/library/windows/hardware/ff557644)结构。
    -   [ **DxgkDdiQueryAdapterInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff559746)函数，在**pInputData**缓冲区隶属[ **DXGKARG\_QUERYADAPTERINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff557621)结构时 DXGKQAITYPE\_中指定 UMDRIVERPRIVATE 值**类型**成员。

 

 





