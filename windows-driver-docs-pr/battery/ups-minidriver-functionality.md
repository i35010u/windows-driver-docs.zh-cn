---
title: UPS 微型驱动程序功能
description: UPS 微型驱动程序功能
ms.assetid: a93dbada-bcf7-4963-ba57-c6db5922c66b
keywords:
- UPS 微型驱动程序 WDK，功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14acc80101a87b3ed0e614bd81b1288458969699
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364709"
---
# <a name="ups-minidriver-functionality"></a>UPS 微型驱动程序功能


## <span id="ddk_ups_minidriver_functionality_kg"></span><span id="DDK_UPS_MINIDRIVER_FUNCTIONALITY_KG"></span>


UPS 微型驱动程序必须将导出函数，由系统提供 UPS 服务调用以下的集：

-   [**UPSInit**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/upssvc/nf-upssvc-upsinit)

-   [**UPSGetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/upssvc/nf-upssvc-upsgetstate)

-   [**UPSWaitForStateChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/upssvc/nf-upssvc-upswaitforstatechange)

-   [**UPSCancelWait**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/upssvc/nf-upssvc-upscancelwait)

-   [**UPSTurnOff**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/upssvc/nf-upssvc-upsturnoff)

-   [**UPSStop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/upssvc/nf-upssvc-upsstop)

此外，微型驱动程序必须将导出[ **DLLMain** ](https://docs.microsoft.com/windows/desktop/Dlls/dllmain)函数，如 Microsoft Windows SDK 文档中所述。

除了导出这些函数，微型驱动程序必须提供的初始值[UPS 注册表项](ups-registry-entries.md)，然后根据需要以反映 UPS 状态更改中修改值。

通常情况下，UPS 微型驱动程序与通信的 COM 端口通过一个 UPS 单元通过调用[ **CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)， [ **ReadFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-readfile)，和[**WriteFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-writefile)函数 （Windows SDK 文档中所述）。 微型驱动程序负责实施任何通信协议 UPS 设备支持的。

 

 




