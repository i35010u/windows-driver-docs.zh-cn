---
title: 提取设置为 ON 的按钮用途
description: 提取设置为 ON 的按钮用途
ms.assetid: 700cdb18-f570-4189-a33c-f57af56a52fd
keywords:
- HID 的报表 WDK，提取控件数据
- WDK HID，提取控件数据的报表
- HID 控制如何将数据提取
- WDK HID 按钮用途
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ceeef56537de70071f89f3481cca1bf2691c21d5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375727"
---
# <a name="extracting-button-usages-that-are-set-to-on"></a>提取设置为 ON 的按钮用途





若要提取[HID 用法](hid-usages.md)设置为 ON (1) 的按钮，应用程序和驱动程序调用一个以下 HID 支持例程：

<a href="" id="hidp-getbuttons--or-hidp-getusages-"></a>[**HidP\_GetButtons** ](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros) (或[ **HidP\_GetUsages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_getusages))  
返回设置为 ON 指定的用法页上的所有按钮的使用情况 ID。

<a href="" id="hidp-getbuttonsex--or-hidp-getusagesex-"></a>[**HidP\_GetButtonsEx** ](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros) (或[ **HidP\_GetUsagesEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_getusagesex))  
返回的使用情况页面和使用情况设置为 ON 的所有按钮的 ID。

这些例程返回的当前设置为 ON 的所有按钮的所有使用情况信息的数组。 隐式，这些例程不返回对其使用的按钮都设置为 OFF （零）。

若要调用这些例程，应用程序和驱动程序必须首先分配并零初始化返回按钮用途的数组所使用的缓冲区。 应用程序或驱动程序调用[ **HidP\_MaxUsageListLength** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_maxusagelistlength)来确定按钮在报表中指定的使用情况页面中的使用情况的数目。 如果应用程序或驱动程序指定零使用情况页上，例程将返回在报表中的所有按钮使用实例数。

所需的缓冲区大小，以字节为单位，则可如下：

-   (有关[ **HidP\_GetButtons**](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros)) 返回的值**HidP\_MaxUsageListLength**时间 sizeof(USAGE)

-   (有关[ **HidP\_GetButtonsEx**](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros)) 返回的值**HidP\_MaxUsageListLength**时间 sizeof (使用情况\_与\_页）

它的应用程序或驱动程序具有使用这些例程来获取有关该按钮当前设置为 ON 的信息后，可以通过调用以下方法之一来确定的当前状态和按钮的前一状态之间的差异[HIDClass 支持例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。 这些例程将返回的使用情况信息的两个数组之间的差异：

[**HidP\_UsageListDifference**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_usagelistdifference)

[**HidP\_UsageAndPageListDifference**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff539824(v=vs.85))

 

 




