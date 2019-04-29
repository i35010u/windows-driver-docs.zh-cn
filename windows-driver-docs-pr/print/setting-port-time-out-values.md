---
title: 设置端口超时值
description: 设置端口超时值
ms.assetid: bf39670b-440d-46f9-9110-790d36eb3b49
keywords:
- 端口管理 WDK 打印，超时值
- 超时 WDK 打印
- OpenPort
- SetPortTimeOuts
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22c4dfcd6fd4ad424b61c57f2f92b9c42f339c45
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372065"
---
# <a name="setting-port-time-out-values"></a>设置端口超时值





如果你正在编写具有可修改的超时值为端口是端口监视器，应在监视器的初始化从超时值[ **OpenPort** ](https://msdn.microsoft.com/library/windows/hardware/ff559593)函数。 例如**OpenPort** Localmon.dll 中的函数[示例端口监视器](sample-port-monitor.md)，调用**SetCommTimeouts**函数，在 Microsoft Windows SDK 中所述为此目的的文档。

此外，可以选择提供端口监视器[ **SetPortTimeOuts** ](https://msdn.microsoft.com/library/windows/hardware/ff562630)函数，可由语言监视器。 Pjlmon.dll，调用该函数[示例语言监视器](sample-language-monitor.md)。 打印后台处理程序不会调用**SetPortTimeOuts**。

 

 




