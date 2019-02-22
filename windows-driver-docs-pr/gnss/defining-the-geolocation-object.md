---
title: 为对象定义地理位置传感器
description: 传感器地理位置驱动程序示例将对象视为其模拟的地理位置传感器。
ms.assetid: CDAA93A1-9B20-4602-9A8A-A2C7CF52B576
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b578074781b44439f818ab1644d56e1abfc296ba
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523024"
---
# <a name="defining-the-geolocation-sensor-as-an-object"></a>为对象定义地理位置传感器

> [!IMPORTANT] 
> 已弃用此文档和 Windows 8.1 的地理位置驱动程序示例。

传感器地理位置驱动程序示例将对象视为其模拟的地理位置传感器。 此对象是名为 geolocation.h 标头文件中声明的。 (有关标头文件和其他驱动程序示例文件的说明，请参阅[示例驱动程序文件列表](the-sample-driver-file-list.md)部分。)

标头文件包含一个定义伪传感器支持的属性的数据结构。 此外，该标头文件包含执行以下操作方法的定义：

-   [初始化地理位置对象](initializing-the-geolocation-object.md)
-   设置或检索的地理位置属性

名为的源代码文件中找到相应的方法的定义： geolocation.cpp。

若要扩展此示例，若要支持的硬件，请创建类似的标头和声明和定义你的设备的相应对象的源文件。 有关扩展此示例的详细信息，请参阅[添加对实际硬件支持](adding-support-for-actual-hardware.md)。

## <a name="related-topics"></a>相关主题
[添加对实际硬件的支持](adding-support-for-actual-hardware.md)  
[初始化地理位置对象](initializing-the-geolocation-object.md)  
[示例驱动程序文件列表](the-sample-driver-file-list.md)  



