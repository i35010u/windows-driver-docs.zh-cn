---
title: 创建自定义设备属性
description: 创建自定义设备属性
keywords:
- 设备属性 WDK 设备安装，创建自定义
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 394db63478e3908905ffb1685730a9a0c866d9c8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827807"
---
# <a name="creating-custom-device-properties"></a>创建自定义设备属性


在 Windows Vista 和更高版本的 Windows 中， [统一设备属性模型](unified-device-property-model--windows-vista-and-later-.md) 支持为设备实例、 [设备安装程序类](./overview-of-device-setup-classes.md)、设备接口类和设备接口创建自定义设备属性类别。 可以通过调用相应的 [setupapi.log 属性函数](/previous-versions/ff541483(v=vs.85))来访问自定义属性。 还可以使用 [**Inf AddProperty 指令**](inf-addproperty-directive.md) 或 [**inf DelProperty 指令**](inf-delproperty-directive.md)修改自定义设备属性。

有关自定义设备属性的详细信息，请参阅以下主题：

[创建自定义设备属性类别](#creating-custom-device-property-categories)

[使用 Setupapi.log 属性函数访问自定义设备属性](#using-the-setupapi-property-functions-to-access-custom-device-properti)

[使用 INF AddProperty 指令或 INF DelProperty 指令修改自定义设备属性](#using-the-inf-addproperty-directive-or-the-inf-delproperty-directive-t)

### <a name="creating-custom-device-property-categories"></a><a href="" id="creating-custom-device-property-categories"></a> 创建自定义设备属性类别

自定义设备属性类别是逻辑上相关的自定义设备属性的集合。 若要以编程方式创建自定义设备属性类别，请使用 [**DEFINE_DEVPROPKEY**](./define-devpropkey.md) 宏创建表示属性类别中属性的属性键，如下所示：

-   创建表示属性类别的唯一 GUID 值，并将每个属性键的 GUID 值设置为此唯一的 GUID 值。 有关如何创建新 GUID 值的信息，请参阅 [定义和导出新的 guid](../kernel/defining-and-exporting-new-guids.md)。

    **注意**  系统定义的属性类别只保留给操作系统使用。

     

-   将每个属性键的属性标识符设置为一个整数值，该值在属性类别中是唯一的且大于或等于2。

还可以通过使用 [**INF AddProperty 指令**](inf-addproperty-directive.md)为设备实例创建自定义设备属性类别。

### <a name="using-the-setupapi-property-functions-to-access-custom-device-properties"></a><a href="" id="using-the-setupapi-property-functions-to-access-custom-device-properti"></a> 使用 Setupapi.log 属性函数访问自定义设备属性

按照 [使用 Setupapi.log 访问设备属性 (Windows Vista 和) 更高版本 ](using-setupapi-to-access-device-properties--windows-vista-and-later-.md)中所述的相同方式访问自定义设备属性。 访问自定义设备属性时，需要注意以下附加事项：

-   **SetupDiGetXxxPropertyKeys** 和 **SetupDiGetXxxPropertyKeysEx** 函数检索系统定义的设备属性键和自定义设备属性键，它们表示为组件设置的属性。

-   **SetupDiSetXxxProperty** 函数为组件设置自定义设备属性。 Windows 内部将自定义设备属性键、属性数据类型和属性值关联起来。 如果已经设置了具有相同属性键的自定义设备属性，则 **SetupDiSetXxxProperty** 函数将覆盖与属性关联的属性值和属性数据类型。

-   **SetupDiGetXxxProperty** 函数检索为组件设置的自定义设备属性。 **SetupDiGetXxxProperty** 函数检索属性值和在设置属性时设置的属性数据类型。

### <a name="using-the-inf-addproperty-directive-or-the-inf-delproperty-directive-to-modify-a-custom-device-property"></a><a href="" id="using-the-inf-addproperty-directive-or-the-inf-delproperty-directive-t"></a> 使用 INF AddProperty 指令或 INF DelProperty 指令修改自定义设备属性

若要使用 [**INF AddProperty 指令**](inf-addproperty-directive.md)修改自定义设备属性，请在安装组件的部分中包括 AddProperty 指令，并为属性提供以下项：

-   表示自定义设备属性类别的 *属性类别 guid* 条目

-   标识自定义设备属性类别中的属性的属性标识符项

-   新设备属性的 *值* 项或修改现有设备属性值的 *值* 项

使用 [**INF DelProperty 指令**](inf-delproperty-directive.md) 删除自定义设备属性。

有关如何使用这些指令的详细信息，请参阅 [Using THE Inf AddProperty 指令和 Inf DelProperty 指令](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md)。

 

