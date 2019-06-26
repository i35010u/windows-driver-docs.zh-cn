---
title: 识别打印机的颜色功能
description: 识别打印机的颜色功能
ms.assetid: 24abf76d-c0f9-440e-b825-8b39ea9ab807
keywords:
- 打印机接口 DLL WDK，颜色功能支持
- 颜色管理 WDK 打印，识别功能
- 识别打印机颜色功能
- 打印机颜色功能 WDK
- dmColor
- DC_COLORDEVICE
- DrvDeviceCapabilities
- 单色输出 WDK 打印机
- 普通输出 WDK 打印机
- 灰度输出 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f50078222e1b210934e8d803adf0011c80dd8686
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382564"
---
# <a name="identifying-a-printers-color-capability"></a>识别打印机的颜色功能





若要区分颜色和普通 （单色或灰度） 设备、 Windows 2000 和更高版本基于 NT 的操作系统版本调用[ **DrvDeviceCapabilities** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdevicecapabilities)函数，传递 DC\_COLORDEVICE 常量的调用中。 如果设备支持颜色和 0，如果设备生成单色或灰度输出，则此函数返回 1。 建议所有打印机驱动程序都支持对调用**DrvDeviceCapabilities** dc\_COLORDEVICE 常量。

它是非常重要的驱动程序，以实现[ **DrvDeviceCapabilities** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdevicecapabilities)函数。 否则会更加困难的操作系统，以区分颜色和普通设备，原因如下：

-   调用**GetDeviceCaps**函数 （Windows SDK 文档中所述），在其中传递 NUMCOLORS 常量，通常在返回的结果值小于或等于 2 适用于大多数普通设备，且大于 2颜色的设备。 操作系统不能区分单色和灰度设备。

-   值**dmColor**的成员[ **DEVMODEW** ](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)结构不是设备是一个颜色或普通的设备的可靠指示器。 某些打印机驱动程序将此成员设置为 DMCOLOR\_即使设备不能够生成颜色的颜色。

 

 




