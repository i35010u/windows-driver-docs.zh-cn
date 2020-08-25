---
title: 返回打印机特定的信息
description: 返回打印机特定的信息
ms.assetid: 7a47b395-4b01-437f-bed7-967b31b5841e
keywords:
- 打印机图形 DLL WDK，返回打印机特定的信息
- 图形 DLL WDK 打印机，返回打印机特定的信息
- 返回特定于打印机的信息 WDK 打印机图形
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f0541956707985c14644d333993e00d50bf6e6f
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802340"
---
# <a name="returning-printer-specific-information"></a>返回打印机特定的信息





GDI 有时会请求打印机图形 DLL 在打印作业之间返回特定于打印机的信息，方法是调用这样的 **DrvQuery**前缀的图形 DDI 函数作为 [**DrvQueryAdvanceWidths**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvqueryadvancewidths) (（如果图形 DLL) 定义）。

这种情况的一个示例是在处理应用程序时，该应用程序维护可打印页面的 WYSIWYG 屏幕显示。 若要在文本中正确地显示分行符，字处理器必须基于选定打印机的字体实现中的字符宽度和其他字体规格来基准线拟合计算。

 

 




