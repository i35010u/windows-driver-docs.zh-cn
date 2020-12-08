---
title: 检索设备类属性值
description: 检索设备类属性值
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ebbe0427265950bd93f96495836c67fb01bc5f0e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818891"
---
# <a name="retrieving-a-device-class-property-value"></a>检索设备类属性值


以下主题介绍如何在 Windows Vista 和更高版本的 Windows 中检索设备类属性值：

[检索本地计算机上的设备类属性值](#retrieving-a-device-class-property-value-on-a-local-computer)

[检索远程计算机上的设备类属性值](#retrieving-a-device-class-property-value-on-a-remote-computer)

### <a name="retrieving-a-device-class-property-value-on-a-local-computer"></a><a href="" id="retrieving-a-device-class-property-value-on-a-local-computer"></a> 检索本地计算机上的设备类属性值

若要检索本地计算机上设备类属性的值，请执行以下步骤：

1.  调用 [**SetupDiGetClassProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclasspropertyw) 以确定属性值的数据类型和大小（以字节为单位）。 提供以下参数值：

    -   将 *ClassGuid* 设置为指向 GUID 的指针，该 GUID 标识要为其检索为设备类设置的类属性的 [设备安装程序类](./overview-of-device-setup-classes.md) 或 [设备接口类](./overview-of-device-interface-classes.md) 。
    -   将 *PropertyKey* 设置为指向表示属性的 [**DEVPROPKEY**](./devpropkey.md) 结构的指针。
    -   将 *PropertyType* 设置为指向 [**DEVPROPTYPE**](/previous-versions/ff543546(v=vs.85))类型的变量的指针。
    -   将 *PropertyBuffer* 设置为 **NULL**。
    -   将 *PropertyBufferSize* 设置为零。
    -   将 *RequiredSize* 设置为 DWORD 类型化变量。
    -   如果设备类是设备安装程序类，请将 *Flags* 设置为 DICLASSPROP_INSTALLER。 否则，如果设备类是设备接口类，请将 *Flags* 设置为 DICLASSPROP_INTERFACE。

    在对 [**SetupDiGetClassProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclasspropertyw)的第一次调用时， **SetupDiGetClassProperty** 将 \* *RequiredSize* 设置为检索属性值所需的缓冲区大小（以字节为单位），记录错误代码 ERROR_INSUFFICIENT_BUFFER 并返回 **FALSE**。 对 [GetLastError](/windows/win32/api/errhandlingapi/nf-errhandlingapi-getlasterror) 的后续调用将返回最近记录的错误代码。

2.  再次调用 **SetupDiGetClassProperty** ，并提供在第一次调用中提供的相同参数，但以下更改除外：
    -   将 *PropertyBuffer* 设置为指向接收属性值的缓冲区的指针。
    -   将 *PropertyBufferSize* 设置为 *PropertyBuffer* 缓冲区的所需大小（以字节为单位）。 第一次调用 **SetupDiGetClassProperty** 时，检索到 RequiredSize 中的 *PropertyBuffer* 缓冲区的所需大小 \* *RequiredSize*。

如果对 **SetupDiGetClassProperty** 的第二次调用成功，则 **SetupDiGetClassProperty** 将 \* *PropertyType* 设置为属性的属性数据类型标识符，将 *PropertyBuffer* 缓冲区设置为属性值，将 \* *RequiredSize* 设置为检索到的属性值的大小（以字节为单位），并返回 **TRUE**。 如果函数调用失败， **SetupDiGetDeviceProperty** 将返回 **FALSE** ，并且对 [GetLastError](/windows/win32/api/errhandlingapi/nf-errhandlingapi-getlasterror) 的调用将返回记录的错误代码。

### <a name="retrieving-a-device-class-property-value-on-a-remote-computer"></a><a href="" id="retrieving-a-device-class-property-value-on-a-remote-computer"></a> 检索远程计算机上的设备类属性值

若要检索远程计算机上的设备类属性值，请遵循在 [本地计算机上检索设备类属性值](#retrieving-a-device-class-property-value-on-a-local-computer) 中所述的相同过程进行以下修改：

-   调用 [**SetupDiGetClassPropertyEx**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclasspropertyexw) 而不是 **SetupDiGetClassProperty**。

-   除了提供 **SetupDiGetDevicePropertyEx** 和 **SetupDiGetClassProperty** 都需要的参数值，还需要提供 *MachineName* 参数，该参数必须设置为指向以 NULL 结尾的字符串的指针，该字符串包含计算机的 UNC 名称，包括 \\ \\ 前缀。

