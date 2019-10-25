---
title: 正在提取设置为 ON 的按钮用法
description: 正在提取设置为 ON 的按钮用法
ms.assetid: 700cdb18-f570-4189-a33c-f57af56a52fd
keywords:
- HID 报告 WDK，提取控制数据
- 报告 WDK HID，提取控件数据
- 提取 HID 控件数据
- 按钮用法 WDK HID
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 206c3a9d97ff8ece84d60b90c939a1fbea66f1fe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824822"
---
# <a name="extracting-button-usages-that-are-set-to-on"></a>正在提取设置为 ON 的按钮用法





若要提取设置为 ON （1）的按钮的[HID 用法](hid-usages.md)，应用程序和驱动程序调用以下 HID 支持例程之一：

<a href="" id="hidp-getbuttons--or-hidp-getusages-"></a>[**HidP\_GetButtons**](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros) （或[**HidP\_GetUsages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusages)）  
返回在指定的 "使用情况" 页上设置为 "开" 的所有按钮的使用 ID。

<a href="" id="hidp-getbuttonsex--or-hidp-getusagesex-"></a>[**HidP\_GetButtonsEx**](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros) （或[**HidP\_GetUsagesEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagesex)）  
返回设置为 ON 的所有按钮的使用页面和使用 ID。

这些例程返回当前设置为 ON 的所有按钮的所有使用情况信息的数组。 隐式，其使用情况不会被这些例程返回的按钮将设置为 OFF （零）。

若要调用这些例程，应用程序和驱动程序必须先分配，并将用于返回按钮用法数组的缓冲区初始化为零。 应用程序或驱动程序调用[**HidP\_MaxUsageListLength**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_maxusagelistlength) ，以确定报表的指定使用情况页中的按钮使用数。 如果应用程序或驱动程序指定了 "使用情况" 页，则例程将返回报表中所有按钮用法的数目。

所需的缓冲区大小（以字节为单位）如下所示：

-   （适用于[**HidP\_GetButtons**](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros)）HidP 返回的值 **\_MaxUsageListLength**的 sizeof 时间（使用情况）

-   （适用于[**HidP\_GetButtonsEx**](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros)）**HidP\_MaxUsageListLength**时间 sizeof 返回的值（"使用情况"\_和 "\_" 页）

在应用程序或驱动程序已使用这些例程获取有关当前设置为 ON 的按钮的信息后，它可以通过调用以下 HIDClass 之一来确定按钮的当前状态和之前状态之间的差异[支持例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。 这些例程返回使用情况信息的两个数组之间的差异：

[**HidP\_UsageListDifference**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_usagelistdifference)

[**HidP\_UsageAndPageListDifference**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff539824(v=vs.85))

 

 




