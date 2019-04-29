---
title: 关于传感器常量
description: 关于传感器常量
ms.assetid: 9c26e305-0d5c-4442-9bcf-a9cdc1778c6b
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: fcc794e1f0e2d68bc074c5fa3ee349b1d831ce19
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360947"
---
# <a name="about-sensor-constants"></a>有关传感器常量


Windows 传感器和位置平台使用不同的方式中的常量。 本部分介绍这些常量和它们的用法。

平台定义各种可以在传感器驱动程序代码中使用的常量。 此外可以定义您自己的常量。 您可以在 Sensors.h 和 Sensorsdef.h 文件中查找平台定义的常量的定义。

## <a name="sensor-and-data-organization"></a>传感器和数据的组织

在平台中通过以下方式组织的传感器和他们的数据：

-   *类别*表示传感器设备的广泛类。 类别提供组传感器可能能够提供类似类型的信息，或以某种方式无关的方式。 每个类别均由 GUID 常量表示。 例如，报表纬度和经度坐标属于位置传感器类别，由表示的传感器[**传感器\_类别\_位置**](sensor-category-loc.md)常量。

-   *传感器类型*表示特定类型的传感器。 每个传感器类型适合于特定类别。 不同类型的两个传感器可以属于同一类别或两个不同的类别。 每个传感器类型由 GUID 常量表示。 例如，全球定位系统传感器将由传感器\_类型\_位置\_GPS 常量，而将由标识提供当前使用的 Internet IP 地址的位置的传感器传感器\_类型\_位置\_查找常量。 但是，这两个传感器将属于位置传感器类别。

-   *数据类型*表示特定类型的传感器可以提供的信息。 传感器数据类型可以包含实际测量值，如海拔高度，单位用于表示数据，例如计量器和数据，例如 sea 级别的引用点的信息。 每种数据类型表示由**PROPERTYKEY**常量。 例如，表示 x 轴加速 g's 中的数据类型将传感器\_数据\_类型\_加速\_X\_G 常量。

-   在报告数据，值被认为是要包含在*数据字段*，和相关的数据字段的集合构成*数据报表*。 通过使用一起打包数据报表[IPortableDeviceValues](https://go.microsoft.com/fwlink/p/?linkid=131486)接口。 数据的每个报表必须包含至少一个有效的数据字段和一个时间戳，标识创建了数据报表的时间。 时间戳由传感器\_数据\_类型\_时间戳属性键。


## <a name="other-constants"></a>其他常量

您的驱动程序将需要使用某些其他类型的常量，也。 这些常量包括：

-   传感器属性，如传感器\_属性\_说明。 这些常量包括 WPD 常量，例如 WPD\_功能\_对象\_类别。 通常情况下，这些常量用于描述您的传感器，例如何时在中称为[ **ISensorDriver::OnGetSupportedSensorObjects**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetsupportedsensorobjects)。 您还将返回属性值通过[ **ISensorDriver::OnGetSupportedProperties** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetsupportedproperties)并[ **ISensorDriver::OnGetProperties** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetproperties).

-   某些传感器属性需要由您的驱动程序提供，某些属性可以设置客户端应用程序，而且一些必须始终返回相同的值。 [**传感器属性**](sensor-properties.md)参考部分提供了每个属性的此信息。 若要了解哪些属性所需的特定方法，请参阅中的方法文档[Windows 传感器引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_sensors/#functions)部分。

-   [**事件常量**](about-sensor-driver-events.md)，如传感器\_事件\_状态\_已更改。 事件常量包括 GUID，表示类型的事件，以及 PROPERTYKEYs，表示事件参数类型。 将使用这些常量中的类扩展调用[ **ISensorDriver::OnGetSupportedEvents**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetsupportedevents)，或在引发事件通过时[ **ISensorClassExtension:: PostEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-postevent)或[ **ISensorClassExtension::PostStateChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-poststatechange)。

-   图标的常量。 您的驱动程序可以指定一个特定的图标来表示在 Windows 设备。 请参阅[指定一个图标](specifying-an-icon.md)。

-   传感器平台定义 GUID_DEVINTERFACE_SENSOR 常量，以确定传感器设备接口类。 其在安装期间，驱动程序注册至少一台设备接口类。 传感器类扩展为您注册的传感器设备接口类。



## <a name="persistent-unique-identifier"></a>持久的唯一标识符

传感器属性名为传感器\_属性\_的永久\_UNIQUE\_ID 需要特别注意。 此属性的值必须是唯一的设备上的每个传感器。 同时，此值必须保持一致的某个特定传感器传感器平台使用它每次。 有关如何在驱动程序代码中创建的永久性的唯一标识符的示例，请参阅[创建持久的唯一标识符](creating-a-persistent-unique-identifier.md)。

## <a name="providing-geolocation-information"></a>提供地理位置信息

有时它是重要的用户知道的物理位置传感器，即使传感器不是位置传感器。 例如，气象站提供的数据的含义已紧密连接到工作站的位置。

若要提供此类型的地理位置数据，任何传感器可以使用适当的数据字段从[**传感器\_类别\_位置**](sensor-category-loc.md)类别，即使不是位置传感器。传感器。 因此，气象站可能会报告其位置使用传感器\_数据\_类型\_纬度\_度和传感器\_数据\_类型\_经度\_度数据字段常量。 但是，务必不报告为位置类别中，调用时不属于此类传感器[ **ISensorDriver::OnGetProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetproperties)。

Windows 将视为现有位置类别中具有的任何位置类型的传感器 (传感器\_类别\_位置)。 因此，这些传感器属于位置权限模型。 不应尝试绕过位置传感器的权限模式 (例如，公开将 GPS 传感器类型作为传感器\_类型\_位置\_GPS 但指定非位置类别)。

## <a name="custom-values"></a>自定义值

可以定义自定义值的类别、 传感器类型，数据字段、 属性和事件。

有关指导原则和如何定义自定义值的常量的示例，请参阅[定义的自定义值的常量](defining-custom-values-for-constants.md)。

 

 




