---
title: 设置和检索地理位置属性
description: 当应用程序检索特定属性值时，会在示例驱动程序中调用相应的属性检索方法。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bdebb7816ac02de7e82ae728a2dc51ad9fc07ee
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825989"
---
# <a name="setting-and-retrieving-the-geolocation-properties"></a>设置和检索地理位置属性

> [!IMPORTANT] 
> 此文档和 Windows 8.1 的地理位置驱动程序示例已弃用。

当应用程序检索特定属性值时，会在示例驱动程序中调用相应的属性检索方法。 对于模拟传感器，这应为 **CGeolocation：： GetPropertyValuesForGeolocationObject**。 传感器 API 会传递应用程序请求的属性的属性键，驱动程序会将属性值绑定到 **IPortableDeviceValues** 对象中，并将其返回到 API。

当应用程序写入或更新属性 (如) 更改敏感度或所需准确性时，将在示例驱动程序中调用相应的属性写入方法。 对于模拟传感器，这应为 **CGeolocation：： UpdateGeolocationPropertyValues**。 此方法在传感器对象的文件中声明和定义 (地理位置 .h 和地理位置 .cpp) 并在 SensorDDI 模块中调用。

有关如何定义传感器属性的信息，请参阅 [支持地理位置属性](supporting-the-geolocation-properties.md)。

## <a name="related-topics"></a>相关主题
[定义地理位置对象](defining-the-geolocation-object.md)  
[支持地理位置属性](supporting-the-geolocation-properties.md)  



