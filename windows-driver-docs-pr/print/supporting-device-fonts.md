---
title: 支持设备字体
description: 支持设备字体
keywords:
- 打印机图形 DLL WDK，设备字体
- 图形 DLL WDK 打印机，设备字体
- 设备字体 WDK 打印机图形
- 字体 WDK 打印机图形
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 785b18fd12f89e69830836211362de55adaf80ed
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806809"
---
# <a name="supporting-device-fonts"></a>支持设备字体





如果打印机提供设备字体，则打印机图形 DLL 必须定义 [**DrvTextOut**](/windows/win32/api/winddi/nf-winddi-drvtextout) 函数以生成文本输出命令。 图形 DLL 还必须定义以下函数：

[**DrvQueryAdvanceWidths**](/windows/win32/api/winddi/nf-winddi-drvqueryadvancewidths) 
[**DrvQueryFont**](/windows/win32/api/winddi/nf-winddi-drvqueryfont) 
[**DrvQueryFontData**](/windows/win32/api/winddi/nf-winddi-drvqueryfontdata) 
[**DrvQueryFontTree**](/windows/win32/api/winddi/nf-winddi-drvqueryfonttree)有关支持设备字体的详细信息，请参阅 [支持图形 DDI 字体和文本函数](../display/supporting-graphics-ddi-font-and-text-functions.md)。

 

