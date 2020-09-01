---
title: 确定为设备类设置哪些属性
description: 确定为设备类设置哪些属性
ms.assetid: a8016b04-ae52-47d9-b3ef-74e0896aa825
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d44a62a34ea3199b39922798dd17cd6500b4afc5
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095975"
---
# <a name="determining-which-properties-are-set-for-a-device-class"></a>确定为设备类设置哪些属性


以下主题介绍如何在 Windows Vista 和更高版本的 Windows 中确定为设备类设置了哪些类属性：

[确定为本地计算机上的设备类设置的类属性](#determining-which-class-properties-are-set-for-a-device-class-on-a-loc)

[确定为远程计算机上的设备类设置了哪些类属性](#determining-which-class-properties-are-set-for-a-device-class-on-a-rem)

### <a name="determining-which-class-properties-are-set-for-a-device-class-on-a-local-computer"></a><a href="" id="determining-which-class-properties-are-set-for-a-device-class-on-a-loc"></a> 确定为本地计算机上的设备类设置的类属性

若要确定为本地计算机上的设备类设置的属性，请执行以下步骤：

1.  调用 [**SetupDiGetClassPropertyKeys**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertykeys) ，以确定为设备类设置了多少个属性。 提供以下参数值：

    -   将 *ClassGuid* 设置为一个指向 GUID 的指针，该 GUID 标识要为其检索类属性键列表的 [设备安装程序类](./overview-of-device-setup-classes.md) 或 [设备接口类](./overview-of-device-interface-classes.md) 。
    -   将 *PropertyKeyArray* 设置为 **NULL**。
    -   将 *PropertyKeyCount* 设置为零。
    -   将 *RequiredPropertyKeyCount* 设置为指向 DWORD 类型化变量的指针。
    -   如果设备类是设备安装程序类，请将 *Flags* 设置为 DICLASSPROP_INSTALLER;否则，如果设备类是设备接口类，请将 *Flags* 设置为 DICLASSPROP_INTERFACE。

    在对[**SetupDiGetClassPropertyKeys**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertykeys)的第一次调用时， **SetupDiGetClassPropertyKeys**将 \* *RequiredPropertyKeyCount*设置为设备安装程序类设置的属性数，将错误代码记录 ERROR_INSUFFICIENT_BUFFER，并返回**FALSE**。 对 [GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416) 的后续调用将返回最近记录的错误代码。

2.  再次调用 **SetupDiGetDevicePropertyKeys** ，并提供在第一次调用中提供的相同参数，但以下更改除外：
    -   将 *PropertyKeyArray* 设置为 [**DEVPROPKEY**](./devpropkey.md)类型的指针，该指针指向接收请求的属性键数组的缓冲区。
    -   将 *PropertyKeyCount* 设置为 *PropertyKeyArray* 缓冲区的大小，采用 DEVPROPKEY 类型的值。 第一次调用**SetupDiGetClassPropertyKeys**时，返回 RequiredPropertyKeyCount 中*PropertyKeyArray*缓冲区的所需大小 \* *RequiredPropertyKeyCount*。

如果对**SetupDiGetClassPropertyKeys**的第二次调用成功，则该函数将返回*PropertyKeyArray*缓冲区中请求的属性键数组，将 \* *RequiredPropertyKeyCount*设置为缓冲区中的属性键的数目，并返回**TRUE**。 如果函数调用失败， **SetupDiGetClassPropertyKeys** 将返回 **FALSE** ，并且对 [GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416) 的调用将返回记录的错误代码。

### <a name="determining-which-class-properties-are-set-for-a-device-class-on-a-remote-computer"></a><a href="" id="determining-which-class-properties-are-set-for-a-device-class-on-a-rem"></a> 确定为远程计算机上的设备类设置了哪些类属性

若要确定为远程计算机上的设备类设置的类属性，请按照 [确定为本地计算机上的设备类设置的类](#determining-which-class-properties-are-set-for-a-device-class-on-a-loc) 属性中所述的过程进行以下修改：

-   调用 [**SetupDiGetClassPropertyKeysEx**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertykeysexw) 而不是 [**SetupDiGetClassPropertyKeys**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertykeys)。

-   除了提供[**SetupDiGetClassPropertyKeysEx**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertykeysexw)和[**SetupDiGetClassPropertyKeys**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertykeys)所需的参数值外，还需提供*MachineName*参数，该参数必须设置为指向以 NULL 结尾的字符串的指针，该字符串包含计算机的 UNC 名称，包括 \\ \\ 前缀。

 

