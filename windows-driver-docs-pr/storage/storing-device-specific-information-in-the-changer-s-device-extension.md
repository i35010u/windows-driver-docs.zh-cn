---
title: 将特定于设备的信息存储在换带机的设备扩展
description: 将特定于设备的信息存储在换带机的设备扩展
ms.assetid: 72048d84-1c2d-4f3c-b5e8-f55a812ad567
keywords:
- 更换器驱动程序 WDK 存储特定于设备的数据存储
- 存储更换器驱动程序 WDK，特定于设备的数据存储
- 特定于设备的数据存储 WDK 换带机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38ed70319bd7c22cc20044f0a63296e6538674b0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525493"
---
# <a name="storing-device-specific-information-in-the-changers-device-extension"></a>将特定于设备的信息存储在换带机的设备扩展


## <span id="ddk_storing_device_specific_information_in_the_changers_device_extensi"></span><span id="DDK_STORING_DEVICE_SPECIFIC_INFORMATION_IN_THE_CHANGERS_DEVICE_EXTENSI"></span>


换带机 miniclass 驱动程序指定它需要使用特定于设备的数据中的存储其[ **ChangerAdditionalExtensionSize** ](https://msdn.microsoft.com/library/windows/hardware/ff551400)例程。 转换器类驱动程序分配请求的存储代表换带机 miniclass 驱动程序，然后调用 miniclass 驱动程序[ **ChangerInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff551431)例程。

换带机 miniclass 驱动程序是否将数据存储在设备扩展以及哪些数据，它将存储，由驱动程序设计器。 它通常包括 SCSI 查询数据或转换器设备的非 SCSI 等效项。

设备扩展还可能包含 miniclass 驱动程序使用特定于设备的元素地址和在请求中传递的从零开始的元素地址之间进行转换的数据。 在请求中，通过从给定类型的第一个元素零开始的元素类型进行寻址的元素。 通常特定于设备的地址不遵循此元素的寻址方案，因此换带机 miniclass 驱动程序必须转换为特定于设备的元素地址接收的从零开始的元素地址。

并不重要，只要转换地址 miniclass 驱动程序如何转换元素地址。 若要优化此过程，miniclass 驱动程序可能会存储数据，帮助在设备扩展中的翻译。 例如，在初始化时，驱动程序无法获取特定于设备的元素地址从 SCSI 元素地址分配页或非 SCSI 等效项，将它们映射到可用于重新构造的特定于设备的地址，并将存储的偏移量设备扩展中的偏移量。 然后，当换带机 miniclass 驱动程序收到包含的从零开始的元素地址的请求时，它可以使用存储在设备扩展中的偏移量为特定于设备的等效项的从零开始地址转换。 换带机 miniclass 驱动程序可以使用它将发送到系统端口驱动程序 Srb 中的这些特定于设备的地址。

 

 




