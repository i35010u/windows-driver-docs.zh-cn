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
ms.openlocfilehash: 9ed759ad3b03575026bff05c1889c680511bf666
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534002"
---
# <a name="setting-button-state-by-specifying-its-usage"></a>通过指定其使用情况设置按钮状态





应用程序或驱动程序可以设置按钮的状态正确初始化 HID 报表中通过调用以下 HID 支持例程之一：

<a href="" id="hidp-setbuttons--or-hidp-setusages-"></a>[**HidP\_SetButtons** ](https://msdn.microsoft.com/library/windows/hardware/ff539779) (或[ **HidP\_SetUsages**](https://msdn.microsoft.com/library/windows/hardware/ff539792))  
(1) 上设置一组指定的按钮。

<a href="" id="hidp-unsetbuttons--or-hidp-unsetusages-"></a>[**HidP\_UnsetButtons** ](https://msdn.microsoft.com/library/windows/hardware/ff539812) (或[ **HidP\_UnsetUsages**](https://msdn.microsoft.com/library/windows/hardware/ff539819))  
将一组指定的按钮设置为 OFF （零）。

<a href="" id="see-also-initializing-hid-reports-"></a>另请参阅[初始化 HID 报表](initializing-hid-reports.md)。  

 

 




