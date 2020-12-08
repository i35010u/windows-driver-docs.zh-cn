---
title: 返回打印机特定的信息
description: 返回打印机特定的信息
keywords:
- 打印机图形 DLL WDK，返回打印机特定的信息
- 图形 DLL WDK 打印机，返回打印机特定的信息
- 返回特定于打印机的信息 WDK 打印机图形
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6d3977acda4d9b998dd306213834f5c2a30f027
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807015"
---
# <a name="returning-printer-specific-information"></a>返回打印机特定的信息





GDI 有时会请求打印机图形 DLL 在打印作业之间返回特定于打印机的信息，方法是调用这样的 **DrvQuery** 前缀的图形 DDI 函数作为 [**DrvQueryAdvanceWidths**](/windows/win32/api/winddi/nf-winddi-drvqueryadvancewidths) (（如果图形 DLL) 定义）。

这种情况的一个示例是在处理应用程序时，该应用程序维护可打印页面的 WYSIWYG 屏幕显示。 若要在文本中正确地显示分行符，字处理器必须基于选定打印机的字体实现中的字符宽度和其他字体规格来基准线拟合计算。

 

