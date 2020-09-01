---
title: 支持设备字体
description: 支持设备字体
ms.assetid: 9ca3269d-3f87-4d8a-a897-7305ac172227
keywords:
- 打印机图形 DLL WDK，设备字体
- 图形 DLL WDK 打印机，设备字体
- 设备字体 WDK 打印机图形
- 字体 WDK 打印机图形
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1c2e75ec49e41c5f27b1e3de8cff72d71c4bf25
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217953"
---
# <a name="supporting-device-fonts"></a>支持设备字体





如果打印机提供设备字体，则打印机图形 DLL 必须定义 [**DrvTextOut**](/windows/win32/api/winddi/nf-winddi-drvtextout) 函数以生成文本输出命令。 图形 DLL 还必须定义以下函数：

[**DrvQueryAdvanceWidths**](/windows/win32/api/winddi/nf-winddi-drvqueryadvancewidths) 
[**DrvQueryFont**](/windows/win32/api/winddi/nf-winddi-drvqueryfont) 
[**DrvQueryFontData**](/windows/win32/api/winddi/nf-winddi-drvqueryfontdata) 
[**DrvQueryFontTree**](/windows/win32/api/winddi/nf-winddi-drvqueryfonttree)有关支持设备字体的详细信息，请参阅[支持图形 DDI 字体和文本函数](../display/supporting-graphics-ddi-font-and-text-functions.md)。

 

