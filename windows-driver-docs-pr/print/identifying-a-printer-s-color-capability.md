---
title: 识别打印机的颜色功能
description: 识别打印机的颜色功能
ms.assetid: 24abf76d-c0f9-440e-b825-8b39ea9ab807
keywords:
- 打印机接口 DLL WDK，支持的颜色功能
- 颜色管理 WDK 打印，识别功能
- 标识打印机颜色功能
- 打印机颜色功能 WDK
- dmColor
- DC_COLORDEVICE
- DrvDeviceCapabilities
- 单色输出 WDK 打印机
- noncolor 输出 WDK 打印机
- 灰度输出 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7198bd12540e38cc3e0a3eacca29ec0579fb47cb
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802563"
---
# <a name="identifying-a-printers-color-capability"></a>识别打印机的颜色功能





若要区分 color 和 noncolor (单色或灰度) 设备，Windows 2000 和更高版本的基于 NT 的操作系统版本调用 [**DrvDeviceCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdevicecapabilities) 函数，并 \_ 在调用中传递 DC COLORDEVICE 常数。 如果设备支持颜色，则此函数返回 1; 如果设备生成单色或灰度输出，则返回0。 建议所有打印机驱动程序都支持对 DC COLORDEVICE 常量调用 **DrvDeviceCapabilities** \_ 。

驱动程序实现 [**DrvDeviceCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdevicecapabilities) 函数非常重要。 否则，操作系统更难区分 color 和 noncolor 设备，原因如下：

-   对 **GetDeviceCaps** 函数的调用 (Windows SDK 文档) 中所述，在这种情况下传递 NUMCOLORS 常数，通常会导致大多数 noncolor 设备的返回值小于或等于2，对于彩色设备，则为大于2的值。 操作系统无法区分单色和灰度设备。

-   [**DEVMODEW**](https://docs.microsoft.com/windows/win32/api/wingdi/ns-wingdi-devmodew)结构的**dmColor**成员的值并不是设备是否为彩色或 noncolor 设备的可靠指示器。 某些打印机驱动程序将此成员设置为 DMCOLOR \_ 颜色，即使对于不能生成颜色的设备也是如此。

 

 




