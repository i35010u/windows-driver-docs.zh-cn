---
title: 创建自定义设备属性
description: 创建自定义设备属性
ms.assetid: e18fcbe8-6083-451e-b1be-5a543b61c627
keywords:
- 设备属性 WDK 设备安装，创建自定义
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ec294e7d9e6dacaa47fdb9e7d8de8664aa4d0fd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547073"
---
# <a name="creating-custom-device-properties"></a>创建自定义设备属性


在 Windows Vista 和更高版本的 Windows，[统一的设备属性模型](unified-device-property-model--windows-vista-and-later-.md)支持为设备实例创建自定义设备属性类别[设备安装程序类](device-setup-classes.md)，设备类和设备接口的接口。 自定义属性可以访问通过调用适当[SetupAPI 属性函数](https://msdn.microsoft.com/library/windows/hardware/ff541483)。 此外可以通过使用修改的自定义设备属性[ **INF AddProperty 指令**](inf-addproperty-directive.md)或[ **INF DelProperty 指令**](inf-delproperty-directive.md)。

有关自定义设备属性的详细信息，请参阅以下主题：

[创建自定义设备属性类别](#creating-custom-device-property-categories)

[使用 SetupAPI 属性函数访问自定义设备属性](#using-the-setupapi-property-functions-to-access-custom-device-properti)

[使用 INF AddProperty 指令或 INF DelProperty 指令来修改自定义设备属性](#using-the-inf-addproperty-directive-or-the-inf-delproperty-directive-t)

### <a href="" id="creating-custom-device-property-categories"></a> 创建自定义设备属性类别

自定义设备的属性类别是逻辑上相关的自定义设备属性的集合。 若要以编程方式创建自定义设备的属性类别，请使用[ **DEFINE_DEVPROPKEY** ](https://msdn.microsoft.com/library/windows/hardware/ff541072)宏来创建表示属性类别中的属性，如下所示的属性关键字：

-   创建唯一的 GUID 值，该值表示的属性类别并将每个属性密钥的 GUID 值设置为此唯一的 GUID 值。 有关如何创建新的 GUID 值的信息，请参阅[定义和导出新的 Guid](https://msdn.microsoft.com/library/windows/hardware/ff542998)。

    **请注意**  仅用于操作系统保留的系统定义的属性类别。

     

-   将每个属性键的属性标识符设置为一个整数值的属性类别中是唯一的而这是大于或等于 2。

此外可以通过使用创建的设备实例自定义设备的属性类别[ **INF AddProperty 指令**](inf-addproperty-directive.md)。

### <a href="" id="using-the-setupapi-property-functions-to-access-custom-device-properti"></a> 使用 SetupAPI 属性函数访问自定义设备属性

相同的方式访问自定义设备属性，如中所述[以访问设备的属性 （Windows Vista 和更高版本） 使用 SetupAPI](using-setupapi-to-access-device-properties--windows-vista-and-later-.md)。 访问自定义设备属性时，将应用以下其他注意事项：

-   **SetupDiGetXxxPropertyKeys**并**SetupDiGetXxxPropertyKeysEx**函数检索的系统定义的设备属性键和表示的属性的自定义设备属性键为组件设置。

-   **SetupDiSetXxxProperty**函数将设置为组件的自定义设备属性。 Windows 的自定义设备属性键、 属性数据类型和属性值在内部将相关联。 如果已设置具有相同的属性键的自定义设备属性， **SetupDiSetXxxProperty**函数将覆盖属性值和与属性关联的属性数据类型。

-   **SetupDiGetXxxProperty**函数检索为组件设置的自定义设备属性。 **SetupDiGetXxxProperty**函数检索属性值和属性已设置时所设置的属性数据类型。

### <a href="" id="using-the-inf-addproperty-directive-or-the-inf-delproperty-directive-t"></a> 使用 INF AddProperty 指令或 INF DelProperty 指令来修改自定义设备属性

若要使用修改的自定义设备属性[ **INF AddProperty 指令**](inf-addproperty-directive.md)，在安装该组件的部分中包括 AddProperty 指令，并提供了以下项的属性:

-   *属性类别 guid*表示自定义设备的属性类别的项

-   标识自定义设备的属性类别中的属性的属性标识符项

-   *值*的新设备属性的条目或*值*修改现有的设备属性值的条目

使用[ **INF DelProperty 指令**](inf-delproperty-directive.md)删除自定义设备属性。

有关如何使用这些指令的详细信息，请参阅[INF AddProperty 指令和 INF DelProperty 指令](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md)。

 

 





