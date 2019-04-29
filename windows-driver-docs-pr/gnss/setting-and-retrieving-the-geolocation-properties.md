---
title: 设置和检索地理位置属性
description: 当应用程序检索特定属性值时，示例驱动程序中调用相应的属性检索方法。
ms.assetid: 576C610E-180A-44A0-9637-5C18341F3777
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2154b2fdabdd09c3f450b5e4132181669201dfd5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386330"
---
# <a name="setting-and-retrieving-the-geolocation-properties"></a>设置和检索地理位置属性

> [!IMPORTANT] 
> 已弃用此文档和 Windows 8.1 的地理位置驱动程序示例。

当应用程序检索特定属性值时，示例驱动程序中调用相应的属性检索方法。 对于模拟的传感器，这将是**CGeolocation::GetPropertyValuesForGeolocationObject**。 传感器 API 将通过应用程序请求的属性的属性键和驱动程序捆绑包中的属性值**IPortableDeviceValues**对象将其返回到 API。

当应用程序写入，或更新的属性 （如更改敏感度或所需的准确性），相应的属性写方法调用中的示例驱动程序。 对于模拟的传感器，这将是**CGeolocation::UpdateGeolocationPropertyValues**。 此方法是声明和定义传感器对象中的文件 （Geolocation.h 和 Geolocation.cpp），并在 SensorDDI.cpp 模块中调用。

有关如何定义传感器属性的信息，请参阅[支持的地理位置属性](supporting-the-geolocation-properties.md)。

## <a name="related-topics"></a>相关主题
[定义地理位置对象](defining-the-geolocation-object.md)  
[支持地理位置属性](supporting-the-geolocation-properties.md)  



