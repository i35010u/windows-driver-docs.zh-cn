---
title: 确定为设备实例设置哪些属性
description: 确定为设备实例设置哪些属性
ms.assetid: aeca4da5-9632-4523-aa2d-8d1c64b1eccc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a66cf363c690450895a432df3c2c9930864cf165
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374246"
---
# <a name="determining-which-properties-are-set-for-a-device-instance"></a>确定为设备实例设置哪些属性


若要确定哪些属性设置为在 Windows Vista 和更高版本的 Windows 上的设备实例，请执行以下步骤：

1.  调用[ **SetupDiGetDevicePropertyKeys** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertykeys)确定多少属性设置为设备实例。 提供以下参数值：

    -   设置*DeviceInfoSet*到设备的信息集，其中包含要检索的属性键列表的设备实例的句柄。
    -   设置*DeviceInfoData*指向的[ **SP_DEVINFO_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)结构，它表示要检索的属性键列表的设备实例。
    -   设置*PropertyKeyArray*到**NULL**。
    -   设置*PropertyKeyCount*为零。
    -   设置*RequiredPropertyKeyCount*到指向 DWORD 类型的变量的指针。
    -   设置*标志*为零。

    以响应对的调用[ **SetupDiGetDevicePropertyKeys**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertykeys)， **SetupDiGetDevicePropertyKeys**设置\* *RequiredPropertyKeyCount*到设备实例设置的属性的数目，日志错误代码 ERROR_INSUFFICIENT_BUFFER，并返回**FALSE**。 随后调用[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)将返回最近记录的错误代码。

2.  调用**SetupDiGetDevicePropertyKeys**试并提供在第一个调用中，除以下更改外提供了相同的参数值：

    -   设置*PropertyKeyArray*作为[ **DEVPROPKEY**](https://docs.microsoft.com/windows-hardware/drivers/install/devpropkey)-类型化的指针，指向该缓冲区用于接收请求的属性键数组。
    -   设置*PropertyKeyCount*到的大小，以 DEVPROPKEY 类型化值的*PropertyKeyArray*缓冲区。 首次调用**SetupDiGetDevicePropertyKeys**检索所需的大小*PropertyKeyArray*中的缓冲区\* *RequiredPropertyKeyCount*。

如果第二个调用**SetupDiGetDevicePropertyKeys**成功， **SetupDiGetDevicePropertyKeys**返回请求的属性中的键数组*PropertyKeyArray*缓冲集\* *RequiredPropertyKeyCount*到的缓冲区，并返回的属性键的数目**TRUE**。 如果函数调用失败， **SetupDiGetDevicePropertyKeys**返回**FALSE**并调用[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=74036)将返回的记录的错误代码。

 

 





