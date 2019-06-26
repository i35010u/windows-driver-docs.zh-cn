---
title: 通过指定其使用情况设置值数据
description: 通过指定其使用情况设置值数据
ms.assetid: 69dc3bb4-8999-4990-950c-8581328030eb
keywords:
- HID 报告 WDK，设置控制数据
- 报告 WDK HID，设置控制数据
- WDK HID 数据使用情况设置
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9276ed90640f62e90606513d468c116f8c25c92c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385798"
---
# <a name="setting-value-data-by-specifying-its-usage"></a>通过指定其使用情况设置值数据





应用程序或驱动程序可以设置一个值正确初始化 HID 报表中通过调用以下 HID 支持例程之一：

<a href="" id="hidp-setscaledusagevalue"></a>[**HidP\_SetScaledUsageValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_setscaledusagevalue)  
在报表中设置的签名和缩放值。

<a href="" id="hidp-setusagevalue"></a>[**HidP\_SetUsageValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_setusagevalue)  
在报表中设置一个值。

<a href="" id="hidp-setusagevaluearray"></a>[**HidP\_SetUsageValueArray**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_setusagevaluearray)  
设置在报表中使用值数组。

<a href="" id="see-also-initializing-hid-reports-"></a>另请参阅[初始化 HID 报表](initializing-hid-reports.md)。  

 

 




