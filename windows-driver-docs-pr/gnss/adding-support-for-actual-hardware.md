---
title: 将对实际硬件的支持添加到地理位置驱动程序示例
description: 地理位置驱动程序示例作为模拟 GPS 设备的起点而提供。 本主题介绍如何添加对真实硬件的支持。
ms.assetid: 0D16C46F-4622-4191-83F2-579FC17DE985
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f541ff466138e36ce8e9898d016ca399234e230
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968354"
---
# <a name="adding-support-for-real-hardware-to-the-geolocation-driver-sample"></a>将对实际硬件的支持添加到地理位置驱动程序示例

> [!IMPORTANT] 
> 此文档和 Windows 8.1 的地理位置驱动程序示例已弃用。

地理位置驱动程序示例作为模拟 GPS 设备的起点而提供。 本主题介绍如何添加对真实硬件的支持。

下表简要介绍了支持带有地理位置示例的真实硬件所需的修订和添加。 该表还标识了可在何处找到更多信息。

**修订或补充**：详细信息

**重命名源文件和标头文件，以反映新传感器的用途。**：请参阅 Windows 驱动程序工具包中的示例源随附的 readme （SensorsGeolocationSample.htm）中的 "自定义示例" 和 "向示例添加其他传感器" 部分。

将**地理位置属性替换为新传感器支持的属性。**：请参阅 Windows 驱动程序工具包中的示例源随附的自述文件（SensorsGeolocationSample.htm）中的 "向示例添加其他传感器" 部分。

**添加包含必要代码的模块，以支持新传感器所需的传输。**：。


 

如果要开发 GPS （或其他地理位置）传感器并且它在 HID 传输上运行，则可以将设备与收件箱 HID 类驱动程序集成。

Windows 驱动程序工具包随附的 readme 文件 SensorsGeolocationDriverSample.htm 包含了修改此驱动程序以支持温度传感器的说明。

**注意**   如果你的传感器支持除 HID 之外的传输，则可以在地理位置示例上构建，并将其用作新驱动程序的起点。 但是，如果您的传感器支持 HID 传输，则应该编写与收件箱 HID 类驱动程序兼容的固件。

 

## <a name="related-topics"></a>相关主题
[传感器地理位置驱动程序示例](sensors-geolocation-driver-sample.md)  



