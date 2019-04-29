---
title: 将对实际硬件的支持添加到地理位置驱动程序示例
description: 作为起始点，用于模拟 GPS 设备提供地理位置驱动程序示例。 本主题介绍如何将添加对实际硬件的支持。
ms.assetid: 0D16C46F-4622-4191-83F2-579FC17DE985
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf9b63b47f6a8aeab61f29e575ca63fbabbef1ee
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371139"
---
# <a name="adding-support-for-real-hardware-to-the-geolocation-driver-sample"></a>将对实际硬件的支持添加到地理位置驱动程序示例

> [!IMPORTANT] 
> 已弃用此文档和 Windows 8.1 的地理位置驱动程序示例。

作为起始点，用于模拟 GPS 设备提供地理位置驱动程序示例。 本主题介绍如何将添加对实际硬件的支持。

下表中简要介绍的修订版本和支持的地理位置示例的真实硬件所需的新增功能。 该表还标识在哪里可以找到详细信息。

|                                                                                                  |                                                                                                                                                                                                                |
|--------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 修订版本或添加                                                                             | 详细信息                                                                                                                                                                                               |
| 重命名的源文件和头文件，以反映新的传感器的用途。                    | 请参阅"自定义示例"和"添加其他传感器到示例"部分包含在 Windows 驱动程序工具包中的示例源的自述文件 (SensorsGeolocationSample.htm)。 |
| 地理位置属性替换为新的传感器支持的属性。            | 请参阅随 Windows 驱动程序工具包中的示例源的自述文件 (SensorsGeolocationSample.htm) 的"添加其他传感器到示例"部分。                                  |
| 添加包含所需的代码以支持新传感器所需的传输的模块。 | .                                                                                                                                                                                                              |

 

如果你正在开发 GPS （或其他地理位置） 传感器和其运行 HID 传输上时，可以将你的设备的收件箱 HID 类驱动程序与集成。

自述文件，SensorsGeolocationDriverSample.htm，随 Windows 驱动程序工具包包括修改此驱动程序以支持温度传感器的说明。

**请注意**  如果您的传感器支持以外 HID 传输，您可以基于地理位置示例并将其作为起始点在新的驱动程序。 但是，如果您的传感器支持 HID 传输，您应编写固件与收件箱 HID 类驱动程序兼容。

 

## <a name="related-topics"></a>相关主题
[传感器地理位置驱动程序示例](sensors-geolocation-driver-sample.md)  



