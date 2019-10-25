---
title: 按数据索引提取和设置控件数据
description: 按数据索引提取和设置控件数据
ms.assetid: d26d169f-4116-4d81-94c7-63c92d22877d
keywords:
- HID 报告 WDK，设置控制数据
- 报告 WDK HID，设置控制数据
- HID 报告 WDK，提取控制数据
- 报告 WDK HID，提取控件数据
- 提取 HID 控件数据
- 数据索引 WDK HID
- 为 WDK HID 数据编制索引
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 20779e7442951eed81462b2b7239021330bca3d0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824836"
---
# <a name="extracting-and-setting-control-data-by-data-indices"></a>按数据索引提取和设置控件数据





若要使用[数据索引](data-indices.md)来提取和设置 HID 报表中的控件数据，应用程序或驱动程序可以使用以下 HID 支持例程：

[**HidP\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getdata)

[**HidP\_SetData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setdata)

这些例程对于提供 "增值" 服务的应用程序或驱动程序特别有用。 例如，为 HIDClass 设备支持的所有控件提供自定义接口。 Microsoft DirectInput 是一个示例。

通过调用这些例程，应用程序或驱动程序可以最有效地获取和设置报表中的所有值。 例如，若要按其[HID 使用](hid-usages.md)情况获取所有值数据，则必须为每个使用调用[**HidP\_GetUsageValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagevalue) 。 但是，若要按数据索引获取所有值数据，它只需要调用**HidP\_** 一次。

应用程序或驱动程序使用集合的[按钮功能数组](button-capability-arrays.md)和[值功能数组](value-capability-arrays.md)中指定的数据索引来标识 HID 用法。

 

 




