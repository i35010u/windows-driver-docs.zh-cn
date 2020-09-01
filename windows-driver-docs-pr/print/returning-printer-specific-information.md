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
ms.openlocfilehash: 1c056c08703d9bdd50edbc6e3c1b94db86c03672
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213643"
---
# <a name="returning-printer-specific-information"></a>返回打印机特定的信息





GDI 有时会请求打印机图形 DLL 在打印作业之间返回特定于打印机的信息，方法是调用这样的 **DrvQuery**前缀的图形 DDI 函数作为 [**DrvQueryAdvanceWidths**](/windows/win32/api/winddi/nf-winddi-drvqueryadvancewidths) (（如果图形 DLL) 定义）。

这种情况的一个示例是在处理应用程序时，该应用程序维护可打印页面的 WYSIWYG 屏幕显示。 若要在文本中正确地显示分行符，字处理器必须基于选定打印机的字体实现中的字符宽度和其他字体规格来基准线拟合计算。

 

