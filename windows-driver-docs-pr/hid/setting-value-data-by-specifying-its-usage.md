---
title: 通过指定值数据的使用情况来设置该值
description: 通过指定值数据的使用情况来设置该值
ms.assetid: 69dc3bb4-8999-4990-950c-8581328030eb
keywords:
- HID 报告 WDK，设置控制数据
- 报告 WDK HID，设置控制数据
- 数据使用设置 WDK HID
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 546c498bf182f8c0daa53d8d407355ce1cbc5a01
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841553"
---
# <a name="setting-value-data-by-specifying-its-usage"></a>通过指定值数据的使用情况来设置该值





应用程序或驱动程序可以通过调用以下一个 HID 支持例程来设置正确初始化的 HID 报表中的值：

<a href="" id="hidp-setscaledusagevalue"></a>[**HidP\_SetScaledUsageValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setscaledusagevalue)  
在报表中设置经过签名和缩放的值。

<a href="" id="hidp-setusagevalue"></a>[**HidP\_SetUsageValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusagevalue)  
在报表中设置一个值。

<a href="" id="hidp-setusagevaluearray"></a>[**HidP\_SetUsageValueArray**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusagevaluearray)  
在报表中设置使用值数组。

<a href="" id="see-also-initializing-hid-reports-"></a>另请参阅[初始化 HID 报表](initializing-hid-reports.md)。  

 

 




