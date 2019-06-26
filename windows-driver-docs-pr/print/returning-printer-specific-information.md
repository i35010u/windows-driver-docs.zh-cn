---
title: 返回打印机特定的信息
description: 返回打印机特定的信息
ms.assetid: 7a47b395-4b01-437f-bed7-967b31b5841e
keywords:
- 打印机图形 DLL WDK 返回特定于打印机的信息
- 图形 DLL WDK 打印机，返回特定于打印机的信息
- 返回特定于打印机的信息 WDK 打印机图形
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d9e4a8e59c8f1c23eea893ceb157f05dac03ef1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384177"
---
# <a name="returning-printer-specific-information"></a>返回打印机特定的信息





GDI 有时请求打印机图形 DLL 之间返回特定于打印机的信息打印作业，通过调用此类**DrvQuery**-前缀作为图形 DDI 函数[ **DrvQueryAdvanceWidths** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvqueryadvancewidths) （如果已定义的图形 DLL）。

这可能会发生时的一个示例是维护可打印页的所见即所得的屏幕显示的文字处理应用程序的大小写。 若要正确显示文本中的分行符，字处理器必须基准线调整的字符宽度和从所选的打印机的字体实现其他字体指标计算。

 

 




