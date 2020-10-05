---
title: 检索 SPCRP_Xxx 属性
description: 检索 SPCRP_Xxx 属性
ms.assetid: a5d52da9-a593-42bd-aeaf-8ab203bc3d21
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06cc906731aeddb471e0bd40845c785b70b6467b
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733691"
---
# <a name="retrieving-spcrp_xxx-properties"></a>检索 SPCRP_Xxx 属性


在 Windows Vista 和更高版本的 Windows 中， [统一设备属性模型](unified-device-property-model--windows-vista-and-later-.md) 支持与 *setupapi.log*中定义的 SPCRP_Xxx 标识符对应的设备实例属性。 这些属性描述 [设备安装程序类](./overview-of-device-setup-classes.md)的特征。 统一设备属性模型使用 [属性键](property-keys.md) 来表示这些属性。

Windows Server 2003、Windows XP 和 Windows 2000 还支持其中的大多数设备安装程序类属性。 但是，这些早期版本的 Windows 不支持统一设备属性模型的属性键。 相反，这些版本的 Windows 版本使用 SPCRP_*Xxx* 标识符来表示和访问设备安装程序类属性。 为了保持与早期版本的 Windows 的兼容性，Windows Vista 及更高版本还支持使用 SPCRP_*Xxx* 标识符来访问设备安装程序类属性。 但是，你应该使用统一设备属性模型的属性键来访问设备安装程序类属性。

有关系统定义的设备安装程序类属性的列表，请参阅 [与 SPCRP_Xxx 标识符对应的设备安装程序类属性](/previous-versions/ff542245(v=vs.85))。 设备安装程序类属性由用于访问 Windows Vista 和更高版本中的属性的属性键标识符列出。 使用属性键提供的信息还包括相应的 SPCRP_*Xxx* 标识符，可用于访问 windows Server 2003、windows XP 和 windows 2000 上的属性。

有关如何使用属性键访问 Windows Vista 和更高版本中的设备安装程序类属性的信息，请参阅 [访问设备类属性 (Windows vista 和更高版本) ](accessing-device-class-properties--windows-vista-and-later-.md)。

若要在 Windows Server 2003、Windows XP 和 Windows 2000 上检索设备安装程序类属性，请使用 [**SetupDiGetClassRegistryProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclassregistrypropertya) 函数。

若要使用 SetupDiGetClassRegistryProperty 检索与 SPCRP_Xxx 标识符对应的属性，请执行以下步骤：

1.  调用 **SetupDiGetClassRegistryProperty** 并提供以下参数值：

    -   将 *ClassGuid* 设置为指向表示要为其检索属性的设备安装程序类的 GUID 的指针。
    -   将 *属性* 设置为要检索其属性值大小的前缀为 "SPCRP_" 的属性标识符。
    -   将 *PropertyRegDataType* 设置为 **NULL**。
    -   将 *PropertyBuffer* 设置为 **NULL**。
    -   将 *PropertyBufferSize* 设置为零。
    -   将 *RequiredSize* 设置为指向 DWORD 类型的变量的指针，该变量接收所请求属性的大小（以字节为单位）。
    -   将 *MachineName* 设置为计算机的名称。
    -   将保留设置为 **NULL**。

    在响应对[**SetupDiGetClassRegistryProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclassregistrypropertya)的调用时， **SetupDiGetClassRegistryProperty**将 \* *RequiredSize*设置为检索属性值所需的缓冲区大小（以字节为单位），记录错误代码 ERROR_INSUFFICIENT_BUFFER 并返回**FALSE**。 对 [GetLastError](/windows/win32/api/errhandlingapi/nf-errhandlingapi-getlasterror) 的后续调用将返回最近记录的错误代码。

2.  再次调用 **SetupDiGetClassRegistryProperty** 来检索属性值，并提供在第一个调用中提供的相同参数，但以下更改除外：
    -   将 *PropertyBuffer* 设置为指向接收属性值的缓冲区的指针。
    -   将 *PropertyBufferSize* 设置为 *PropertyBuffer* 缓冲区的大小（以字节为单位）。 第一次调用**SetupDiGetClassRegistryProperty**时，检索到 RequiredSize 中的*PropertyBuffer*缓冲区的所需大小 \* *RequiredSize*。

如果对**SetupDiGetClassRegistryProperty**的第二次调用成功，则**SetupDiGetClassRegistryProperty**将 \* *PropertyRegDataType*设置为 registry 数据类型，将*PropertyBuffer*缓冲区设置为属性值，将 \* *PropertyBufferSize*设置为属性值的大小（以字节为单位），并返回**TRUE**。 如果函数调用失败， **SetupDiGetClassRegistryProperty** 将返回 **FALSE** ，并且对 [GetLastError](/windows/win32/api/errhandlingapi/nf-errhandlingapi-getlasterror) 的调用将返回记录的错误代码。

