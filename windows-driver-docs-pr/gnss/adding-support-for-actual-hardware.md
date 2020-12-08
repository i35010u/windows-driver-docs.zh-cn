---
title: 将对实际硬件的支持添加到地理位置驱动程序示例
description: 地理位置驱动程序示例作为模拟 GPS 设备的起点而提供。 本主题介绍如何添加对真实硬件的支持。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a00ea1a2d779d30fa3e4e360cd021d2ed972b602
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823269"
---
# <a name="adding-support-for-real-hardware-to-the-geolocation-driver-sample"></a>将对实际硬件的支持添加到地理位置驱动程序示例

> [!IMPORTANT] 
> 此文档和 Windows 8.1 的地理位置驱动程序示例已弃用。

地理位置驱动程序示例作为模拟 GPS 设备的起点而提供。 本主题介绍如何添加对真实硬件的支持。

下表简要介绍了支持带有地理位置示例的真实硬件所需的修订和添加。 该表还标识了可在何处找到更多信息。

**修订或补充**：详细信息

**重命名源文件和标头文件，以反映新传感器的用途。**：请参阅 "自定义示例" 和 "将其他传感器添加到示例" 这两节，其中包含了 Windows 驱动程序工具包中的示例源随附的 readme ( # A0) 。

将 **地理位置属性替换为新传感器支持的属性。**：请参阅自述文件的 "将其他传感器添加到示例" 部分，该部分包含在 Windows 驱动程序工具包的示例源中 ( # A0) 。

**添加包含必要代码的模块，以支持新传感器所需的传输。**：。


 

如果要开发 GPS (或其他地理位置) 传感器，并在 HID 传输上运行，则可以将设备与收件箱 HID 类驱动程序集成。

Windows 驱动程序工具包随附的 readme 文件 SensorsGeolocationDriverSample.htm 包含了修改此驱动程序以支持温度传感器的说明。

**注意**  
如果你的传感器支持除 HID 之外的传输，则可以在地理位置示例上构建，并将其用作新驱动程序的起点。 但是，如果您的传感器支持 HID 传输，则应该编写与收件箱 HID 类驱动程序兼容的固件。

 

## <a name="related-topics"></a>相关主题
[传感器地理位置驱动程序示例](sensors-geolocation-driver-sample.md)  



