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
ms.openlocfilehash: 4b885a93bf185c18c9e00691b1c4e34ca5f836f4
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802359"
---
# <a name="supporting-device-fonts"></a>支持设备字体





如果打印机提供设备字体，则打印机图形 DLL 必须定义 [**DrvTextOut**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvtextout) 函数以生成文本输出命令。 图形 DLL 还必须定义以下函数：

[**DrvQueryAdvanceWidths**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvqueryadvancewidths) 
[**DrvQueryFont**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvqueryfont) 
[**DrvQueryFontData**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvqueryfontdata) 
[**DrvQueryFontTree**](https://docs.microsoft.com/windows/win32/api/winddi/nf-winddi-drvqueryfonttree)有关支持设备字体的详细信息，请参阅[支持图形 DDI 字体和文本函数](https://docs.microsoft.com/windows-hardware/drivers/display/supporting-graphics-ddi-font-and-text-functions)。

 

 




