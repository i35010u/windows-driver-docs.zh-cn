---
title: UPS 微型驱动程序功能
description: UPS 微型驱动程序功能
ms.assetid: a93dbada-bcf7-4963-ba57-c6db5922c66b
keywords:
- 微型驱动程序 WDK，功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d558da26414534e54ee86fb10c56df6fa59439ba
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833962"
---
# <a name="ups-minidriver-functionality"></a>UPS 微型驱动程序功能


## <span id="ddk_ups_minidriver_functionality_kg"></span><span id="DDK_UPS_MINIDRIVER_FUNCTIONALITY_KG"></span>


UPS 微型驱动程序必须导出以下由系统提供的 UPS 服务调用的函数集：

-   [**UPSInit**](https://docs.microsoft.com/windows-hardware/drivers/ddi/upssvc/nf-upssvc-upsinit)

-   [**UPSGetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/upssvc/nf-upssvc-upsgetstate)

-   [**UPSWaitForStateChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/upssvc/nf-upssvc-upswaitforstatechange)

-   [**UPSCancelWait**](https://docs.microsoft.com/windows-hardware/drivers/ddi/upssvc/nf-upssvc-upscancelwait)

-   [**UPSTurnOff**](https://docs.microsoft.com/windows-hardware/drivers/ddi/upssvc/nf-upssvc-upsturnoff)

-   [**UPSStop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/upssvc/nf-upssvc-upsstop)

此外，微型驱动程序必须导出[**DLLMain**](https://docs.microsoft.com/windows/desktop/Dlls/dllmain)函数，如 Microsoft Windows SDK 文档中所述。

除了导出这些函数外，微型驱动程序还必须为[UPS 注册表项](ups-registry-entries.md)提供初始值，然后根据需要修改这些值以反映 UPS 状态更改。

通常，UPS 微型驱动程序通过调用[**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)、 [**ReadFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-readfile)和[**WriteFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-writefile)函数（如 Windows SDK 文档中所述）通过 COM 端口与 ups 单元通信。 微型驱动程序负责实现 UPS 设备支持的任何通信协议。

 

 




