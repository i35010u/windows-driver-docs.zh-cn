---
title: 确定该属性设置为设备接口
description: 确定该属性设置为设备接口
ms.assetid: ef261c1d-0715-4501-b2db-fab270cee010
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1cba3efcfc8115e991f93b436d1c2a9c3744b7f6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542223"
---
# <a name="determining-which-properties-are-set-for-a-device-interface"></a>确定该属性设置为设备接口


若要确定哪些属性设置为在 Windows Vista 和更高版本的 Windows 设备接口，请执行以下步骤：

1.  调用[ **SetupDiGetDeviceInterfacePropertyKeys** ](https://msdn.microsoft.com/library/windows/hardware/ff551959)确定多少属性设置为设备类。 提供以下参数值：

    -   设置*DeviceInfoSet*到设备的信息集，其中包含要检索的设备接口属性键列表的设备接口实例的句柄。
    -   设置*DeviceInterfaceData*指向的[ **SP_DEVICE_INTERFACE_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552342)结构，它表示要为其检索一组设备接口实例设备属性键。
    -   设置*PropertyKeyArray*到**NULL**。
    -   设置*PropertyKeyCount*为零。
    -   设置*RequiredPropertyKeyCount*到指向 DWORD 类型的变量的指针。
    -   将标志设置为零。

    此调用的响应[ **SetupDiGetDeviceInterfacePropertyKeys**](https://msdn.microsoft.com/library/windows/hardware/ff551959)， **SetupDiGetDeviceInterfacePropertyKeys**设置\* *RequiredPropertyKeyCount*到设置的设备接口的属性的数目，日志错误代码 ERROR_INSUFFICIENT_BUFFER，并返回**FALSE**。 随后调用[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)将返回最近记录的错误代码。

2.  调用**SetupDiGetDeviceInterfacePropertyKeys**试并提供在第一个调用中，除以下更改外提供了相同的参数值：
    -   设置*PropertyKeyArray*到[ **DEVPROPKEY**](https://msdn.microsoft.com/library/windows/hardware/ff543544)-类型化的指针，指向该缓冲区用于接收请求的属性键数组。
    -   设置*PropertyKeyCount*到的大小，以 DEVPROPKEY 类型化值的*PropertyKeyArray*缓冲区。 首次调用**SetupDiGetDeviceInterfacePropertyKeys**检索所需的大小*PropertyKeyArray*中的缓冲区\* *RequiredPropertyKeyCount*.

如果第二个调用**SetupDiGetDeviceInterfacePropertyKeys**成功， **SetupDiGetDeviceInterfacePropertyKeys**返回请求的属性中的键数组*PropertyKeyArray*缓冲集\* *RequiredPropertyKeyCount*到的缓冲区，并返回的属性键的数目**TRUE**。 如果函数调用失败， **SetupDiGetDeviceInterfacePropertyKeys**返回**FALSE**并调用[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)将返回的记录的错误代码。

 

 





