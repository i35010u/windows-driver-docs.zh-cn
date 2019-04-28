---
title: 保存缺陷跟踪
description: 将缺陷跟踪保存在的 Static Driver Verifier
ms.assetid: 6d54a532-75ff-4226-86a7-cdc2046b0b5b
keywords:
- Static Driver Verifier WDK、 Static Driver Verifier 报表
- StaticDV WDK、 Static Driver Verifier 报表
- SDV WDK、 Static Driver Verifier 报表
- 静态驱动程序验证程序 WDK，查找错误
- StaticDV WDK，查找错误
- SDV WDK，查找错误
- 查找错误 WDK Static Driver Verifier
- 错误 WDK Static Driver Verifier
- 导出 WDK Static Driver Verifier
- Static Driver Verifier 报表 WDK
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a78b986f520a84f92fc3ba40ea8d38d61112e61e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340256"
---
# <a name="saving-defect-traces"></a>保存缺陷跟踪

静态驱动程序验证程序脱离查看器具有功能，可将特定缺陷跟踪保存格式可轻松地共享。  

若要保存跟踪，请选择"另存为..."从文件菜单或按 Ctrl-s。  

![缺陷查看器窗口，显示的保存位置的屏幕截图功能](images/sdv-savedefecttrace.png)

然后指定将放置跟踪文件夹 ("sdvdefect") 的文件夹。

已保存的缺陷跟踪将包含相关的源代码、 缺陷跟踪和必要的 SDV 文件和查看跟踪的可执行文件的副本。  若要查看跟踪，只需双击 sdvdefect.exe 文件。

