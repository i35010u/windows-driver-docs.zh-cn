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
ms.openlocfilehash: 2430cd8a55c3121140bec15d20accc253552200f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354461"
---
# <a name="supporting-device-fonts"></a>支持设备字体





如果打印机提供了设备字体，打印机图形 DLL 必须定义[ **DrvTextOut** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout)函数来生成文本输出的命令。 图形 DLL 还必须定义以下函数：

[**DrvQueryAdvanceWidths**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvqueryadvancewidths)
[**DrvQueryFont**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvqueryfont)
[**DrvQueryFontData**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvqueryfontdata) 
 [ **DrvQueryFontTree** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvqueryfonttree)支持设备字体的详细信息，请参阅[支持图形 DDI 字体和文本函数](https://docs.microsoft.com/windows-hardware/drivers/display/supporting-graphics-ddi-font-and-text-functions).

 

 




