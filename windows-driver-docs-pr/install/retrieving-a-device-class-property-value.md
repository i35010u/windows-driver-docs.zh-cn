---
title: 检索设备类属性值
description: 检索设备类属性值
ms.assetid: 50b16bd9-7f38-4128-af8f-8b39b099931f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a305bdf1de39ecbc277910b808dd51f00ac816d2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520777"
---
# <a name="retrieving-a-device-class-property-value"></a>检索设备类属性值


以下主题介绍如何检索 Windows Vista 和更高版本的 Windows 中的设备类属性值：

[检索本地计算机上的设备类属性值](#retrieving-a-device-class-property-value-on-a-local-computer)

[检索远程计算机上的设备类属性值](#retrieving-a-device-class-property-value-on-a-remote-computer)

### <a href="" id="retrieving-a-device-class-property-value-on-a-local-computer"></a> 检索本地计算机上的设备类属性值

若要检索本地计算机上的设备类属性的值，请按照下列步骤：

1.  调用[ **SetupDiGetClassProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551086)来确定数据类型和大小 （字节） 的属性值。 提供以下参数值：

    -   设置*ClassGuid*标识的 GUID 是指向[设备安装程序类](device-setup-classes.md)或[设备接口类](device-interface-classes.md)要检索的类属性，为设备设置类。
    -   设置*PropertyKey*指向的[ **DEVPROPKEY** ](https://msdn.microsoft.com/library/windows/hardware/ff543544)结构，它表示该属性。
    -   设置*PropertyType*指向的[ **DEVPROPTYPE**](https://msdn.microsoft.com/library/windows/hardware/ff543546)-类型化的变量中。
    -   设置*PropertyBuffer*到**NULL**。
    -   设置*PropertyBufferSize*为零。
    -   设置*RequiredSize*到 DWORD 类型的变量。
    -   如果设备安装程序类的设备类，则设置*标志*DICLASSPROP_INSTALLER 到。 否则，如果设备接口类的设备类，则设置*标志*DICLASSPROP_INTERFACE 到。

    在此第一次调用的响应[ **SetupDiGetClassProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551086)， **SetupDiGetClassProperty**设置\* *RequiredSize*大小，以字节为单位，检索属性值，所需的缓冲区的记录的错误代码 ERROR_INSUFFICIENT_BUFFER，并返回**FALSE**。 随后调用[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)将返回最近记录的错误代码。

2.  调用**SetupDiGetClassProperty**试并提供相同的第一个调用中，除以下更改外中提供的参数：
    -   设置*PropertyBuffer*到指向该缓冲区用于接收的属性值的指针。
    -   设置*PropertyBufferSize*到所需的大小，以字节为单位的*PropertyBuffer*缓冲区。 首次调用**SetupDiGetClassProperty**检索所需的大小*PropertyBuffer*中的缓冲区\* *RequiredSize*。

如果第二个调用**SetupDiGetClassProperty**成功， **SetupDiGetClassProperty**设置\* *PropertyType*为属性数据类型标识符对于属性，设置*PropertyBuffer*属性值设置到缓冲区\* *RequiredSize*大小，以字节为单位，属性值用于已检索，并返回 **，则返回 TRUE**。 如果函数调用失败， **SetupDiGetDeviceProperty**返回**FALSE**并调用[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)将返回的记录的错误代码。

### <a href="" id="retrieving-a-device-class-property-value-on-a-remote-computer"></a> 检索远程计算机上的设备类属性值

若要检索远程计算机上的设备类属性值，请先按照相同的步骤，如中所述[检索本地计算机上的设备类属性值](#retrieving-a-device-class-property-value-on-a-local-computer)并进行以下修改：

-   调用[ **SetupDiGetClassPropertyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551090)而不是**SetupDiGetClassProperty**。

-   除了提供参数值**SetupDiGetDevicePropertyEx**并**SetupDiGetClassProperty**这两种需要，提供*MachineName*参数，它必须设置为指向以 NULL 结尾的字符串包含 UNC 名称，包括\\\\前缀，一台计算机。

 

 





