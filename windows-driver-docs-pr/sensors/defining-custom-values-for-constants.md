---
title: 定义传感器常量的自定义值（以前的版本）
description: 定义传感器常量的自定义值（以前的版本）
ms.assetid: 0ed635c2-117d-4a49-a565-31e5a0a9861d
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3eb02dbc9a49e92ff2e7f9abf2ba941e26dadc69
ms.sourcegitcommit: 9102e34c3322d8697dbb6f9a1d78879147a73373
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87264460"
---
# <a name="defining-custom-values-for-sensor-constants-previous-version"></a>定义传感器常量的自定义值（以前的版本）


您可以为类别、传感器类型、数据字段、属性和事件定义自定义值。

## <a name="guidelines-for-custom-values"></a>自定义值的准则

如果一组平台定义的常量有效，请避免定义新常量。 研究并了解 "[常量](https://docs.microsoft.com/windows-hardware/drivers/sensors/about-sensor-constants)参考" 部分中描述的类别、类型、数据字段、属性和事件，并决定传感器驱动程序是否适合平台框架。

如果选择定义自定义值，请遵循以下准则：

-   生成新 PROPERTYKEYs。 不要将 Guid 用于平台定义的常量，并且不基于平台定义的基准值的新 Guid。

-   对于同一传感器类别中的新传感器数据类型，请使用相同的 Guid。 若要使每个数据类型都是唯一的，请递增属性键的 PID 部分。

-   为传感器定义的新传感器属性使用相同的 Guid。 若要使每个属性都是唯一的，请递增属性键的 PID 部分。

-   为传感器定义的新传感器事件类型使用相同的 Guid。 若要使每个事件类型都是唯一的，请递增属性键的 PID 部分。

-   创建唯一的常量。 若要避免常量名称之间的冲突，请从每个自定义名称开始，其中包含一个值，可帮助在传感器代码内和其他实现之间使名称唯一。 例如，名为 Fabrikam 的公司可以使用开始每个常量定义 `FABRIKAM_` 。

-   记录和发布值。 如果希望开发人员能够通过 Windows 传感器 API 或位置 API 访问传感器中的数据，则必须记录自定义值并发布常量（例如，通过提供标头文件）。 如果你的传感器属于专用系统，则不需要发布自定义值。

## <a name="example"></a>示例

下面的代码示例演示如何定义传感器常量的自定义值。 该示例为提供当前本地时间的示例传感器创建新的类别、传感器类型和数据类型。 可以想象此类传感器通过卫星或其他无线电传输来接收来自引用时钟的时间信息。

```cpp
// Define a sensor ID.
// {0D77BEE3-7169-42bf-8379-28F9A9B59A57}
DEFINE_GUID(SAMPLE_SENSOR_TIME_ID,
0xd77bee3, 0x7169, 0x42bf, 0x83, 0x79, 0x28, 0xf9, 0xa9, 0xb5, 0x9a, 0x57);

// Define a custom category.
// {062A5C3B-44C1-4ad1-8EFC-0F65B2E4AD48}
DEFINE_GUID(SAMPLE_SENSOR_CATEGORY_DATE_TIME,
0x62a5c3b, 0x44c1, 0x4ad1, 0x8e, 0xfc, 0xf, 0x65, 0xb2, 0xe4, 0xad, 0x48);

// Define a custom type.
// {5F199A84-409F-4e35-B2DD-F9C79F5318A0}
DEFINE_GUID(SAMPLE_SENSOR_TYPE_TIME,
0x5f199a84, 0x409f, 0x4e35, 0xb2, 0xdd, 0xf9, 0xc7, 0x9f, 0x53, 0x18, 0xa0);

// Time/Date sensor fields.
// Because these are related, each field uses the same GUID, but changes the PID.
// {340946F2-9A77-42b0-8176-57D4DF00E5CA}
DEFINE_PROPERTYKEY(SAMPLE_SENSOR_DATA_TYPE_HOUR,
0x340946f2, 0x9a77, 0x42b0, 0x81, 0x76, 0x57, 0xd4, 0xdf, 0x0, 0xe5, 0xca, PID_FIRST_USABLE); // PID = 2

DEFINE_PROPERTYKEY(SAMPLE_SENSOR_DATA_TYPE_MINUTE,
0x340946f2, 0x9a77, 0x42b0, 0x81, 0x76, 0x57, 0xd4, 0xdf, 0x0, 0xe5, 0xca, PID_FIRST_USABLE + 1); // PID = 3

DEFINE_PROPERTYKEY(SAMPLE_SENSOR_DATA_TYPE_SECOND,
0x340946f2, 0x9a77, 0x42b0, 0x81, 0x76, 0x57, 0xd4, 0xdf, 0x0, 0xe5, 0xca, PID_FIRST_USABLE + 2); // PID = 4
```

## <a name="using-the-define_propertykey-macro"></a>使用 DEFINE \_ PROPERTYKEY 宏

若要使用 DEFINE \_ PROPERTYKEY 宏，请使用以下两个选项之一：

-   在项目中包括 Initguid.h。 在这种情况下，宏为你定义属性键。 此方法在大多数情况下都有效，但可能会导致大型复杂项目中的命名冲突。

-   不要包含 Initguid.h。 相反，请将您的定义编译为具有 .lib 文件扩展名的静态库文件。 在这种情况下，宏声明编译器的属性键的名称。 但是，您必须在链接器设置中引用 .lib 文件。 此方法最适用于使用多个模块的大型项目。

使用宏而不包含 Initguid.h，并且不引用库文件将导致 LNK2001 错误。

## <a name="related-topics"></a>相关主题
[传感器地理位置驱动程序示例](https://docs.microsoft.com/windows-hardware/drivers/gnss/sensors-geolocation-driver-sample)



