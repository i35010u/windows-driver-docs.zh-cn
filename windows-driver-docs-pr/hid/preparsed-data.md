---
title: 预分析的数据
description: 预分析的数据
ms.assetid: 50ac2877-4c45-4d55-b5cc-013486892fbf
keywords:
- WDK HID 的已分析的数据
- WDK HID preparsed 的数据
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4371d61c2cfb523993b7f7c1855780d1a5a03bc9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385819"
---
# <a name="preparsed-data"></a>预分析的数据





*Preparsed 数据*是报表描述符与关联的数据[顶级集合](top-level-collections.md)。 用户模式应用程序或内核模式驱动程序使用 preparsed 的数据而无需获取和解释设备的整个报表描述符提取特定的 HID 控件有关的信息。 在用户模式应用程序使用获取集合的 preparsed 的数据[ **HidD\_GetPreparsedData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidsdi/nf-hidsdi-hidd_getpreparseddata)和内核模式驱动程序将使用[ **IOCTL\_HID\_获取\_集合\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidclass/ni-hidclass-ioctl_hid_get_collection_descriptor)请求。

以下[HIDClass 支持例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)支持提取和设置按钮和值数据：

[**HidP\_GetButtons**](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros)

[**HidP\_SetButtons**](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros)

[**HidP\_UnsetButtons**](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros)

[**HidP\_GetUsageValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_getusagevalue)

[**HidP\_SetUsageValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_setusagevalue)

[**HidP\_GetScaledUsageValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_getscaledusagevalue)

[**HidP\_SetScaledUsageValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_setscaledusagevalue)

[**HidP\_GetUsageValueArray**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_getusagevaluearray)

[**HidP\_SetUsageValueArray**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_setusagevaluearray)

 

 




