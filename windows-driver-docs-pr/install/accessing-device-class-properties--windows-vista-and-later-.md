---
title: 访问设备类属性
description: 访问设备类属性
ms.assetid: 51eef1f4-ca7d-46ab-a33f-be53de277541
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b4d9683e54f8d53c587629e9f3821de976200d1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544408"
---
# <a name="accessing-device-class-properties"></a>访问设备类属性


在 Windows Vista 和更高版本的 Windows 中，应用程序和安装程序可以访问[设备安装程序类属性](https://msdn.microsoft.com/library/windows/hardware/ff542239)并[设备接口类属性](https://msdn.microsoft.com/library/windows/hardware/ff541406)通过调用以下安装程序 Api函数：

-   [**SetupDiGetClassPropertyKeys** ](https://msdn.microsoft.com/library/windows/hardware/ff551091)并[ **SetupDiGetClassPropertyKeysEx**](https://msdn.microsoft.com/library/windows/hardware/ff551093)

    **SetupDiGetClassPropertyKeys**函数检索标识的类属性的当前设置在本地计算机上的设备安装程序类或设备接口类的类属性键的数组。 **SetupDiGetClassPropertyKeysEx**函数执行本地计算机或远程计算机上相同的操作。 有关如何确定哪些属性设置为设备类的信息，请参阅[确定该属性设置为设备类](determining-which-properties-are-set-for-a-device-class.md)。

-   [**SetupDiGetClassProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551086)

    **SetupDiGetClassProperty**函数[检索类属性](retrieving-a-device-class-property-value.md)设备安装程序类或设备接口类。 [ **SetupDiGetClassPropertyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551090)函数执行本地计算机上相同的操作方式与其在远程计算机上。

-   [**SetupDiSetClassProperty**](https://msdn.microsoft.com/library/windows/hardware/ff552128)

    **SetupDiSetClassProperty**函数[设置为设备安装程序类或设备接口类的类属性](setting-a-device-class-property-value.md)。 [ **SetupDiSetClassPropertyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff552132)函数执行本地计算机上相同的操作方式与其在远程计算机上。

有关如何访问设备类属性对 Windows Server 2003、 Windows XP 和 Windows 2000 上的信息，请参阅[访问设备安装程序类属性](accessing-device-setup-class-properties.md)和[访问设备接口类属性](accessing-device-interface-class-properties.md).

 

 





