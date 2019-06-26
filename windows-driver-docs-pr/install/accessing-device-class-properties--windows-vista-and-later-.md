---
title: 访问设备类属性
description: 访问设备类属性
ms.assetid: 51eef1f4-ca7d-46ab-a33f-be53de277541
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e583302d1feebb5f57d8d5ba26b80425a92a21b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385633"
---
# <a name="accessing-device-class-properties"></a>访问设备类属性


在 Windows Vista 和更高版本的 Windows 中，应用程序和安装程序可以访问[设备安装程序类属性](https://docs.microsoft.com/previous-versions/ff542239(v=vs.85))并[设备接口类属性](https://docs.microsoft.com/previous-versions/ff541406(v=vs.85))通过调用以下安装程序 Api函数：

-   [**SetupDiGetClassPropertyKeys** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertykeys)并[ **SetupDiGetClassPropertyKeysEx**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertykeysexw)

    **SetupDiGetClassPropertyKeys**函数检索标识的类属性的当前设置在本地计算机上的设备安装程序类或设备接口类的类属性键的数组。 **SetupDiGetClassPropertyKeysEx**函数执行本地计算机或远程计算机上相同的操作。 有关如何确定哪些属性设置为设备类的信息，请参阅[确定该属性设置为设备类](determining-which-properties-are-set-for-a-device-class.md)。

-   [**SetupDiGetClassProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)

    **SetupDiGetClassProperty**函数[检索类属性](retrieving-a-device-class-property-value.md)设备安装程序类或设备接口类。 [ **SetupDiGetClassPropertyEx** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)函数执行本地计算机上相同的操作方式与其在远程计算机上。

-   [**SetupDiSetClassProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetclasspropertyw)

    **SetupDiSetClassProperty**函数[设置为设备安装程序类或设备接口类的类属性](setting-a-device-class-property-value.md)。 [ **SetupDiSetClassPropertyEx** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetclasspropertyexw)函数执行本地计算机上相同的操作方式与其在远程计算机上。

有关如何访问设备类属性对 Windows Server 2003、 Windows XP 和 Windows 2000 上的信息，请参阅[访问设备安装程序类属性](accessing-device-setup-class-properties.md)和[访问设备接口类属性](accessing-device-interface-class-properties.md).

 

 





