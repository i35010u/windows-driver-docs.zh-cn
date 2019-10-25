---
title: 通过指定其用法来设置按钮状态
description: 通过指定其用法来设置按钮状态
ms.assetid: 0806f274-2b29-44f5-b487-4c0acb7a3e42
keywords:
- HID 报告 WDK，设置控制数据
- 报告 WDK HID，设置控制数据
- 按钮用法 WDK HID
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f289a214e5e09d1e8bf4e8986e1ae29c7b5d844b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841554"
---
# <a name="setting-button-state-by-specifying-its-usage"></a>通过指定其用法来设置按钮状态





应用程序或驱动程序可以通过调用以下一个 HID 支持例程来设置正确初始化的 HID 报表中的按钮状态：

<a href="" id="hidp-setbuttons--or-hidp-setusages-"></a>[**HidP\_SetButtons**](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros) （或[**HidP\_SetUsages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_setusages)）  
将一组指定的按钮设置为 ON （1）。

<a href="" id="hidp-unsetbuttons--or-hidp-unsetusages-"></a>[**HidP\_UnsetButtons**](https://docs.microsoft.com/windows-hardware/drivers/hid/hdpi-h-macros) （或[**HidP\_UnsetUsages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_unsetusages)）  
将一组指定的按钮设置为 OFF （零）。

<a href="" id="see-also-initializing-hid-reports-"></a>另请参阅[初始化 HID 报表](initializing-hid-reports.md)。  

 

 




