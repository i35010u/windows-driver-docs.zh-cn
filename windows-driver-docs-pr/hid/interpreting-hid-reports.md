---
title: 解释 HID 报告
description: 解释 HID 报告
keywords:
- HID 报告 WDK，解释
- 报告 WDK HID，解释
ms.date: 09/10/2020
ms.localizationpriority: medium
ms.openlocfilehash: 64fd682a5a49ea8eedf113bcd4fe5cd87e99ea19
ms.sourcegitcommit: e47bd7eef2c2b89e3417d7f2dceb7c03d894f3c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "97091226"
---
# <a name="interpreting-hid-reports"></a>解释 HID 报告

本部分介绍用户模式的应用程序和内核模式驱动程序如何使用 **HidP \_ * Xxx** *  [HIDClass 支持例程](/windows-hardware/drivers/ddi/_hid)来解释 HID 报表中的控件数据。

## <a name="extracting-value-data-by-specifying-its-usage"></a>通过指定值数据的使用情况来提取该值

若要从 HID 报表中提取值数据，应用程序或驱动程序可以使用以下 HID 支持例程之一：

- [HidP_GetScaledUsageValue](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getscaledusagevalue) 返回已签名且缩放的值。

- [HidP_GetUsageValue](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagevalue) 返回一个无符号格式的 nonscaled 值或超出其正常范围的缩放值。

- [HidP_GetUsageValueArray](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagevaluearray) 返回使用情况值数组。

若要使用 **HidP_GetUsageValueArray** 应用程序和驱动程序必须分配一个初始化为零的缓冲区，该缓冲区的大小足以容纳用量值数组。 必需的大小（以字节为单位）是使用量值数组的 [HIDP_VALUE_CAPS](/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_value_caps)结构的 **BitSize** 和 **ReportCount** 成员的积，向上舍入到最接近的字节。

## <a name="extracting-button-usages-that-are-set-to-on"></a>正在提取设置为 ON 的按钮用法

若要在 (1) 上提取设置为的按钮的 HID 用法，应用程序和驱动程序调用以下 HID 支持例程之一：

- [HidP_GetButtons](./hdpi-h-macros.md) (或 [HidP_GetUsages](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusages)) 返回指定使用情况页上设置为 on 的所有按钮的使用 ID。

