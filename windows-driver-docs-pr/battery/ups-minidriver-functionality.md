---
title: UPS 微型驱动程序功能
description: UPS 微型驱动程序功能
ms.assetid: a93dbada-bcf7-4963-ba57-c6db5922c66b
keywords:
- UPS 微型驱动程序 WDK，功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 397696d91b29aeb41e00237f9279d408131489c6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522172"
---
# <a name="ups-minidriver-functionality"></a>UPS 微型驱动程序功能


## <span id="ddk_ups_minidriver_functionality_kg"></span><span id="DDK_UPS_MINIDRIVER_FUNCTIONALITY_KG"></span>


UPS 微型驱动程序必须将导出函数，由系统提供 UPS 服务调用以下的集：

-   [**UPSInit**](https://msdn.microsoft.com/library/windows/hardware/ff536313)

-   [**UPSGetState**](https://msdn.microsoft.com/library/windows/hardware/ff536312)

-   [**UPSWaitForStateChange**](https://msdn.microsoft.com/library/windows/hardware/ff536316)

-   [**UPSCancelWait**](https://msdn.microsoft.com/library/windows/hardware/ff536311)

-   [**UPSTurnOff**](https://msdn.microsoft.com/library/windows/hardware/ff536315)

-   [**UPSStop**](https://msdn.microsoft.com/library/windows/hardware/ff536314)

此外，微型驱动程序必须将导出[ **DLLMain** ](https://msdn.microsoft.com/library/windows/desktop/ms682583)函数，如 Microsoft Windows SDK 文档中所述。

除了导出这些函数，微型驱动程序必须提供的初始值[UPS 注册表项](ups-registry-entries.md)，然后根据需要以反映 UPS 状态更改中修改值。

通常情况下，UPS 微型驱动程序与通信的 COM 端口通过一个 UPS 单元通过调用[ **CreateFile**](https://msdn.microsoft.com/library/windows/desktop/aa363858)， [ **ReadFile**](https://msdn.microsoft.com/library/windows/desktop/aa365467)，和[**WriteFile** ](https://msdn.microsoft.com/library/windows/desktop/aa365747)函数 （Windows SDK 文档中所述）。 微型驱动程序负责实施任何通信协议 UPS 设备支持的。

 

 




