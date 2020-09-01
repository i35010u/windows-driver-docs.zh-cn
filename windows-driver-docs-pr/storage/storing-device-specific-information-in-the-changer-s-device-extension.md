---
title: 将特定于设备的信息存储在更换器的设备扩展中
description: 将特定于设备的信息存储在更换器的设备扩展中
ms.assetid: 72048d84-1c2d-4f3c-b5e8-f55a812ad567
keywords:
- 转换器驱动程序，WDK 存储，特定于设备的数据存储
- 存储更换器驱动程序 WDK，特定于设备的数据存储
- 设备特定的数据存储 WDK 转换器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9488096c9614db4ecaf3b2454021702eca8c9a88
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188008"
---
# <a name="storing-device-specific-information-in-the-changers-device-extension"></a>将特定于设备的信息存储在更换器的设备扩展中


## <span id="ddk_storing_device_specific_information_in_the_changers_device_extensi"></span><span id="DDK_STORING_DEVICE_SPECIFIC_INFORMATION_IN_THE_CHANGERS_DEVICE_EXTENSI"></span>


转换器 miniclass 驱动程序在其 [**ChangerAdditionalExtensionSize**](/windows-hardware/drivers/ddi/mcd/nf-mcd-changeradditionalextensionsize) 例程中指定设备特定数据所需的存储。 变换器类驱动程序代表转换器 miniclass 驱动程序分配请求的存储，然后调用 miniclass 驱动程序的 [**ChangerInitialize**](/windows-hardware/drivers/ddi/mcd/nf-mcd-changerinitialize) 例程。

转换器 miniclass 驱动程序是否将数据存储在设备扩展中和存储的数据，取决于驱动程序设计器。 它通常包括 SCSI 查询数据或变换器设备的非 SCSI 等效项。

设备扩展还可能包含 miniclass 驱动程序用来在特定于设备的元素地址与传入请求的从零开始的元素地址之间进行转换的数据。 在请求中，元素由元素类型寻址，从零开始，对于给定类型的第一个元素。 设备特定的地址通常不遵循此元素寻址方案，因此，转换器 miniclass 驱动程序必须将其接收的从零开始的元素地址转换为特定于设备的元素地址。

只要转换地址，miniclass 驱动程序就会转换元素地址并不重要。 为了优化该过程，miniclass 驱动程序可能会存储便于在设备扩展中进行转换的数据。 例如，在初始化时，驱动程序可以从 SCSI 元素地址分配页或非 SCSI 等效项获取特定于设备的元素地址，将它们映射到可用于重新构造特定于设备的地址的偏移量，并在设备扩展中存储偏移量。 然后，当转换器 miniclass driver 收到包含从零开始的元素地址的请求时，它可以使用存储在设备扩展中的偏移量将从零开始的地址转换为特定于设备的等效地址。 转换器 miniclass 驱动程序可以使用其发送到系统端口驱动程序的 SRBs 中的这些特定于设备的地址。

 

