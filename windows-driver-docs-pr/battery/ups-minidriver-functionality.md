---
title: UPS 微型驱动程序功能
description: UPS 微型驱动程序功能
ms.assetid: a93dbada-bcf7-4963-ba57-c6db5922c66b
keywords:
- 微型驱动程序 WDK，功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e45ccaa9f194b9fe844fdedbe09fcf36539b884c
ms.sourcegitcommit: 7a7e61b4147a4aa86bf820fd0b0c7681fe17e544
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89056870"
---
# <a name="ups-minidriver-functionality"></a>UPS 微型驱动程序功能


## <span id="ddk_ups_minidriver_functionality_kg"></span><span id="DDK_UPS_MINIDRIVER_FUNCTIONALITY_KG"></span>


UPS 微型驱动程序必须导出以下由系统提供的 UPS 服务调用的函数集：

-   [**UPSInit**](/windows-hardware/drivers/ddi/upssvc/nf-upssvc-upsinit)

-   [**UPSGetState**](/windows-hardware/drivers/ddi/upssvc/nf-upssvc-upsgetstate)

-   [**UPSWaitForStateChange**](/windows-hardware/drivers/ddi/upssvc/nf-upssvc-upswaitforstatechange)

-   [**UPSCancelWait**](/windows-hardware/drivers/ddi/upssvc/nf-upssvc-upscancelwait)

-   [**UPSTurnOff**](/windows-hardware/drivers/ddi/upssvc/nf-upssvc-upsturnoff)

-   [**UPSStop**](/windows-hardware/drivers/ddi/upssvc/nf-upssvc-upsstop)

此外，微型驱动程序必须导出 [**DLLMain**](/windows/desktop/Dlls/dllmain) 函数，如 Microsoft Windows SDK 文档中所述。

除了导出这些函数外，微型驱动程序还必须为 [UPS 注册表项](ups-registry-entries.md) 提供初始值，然后根据需要修改这些值以反映 UPS 状态更改。

通常情况下，UPS 微型驱动程序通过 COM 端口与 UPS 单元通信，方法是调用 [**CreateFile**](/windows/desktop/api/fileapi/nf-fileapi-createfilea)、 [**ReadFile**](/windows/desktop/api/fileapi/nf-fileapi-readfile)和 [**WriteFile**](/windows/desktop/api/fileapi/nf-fileapi-writefile) 函数， () 的 Windows SDK 文档中所述。 微型驱动程序负责实现 UPS 设备支持的任何通信协议。

 

