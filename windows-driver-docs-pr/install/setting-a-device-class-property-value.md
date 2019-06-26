---
title: 设置设备类属性值
description: 设置设备类属性值
ms.assetid: a1d6908d-e43a-413d-965b-3af226d5c26f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1c3fb136336ecd1e6a5504021b0bf1bb440adfe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386892"
---
# <a name="setting-a-device-class-property-value"></a>设置设备类属性值


以下主题介绍如何在 Windows Vista 和更高版本的 Windows 中设置设备类属性值：

[在本地计算机上设置设备类属性值](#setting-a-device-class-property-value-on-a-local-computer)

[在远程计算机上设置设备类属性值](#setting-a-device-class-property-value-on-a-remote-computer)

### <a href="" id="setting-a-device-class-property-value-on-a-local-computer"></a> 在本地计算机上设置设备类属性值

若要设置的设备类属性值，请调用[ **SetupDiSetClassProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetclasspropertyw) ，并提供以下参数值：

-   设置*ClassGuid*标识的 GUID 是指向[设备安装程序类](device-setup-classes.md)或[设备接口类](device-interface-classes.md)为其设置的类属性。

-   设置*PropertyKey*指向的[ **DEVPROPKEY** ](https://docs.microsoft.com/windows-hardware/drivers/install/devpropkey)结构，它表示要设置的属性。

-   设置*PropertyType*指向的[ **DEVPROPTYPE**](https://docs.microsoft.com/previous-versions/ff543546(v=vs.85))-提供要设置的属性的属性数据类型标识符的类型化的变量。

-   设置*PropertyBuffer*到指向包含的属性值的缓冲区的指针。

-   设置*PropertyBufferSize*到大小 （字节） 的属性值。

-   设置*RequiredSize*到 DWORD 类型的变量。

-   如果设备安装程序类的设备类，则设置*标志*DICLASSPROP_INSTALLER 到。 否则，如果设备接口类的设备类，则设置*标志*DICLASSPROP_INTERFACE 到。

如果调用[ **SetupDiSetClassProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetclasspropertyw)成功， **SetupDiSetClassProperty**设置的设备类属性，并返回**TRUE**. 如果函数调用失败， **SetupDiSetClassProperty**返回**FALSE**并调用[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)将返回的记录的错误代码。

### <a href="" id="setting-a-device-class-property-value-on-a-remote-computer"></a> 在远程计算机上设置设备类属性值

若要在远程计算机上设置设备类属性值，请按照中所述的过程[在本地计算机上设置设备类属性值](#setting-a-device-class-property-value-on-a-local-computer)并进行以下修改：

-   调用[ **SetupDiSetClassPropertyEx** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetclasspropertyexw)而不是**SetupDiSetClassProperty**。

-   除了提供参数值，同时**SetupDiSetClassPropertyEx**并**SetupDiSetClassProperty**需要，提供*MachineName*参数，它必须设置为指向以 NULL 结尾的字符串包含 UNC 名称，包括\\\\前缀，一台计算机。

 

 





