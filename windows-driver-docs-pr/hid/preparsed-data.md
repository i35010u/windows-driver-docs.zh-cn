---
title: 预分析的数据
description: 预分析的数据
ms.assetid: 50ac2877-4c45-4d55-b5cc-013486892fbf
keywords:
- 分析的数据 WDK HID
- preparsed 数据 WDK HID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7684cd229b9edc5b49a901c5ad0b9fb74bdf643d
ms.sourcegitcommit: 9145bffd4cc3b990a9ebff43b588db6ef2001f5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/09/2020
ms.locfileid: "89592387"
---
# <a name="preparsed-data"></a>预分析的数据





*Preparsed 数据* 是与 [顶级集合](top-level-collections.md)关联的报表描述符数据。 用户模式应用程序或内核模式驱动程序使用 preparsed 数据提取有关特定 HID 控件的信息，而无需获取和解释设备的整个报表描述符。 用户模式应用程序使用 [**HidD \_ GetPreparsedData**](/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_getpreparseddata) 获取集合的 preparsed 数据，并且内核模式驱动程序使用 [**IOCTL \_ HID \_ 获取 \_ 集合 \_ 描述符**](/windows-hardware/drivers/ddi/hidclass/ni-hidclass-ioctl_hid_get_collection_descriptor) 请求。

以下 [HIDClass 支持例程](/windows-hardware/drivers/ddi/index) 支持提取和设置按钮和值数据：

[**HidP \_ GetButtons**](./hdpi-h-macros.md)

[**HidP \_ SetButtons**](./hdpi-h-macros.md)

[**HidP \_ UnsetButtons**](./hdpi-h-macros.md)

[**HidP \_ GetUsageValue**](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagevalue)

[**HidP \_ SetUsageValue**](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusagevalue)

[**HidP \_ GetScaledUsageValue**](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getscaledusagevalue)

[**HidP \_ SetScaledUsageValue**](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setscaledusagevalue)

[**HidP \_ GetUsageValueArray**](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagevaluearray)

[**HidP \_ SetUsageValueArray**](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusagevaluearray)

 

