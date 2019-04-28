---
title: 确定为设备类设置哪些属性
description: 确定为设备类设置哪些属性
ms.assetid: a8016b04-ae52-47d9-b3ef-74e0896aa825
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08fc5374cf0be9ccdf03a82dbcd69dde2793bfbb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346177"
---
# <a name="determining-which-properties-are-set-for-a-device-class"></a>确定为设备类设置哪些属性


以下主题介绍如何确定哪些类属性设置为 Windows Vista 和更高版本的 Windows 中的设备类：

[确定本地计算机上的设备类设置哪些类属性](#determining-which-class-properties-are-set-for-a-device-class-on-a-loc)

[确定远程计算机上的设备类设置哪些类属性](#determining-which-class-properties-are-set-for-a-device-class-on-a-rem)

### <a href="" id="determining-which-class-properties-are-set-for-a-device-class-on-a-loc"></a> 确定本地计算机上的设备类设置哪些类属性

若要确定本地计算机上设置设备类的属性，请执行以下步骤：

1.  调用[ **SetupDiGetClassPropertyKeys** ](https://msdn.microsoft.com/library/windows/hardware/ff551091)确定多少属性设置为设备类。 提供以下参数值：

    -   设置*ClassGuid*标识的 GUID 是指向[设备安装程序类](device-setup-classes.md)或[设备接口类](device-interface-classes.md)要检索的类属性键的列表。
    -   设置*PropertyKeyArray*到**NULL**。
    -   设置*PropertyKeyCount*为零。
    -   设置*RequiredPropertyKeyCount*到指向 DWORD 类型的变量的指针。
    -   如果设备安装程序类的设备类，则设置*标志*到 DICLASSPROP_INSTALLER; 否则，如果设备类设备接口类，则设置*标志*DICLASSPROP_INTERFACE 到。

    在此第一次调用的响应[ **SetupDiGetClassPropertyKeys**](https://msdn.microsoft.com/library/windows/hardware/ff551091)， **SetupDiGetClassPropertyKeys**设置\* *RequiredPropertyKeyCount*到设备安装程序类设置的属性的数目，日志错误代码 ERROR_INSUFFICIENT_BUFFER，并返回**FALSE**。 随后调用[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)将返回最近记录的错误代码。

2.  调用**SetupDiGetDevicePropertyKeys**试并提供相同的第一个调用中，除以下更改外中提供的参数：
    -   设置*PropertyKeyArray*到[ **DEVPROPKEY**](https://msdn.microsoft.com/library/windows/hardware/ff543544)-类型化的指针，指向该缓冲区用于接收请求的属性键数组。
    -   设置*PropertyKeyCount*到的大小，以 DEVPROPKEY 类型化值的*PropertyKeyArray*缓冲区。 首次调用**SetupDiGetClassPropertyKeys**返回的所需的大小*PropertyKeyArray*中的缓冲区\* *RequiredPropertyKeyCount*。

如果第二个调用**SetupDiGetClassPropertyKeys**成功请求的属性键数组中该函数返回*PropertyKeyArray*缓冲集\* *RequiredPropertyKeyCount*到缓冲区，并返回的属性键的数目**TRUE**。 如果函数调用失败， **SetupDiGetClassPropertyKeys**返回**FALSE**并调用[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)将返回的记录的错误代码。

### <a href="" id="determining-which-class-properties-are-set-for-a-device-class-on-a-rem"></a> 确定远程计算机上的设备类设置哪些类属性

若要确定在远程计算机设置设备类的类属性，请按照中所述的过程[确定正是类属性被设置为本地计算机上的设备类](#determining-which-class-properties-are-set-for-a-device-class-on-a-loc)以下修改：

-   调用[ **SetupDiGetClassPropertyKeysEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551093)而不是[ **SetupDiGetClassPropertyKeys**](https://msdn.microsoft.com/library/windows/hardware/ff551091)。

-   除了提供这些参数值所需的同时[ **SetupDiGetClassPropertyKeysEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551093)并[ **SetupDiGetClassPropertyKeys**](https://msdn.microsoft.com/library/windows/hardware/ff551091)，提供*MachineName*参数，必须设置为指向包含 UNC 名称的以 NULL 结尾的字符串的指针，其中包括\\\\前缀，一台计算机。

 

 