- [HidP_GetButtonsEx](./hdpi-h-macros.md#hidp_getbuttonsex) (或 [HidP_GetUsagesEx](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagesex)) 返回设置为 ON 的所有按钮的 "使用情况" 页和使用 ID。

这些例程返回当前设置为 ON 的所有按钮的所有使用情况信息的数组。 这些例程未返回其使用情况的按钮将被设置为 OFF (零) 。

若要调用这些例程，应用程序和驱动程序必须先分配，并将用于返回按钮用法数组的缓冲区初始化为零。 应用程序或驱动程序调用 [HidP_MaxUsageListLength](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_maxusagelistlength) 来确定报表的指定使用情况页中的按钮使用次数。 如果应用程序或驱动程序指定了 "使用情况" 页，则例程将返回报表中所有按钮用法的数目。

所需的缓冲区大小（以字节为单位）如下所示：

- 用于 [HidP_GetButtons](./hdpi-h-macros.md) 的 () **HidP_MaxUsageListLength** 次返回的值 sizeof (使用情况) 

- 用于 [HidP_GetButtonsEx](./hdpi-h-macros.md#hidp_getbuttonsex) 的 () **HidP_MaxUsageListLength** 次返回的值 sizeof (USAGE_AND_PAGE) 

在应用程序或驱动程序已使用这些例程获取有关哪些按钮当前设置为 ON 的信息后，它可以通过调用以下 [HIDClass 支持例程](/windows-hardware/drivers/ddi/_hid/#hidclass-support-routines)之一来确定按钮的当前状态和之前状态之间的差异。 这些例程返回使用情况信息的两个数组之间的差异：

- [HidP_UsageListDifference](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_usagelistdifference)

- [HidP_UsageAndPageListDifference](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_usageandpagelistdifference)

## <a name="extracting-and-setting-control-data-by-data-indices"></a>按数据索引提取和设置控件数据

若要使用数据索引来提取和设置 HID 报表中的控件数据，应用程序或驱动程序可以使用以下 [HIDClass 支持例程](/windows-hardware/drivers/ddi/_hid/#hidclass-support-routines)：

- [HidP_GetData](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getdata)

- [HidP_SetData](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setdata)

这些例程对于提供 "增值" 服务的应用程序或驱动程序特别有用。 例如，为 HIDClass 设备支持的所有控件提供自定义接口。 Microsoft DirectInput 是一个示例。

通过调用这些例程，应用程序或驱动程序可以最有效地获取和设置报表中的所有值。 例如，若要按其 [HID 使用](./hid-usages.md) 情况获取所有值数据，则必须对每个使用情况调用 [HidP_GetUsageValue](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagevalue) 。 但是，若要按数据索引获取所有值数据，它只需要调用一次 **HidP_GetData** 。

应用程序或驱动程序使用集合的 [按钮功能数组](./button-capability-arrays.md) 和 [值功能数组](./value-capability-arrays.md) 中指定的数据索引来标识 HID 用法。

## <a name="setting-value-data-by-specifying-its-usage"></a>通过指定值数据的使用情况来设置该值

应用程序或驱动程序可以通过调用以下一个 HID 支持例程来设置正确初始化的 HID 报表中的值：

- [HidP_SetScaledUsageValue](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setscaledusagevalue) 在报表中设置经过签名和缩放的值。

- [HidP_SetUsageValue](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusagevalue) 在报表中设置一个值。

- [HidP_SetUsageValueArray](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusagevaluearray) 在报表中设置使用值数组。

## <a name="setting-button-state-by-specifying-its-usage"></a>通过指定其用法来设置按钮状态

应用程序或驱动程序可以通过调用以下 [HIDClass 支持例程](/windows-hardware/drivers/ddi/_hid/#hidclass-support-routines)之一来设置正确初始化的 HID 报表中的按钮状态：

- [HidP_SetButtons](./hdpi-h-macros.md#hidp_setbuttons) (或 [HidP_SetUsages](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusages)) 在 (1) 上将一组指定的按钮设置为。

- [HidP_UnsetButtons](./hdpi-h-macros.md#hidp_unsetbuttons) (或 [HidP_UnsetUsages](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_unsetusages)) 会将指定的一组按钮设置为 "关闭" (零) 。

## <a name="extracting-and-setting-hid-control-data-by-data-indices"></a>按数据索引提取和设置 HID 控件数据

若要使用数据索引来提取和设置 HID 报表中的控件数据，应用程序或驱动程序可以使用以下 [HIDClass 支持例程](/windows-hardware/drivers/ddi/_hid/#hidclass-support-routines)：

- [HidP_GetData](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getdata)

- [HidP_SetData](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setdata)

这些例程对于提供 "增值" 服务的应用程序或驱动程序特别有用。 例如，为 HIDClass 设备支持的所有控件提供自定义接口。 Microsoft DirectInput 是一个示例。

通过调用这些例程，应用程序或驱动程序可以最有效地获取和设置报表中的所有值。 例如，若要按其 HID 使用情况获取所有值数据，则必须对每个使用情况调用 [HidP_GetUsageValue](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagevalue) 。 但是，若要按数据索引获取所有值数据，它只需要调用一次 **HidP_GetData** 。

应用程序或驱动程序使用集合的 [按钮功能数组](./button-capability-arrays.md) 和 [值功能数组](./value-capability-arrays.md) 中指定的数据索引来标识 HID 用法。

## <a name="see-also"></a>另请参阅

[初始化 HID 报告](initializing-hid-reports.md)
