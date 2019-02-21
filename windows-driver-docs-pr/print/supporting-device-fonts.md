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
ms.openlocfilehash: 11c07cfd3b1f1ace4b9d728e014a6ff182fc4783
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525983"
---
# <a name="supporting-device-fonts"></a>支持设备字体





如果打印机提供了设备字体，打印机图形 DLL 必须定义[ **DrvTextOut** ](https://msdn.microsoft.com/library/windows/hardware/ff557277)函数来生成文本输出的命令。 图形 DLL 还必须定义以下函数：

[**DrvQueryAdvanceWidths**](https://msdn.microsoft.com/library/windows/hardware/ff556259)
[**DrvQueryFont**](https://msdn.microsoft.com/library/windows/hardware/ff556262)
[**DrvQueryFontData**](https://msdn.microsoft.com/library/windows/hardware/ff556264) 
 [ **DrvQueryFontTree** ](https://msdn.microsoft.com/library/windows/hardware/ff556266)支持设备字体的详细信息，请参阅[支持图形 DDI 字体和文本函数](https://msdn.microsoft.com/library/windows/hardware/ff569868).

 

 




