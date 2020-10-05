---
title: 设置设备类属性值
description: 设置设备类属性值
ms.assetid: a1d6908d-e43a-413d-965b-3af226d5c26f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69e34af3270b3e448b569cd4dd745f4783d1a538
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733688"
---
# <a name="setting-a-device-class-property-value"></a>设置设备类属性值


以下主题介绍如何在 Windows Vista 和更高版本的 Windows 中设置 "设备类" 属性值：

[在本地计算机上设置设备类属性值](#setting-a-device-class-property-value-on-a-local-computer)

[设置远程计算机上的设备类属性值](#setting-a-device-class-property-value-on-a-remote-computer)

### <a name="setting-a-device-class-property-value-on-a-local-computer"></a><a href="" id="setting-a-device-class-property-value-on-a-local-computer"></a> 在本地计算机上设置设备类属性值

若要设置设备类属性的值，请调用 [**SetupDiSetClassProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdisetclasspropertyw) 并提供以下参数值：

-   将 *ClassGuid* 设置为一个指向 GUID 的指针，该 GUID 标识要为其设置类属性的 [设备安装程序类](./overview-of-device-setup-classes.md) 或 [设备接口类](./overview-of-device-interface-classes.md) 。

-   将 *PropertyKey* 设置为指向 [**DEVPROPKEY**](./devpropkey.md) 结构的指针，该结构表示要设置的属性。

-   将 *PropertyType* 设置为指向 [**DEVPROPTYPE**](/previous-versions/ff543546(v=vs.85))类型的变量的指针，该变量提供要设置的属性的属性数据类型标识符。

-   将 *PropertyBuffer* 设置为指向包含属性值的缓冲区的指针。

-   将 *PropertyBufferSize* 设置为属性值的大小（以字节为单位）。

-   将 *RequiredSize* 设置为 DWORD 类型化变量。

-   如果设备类是设备安装程序类，请将 *Flags* 设置为 DICLASSPROP_INSTALLER。 否则，如果设备类是设备接口类，请将 *Flags* 设置为 DICLASSPROP_INTERFACE。

如果对 [**SetupDiSetClassProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdisetclasspropertyw) 的调用成功，则 **SetupDiSetClassProperty** 将设置设备类属性并返回 **TRUE**。 如果函数调用失败， **SetupDiSetClassProperty** 将返回 **FALSE** ，并且对 [GetLastError](/windows/win32/api/errhandlingapi/nf-errhandlingapi-getlasterror) 的调用将返回记录的错误代码。

### <a name="setting-a-device-class-property-value-on-a-remote-computer"></a><a href="" id="setting-a-device-class-property-value-on-a-remote-computer"></a> 设置远程计算机上的设备类属性值

若要设置远程计算机上的设备类属性值，请按照在 [本地计算机上设置设备类属性值](#setting-a-device-class-property-value-on-a-local-computer) 中所述的过程进行以下修改：

-   调用 [**SetupDiSetClassPropertyEx**](/windows/win32/api/setupapi/nf-setupapi-setupdisetclasspropertyexw) 而不是 **SetupDiSetClassProperty**。

-   除了提供**SetupDiSetClassPropertyEx**和**SetupDiSetClassProperty**所需的参数值外，还需提供*MachineName*参数，该参数必须设置为指向以 NULL 结尾的字符串的指针，该字符串包含计算机的 UNC 名称，包括 \\ \\ 前缀。

