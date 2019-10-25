---
title: 预分析的数据
description: 预分析的数据
ms.assetid: 50ac2877-4c45-4d55-b5cc-013486892fbf
keywords:
- 分析的数据 WDK HID
- preparsed 数据 WDK HID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b578e7c443fc7b1c73f6369ff73c75f7e5a08868
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841563"
---
# <a name="preparsed-data"></a>预分析的数据





*Preparsed 数据*是与[顶级集合](top-level-collections.md)关联的报表描述符数据。 用户模式应用程序或内核模式驱动程序使用 preparsed 数据提取有关特定 HID 控件的信息，而无需获取和解释设备的整个报表描述符。 用户模式应用程序使用[**HidD\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getpreparseddata)获取集合的 preparsed 数据，并且内核模式驱动程序使用[**IOCTL\_HID\_获取\_集合\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidclass/ni-hidclass-ioctl_hid_get_collection_descriptor)请求。

以下[HIDClass 支持例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)支持提取和设置按钮和值数据：

[**HidP\_GetButtons**](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros)

[**HidP\_SetButtons**](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros)

[**HidP\_UnsetButtons**](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros)

[**HidP\_GetUsageValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagevalue)

[**HidP\_SetUsageValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusagevalue)

[**HidP\_GetScaledUsageValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getscaledusagevalue)

[**HidP\_SetScaledUsageValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setscaledusagevalue)

[**HidP\_GetUsageValueArray**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagevaluearray)

[**HidP\_SetUsageValueArray**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusagevaluearray)

 

 




