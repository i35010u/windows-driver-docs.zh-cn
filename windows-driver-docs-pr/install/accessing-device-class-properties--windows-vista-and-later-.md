---
title: 访问设备类属性
description: 访问设备类属性
ms.assetid: 51eef1f4-ca7d-46ab-a33f-be53de277541
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f3e9c0638caa906c9ef33b0c168dbfb1690277f
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715962"
---
# <a name="accessing-device-class-properties"></a>访问设备类属性


在 Windows Vista 和更高版本的 Windows 中，应用程序和安装程序可以通过调用以下 Setupapi.log 函数来访问 [设备安装程序类属性](/previous-versions/ff542239(v=vs.85)) 和 [设备接口类属性](/previous-versions/ff541406(v=vs.85)) ：

-   [**SetupDiGetClassPropertyKeys**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclasspropertykeys)和[ **SetupDiGetClassPropertyKeysEx**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclasspropertykeysexw)

    **SetupDiGetClassPropertyKeys**函数检索类属性键的数组，这些键用于标识当前为设备安装程序类或本地计算机上的设备接口类设置的类属性。 **SetupDiGetClassPropertyKeysEx**函数在本地计算机或远程计算机上执行相同的操作。 有关如何确定为设备类设置的属性的信息，请参阅确定为 [设备类设置的属性](determining-which-properties-are-set-for-a-device-class.md)。

-   [**SetupDiGetClassProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclasspropertyw)

    **SetupDiGetClassProperty**函数检索设备安装程序类或设备接口类的[类属性](retrieving-a-device-class-property-value.md)。 [**SetupDiGetClassPropertyEx**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)函数在本地计算机上执行与在远程计算机上执行相同的操作。

-   [**SetupDiSetClassProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdisetclasspropertyw)

    **SetupDiSetClassProperty**函数[为设备安装程序类或设备接口类设置类属性](setting-a-device-class-property-value.md)。 [**SetupDiSetClassPropertyEx**](/windows/win32/api/setupapi/nf-setupapi-setupdisetclasspropertyexw)函数在本地计算机上执行与在远程计算机上执行相同的操作。

有关如何在 Windows Server 2003、Windows XP 和 Windows 2000 上访问设备类属性的信息，请参阅 [访问设备安装程序类属性](accessing-device-setup-class-properties.md) 和 [访问设备接口类属性](accessing-device-interface-class-properties.md)。

 

