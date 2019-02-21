---
title: 传感器常量
description: 传感器常量
ms.assetid: F3ED56C2-56AF-44FA-9ED8-7A16F1711AC7
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: d51eff0565c82d4d4999b8cb3e6370b36230b678
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520481"
---
# <a name="sensor-constants"></a>传感器常量


Windows 通用传感器使用不同的方式中的常量。 本部分介绍这些常量和它们的用法。

平台定义各种可以在通用传感器驱动程序代码中使用的常量。 此外可以定义您自己的常量。 您可以在 Sensorsdef.h 文件中找到平台定义的常量的定义。

## <a name="sensor-and-data-organization"></a>传感器和数据的组织

在平台中通过以下方式组织的传感器和他们的数据：

-   [传感器类型](sensor-types.md)表示特定类型的传感器。 每个传感器类型可以根据需要适合于特定类别。

-   [传感器数据字段](sensor-data-fields.md)表示特定类型的传感器可以提供的信息。 在报告数据，值被认为是要包含在*数据字段*，和相关的数据字段的集合构成*数据报表*。 每个数据字段由**PROPERTYKEY**常量。

-   [传感器阈值](sensor-thresholds-v2.md)表示要配置传感器数据筛选的属性。 传感器硬件或驱动程序只报告传感器示例传感器类扩展都达到或超过阈值条件时。

-   [传感器属性](sensor-properties2.md)包含描述 Windows 设备安装的驱动程序的特征的数据。

-   [传感器类别](sensor-categories.md)表示传感器设备的广泛类。 类别提供组传感器可能能够提供类似类型的信息，或以某种方式无关的方式。 每个类别均由 GUID 常量表示。 不同类型的两个传感器可以属于同一类别或两个不同的类别。 每个传感器类型由 GUID 常量表示。 例如，加速感应器和陀螺仪可能同时进行分类 GUID_SensorCategory_Motion 类别下而 abient 光线传感器会归类 GUID_SensorCategory_Light 类别下。


## <a name="other-constants"></a>其他常量

您的驱动程序可能需要使用其他类型的常量，例如图标常量。 您的驱动程序可以指定一个特定的图标来表示在 Windows 设备。 请参阅[指定一个图标](specifying-an-icon.md)。


## <a name="persistent-unique-identifier"></a>持久的唯一标识符

名为 DEVPKEY_Sensor_PersistentUniqueId 传感器属性需要特别注意。 此属性的值必须是唯一的设备上的每个传感器。 同时，此值必须保持一致的某个特定传感器传感器平台使用它每次。 有关如何在驱动程序代码中创建的永久性的唯一标识符的示例，请参阅[创建持久的唯一标识符](creating-a-persistent-unique-identifier-v2.md)。

### <a name="custom-values"></a>自定义值

可以定义自定义值的类别、 传感器类型、 数据字段和属性

有关指导原则和如何定义自定义值的常量的示例，请参阅[定义的自定义值的常量](defining-custom-values-for-constants-v2.md)。

