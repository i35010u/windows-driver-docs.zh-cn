---
title: 将地理位置传感器定义为对象
description: 传感器地理位置驱动程序示例将其模拟的地理位置传感器视为一个对象。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11e7c1258901dde565d3180ade684ca8bd9f1d15
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823266"
---
# <a name="defining-the-geolocation-sensor-as-an-object"></a>将地理位置传感器定义为对象

> [!IMPORTANT] 
> 此文档和 Windows 8.1 的地理位置驱动程序示例已弃用。

传感器地理位置驱动程序示例将其模拟的地理位置传感器视为一个对象。 此对象在名为 "地理位置 .h" 的头文件中声明。  (有关标头文件和其他驱动程序示例文件的说明，请参阅 [示例驱动程序文件列表](the-sample-driver-file-list.md) 部分。 ) 

标头文件包含定义伪传感器支持的属性的数据结构。 此外，头文件包含执行以下操作的方法的定义：

-   [初始化地理位置对象](initializing-the-geolocation-object.md)
-   设置或检索地理位置属性

相应方法的定义位于名为：地理位置 .cpp 的源文件中。

若要将此示例扩展为支持硬件，请创建声明和定义设备的相应对象的类似头文件和源文件。 有关扩展此示例的详细信息，请参阅 [添加对实际硬件的支持](adding-support-for-actual-hardware.md)。

## <a name="related-topics"></a>相关主题
[添加对实际硬件的支持](adding-support-for-actual-hardware.md)  
[初始化地理位置对象](initializing-the-geolocation-object.md)  
[示例驱动程序文件列表](the-sample-driver-file-list.md)  



