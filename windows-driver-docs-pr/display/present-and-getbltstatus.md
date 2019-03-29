---
title: 呈现和 GetBltStatus
description: 呈现和 GetBltStatus
ms.assetid: 76fd88df-18a9-4f00-834d-6683788fc2f6
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示、 演示文稿
- 演示文稿 WDK DirectX 8.0
- 呈现结果可见 WDK DirectX 8.0
- 可见结果 WDK DirectX 8.0
- DdGetBltStatus
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cab5d2eec86f70402741518a4c81bd7b072fe85a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565888"
---
# <a name="present-and-getbltstatus"></a>呈现和 GetBltStatus


## <span id="ddk_present_and_getbltstatus_gg"></span><span id="DDK_PRESENT_AND_GETBLTSTATUS_GG"></span>


对于 DX8 运行时不会再调用[ *DdGetBltStatus* ](https://msdn.microsoft.com/library/windows/hardware/ff549385) blts 涉及系统内存图面上。 这始终是 Windows 2000 上的行为。 结果是不再可以异步 DMA 到或从系统内存图面。 DX8 驱动程序不应本身是页锁定系统内存图面和视频内存传输到系统内存应该同步。

 

 





