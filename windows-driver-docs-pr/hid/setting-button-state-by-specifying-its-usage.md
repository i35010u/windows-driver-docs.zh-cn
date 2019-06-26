---
title: 通过指定其使用情况设置按钮状态
description: 通过指定其使用情况设置按钮状态
ms.assetid: 0806f274-2b29-44f5-b487-4c0acb7a3e42
keywords:
- HID 报告 WDK，设置控制数据
- 报告 WDK HID，设置控制数据
- WDK HID 按钮用途
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b0ebf83eec8456e0f79acae0f289f6741d91c765
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385802"
---
# <a name="setting-button-state-by-specifying-its-usage"></a>通过指定其使用情况设置按钮状态





应用程序或驱动程序可以设置按钮的状态正确初始化 HID 报表中通过调用以下 HID 支持例程之一：

<a href="" id="hidp-setbuttons--or-hidp-setusages-"></a>[**HidP\_SetButtons** ](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros) (或[ **HidP\_SetUsages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_setusages))  
(1) 上设置一组指定的按钮。

<a href="" id="hidp-unsetbuttons--or-hidp-unsetusages-"></a>[**HidP\_UnsetButtons** ](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros) (或[ **HidP\_UnsetUsages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_unsetusages))  
将一组指定的按钮设置为 OFF （零）。

<a href="" id="see-also-initializing-hid-reports-"></a>另请参阅[初始化 HID 报表](initializing-hid-reports.md)。  

 

 




