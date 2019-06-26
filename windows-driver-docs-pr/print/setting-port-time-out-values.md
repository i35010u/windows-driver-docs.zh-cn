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
ms.openlocfilehash: 02b507030b09bbf26a531b439dcae6d1a277ad7a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384168"
---
# <a name="setting-port-time-out-values"></a>设置端口超时值





如果你正在编写具有可修改的超时值为端口是端口监视器，应在监视器的初始化从超时值[ **OpenPort** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-openport)函数。 例如**OpenPort** Localmon.dll 中的函数[示例端口监视器](sample-port-monitor.md)，调用**SetCommTimeouts**函数，在 Microsoft Windows SDK 中所述为此目的的文档。

此外，可以选择提供端口监视器[ **SetPortTimeOuts** ](https://docs.microsoft.com/previous-versions/ff562630(v=vs.85))函数，可由语言监视器。 Pjlmon.dll，调用该函数[示例语言监视器](sample-language-monitor.md)。 打印后台处理程序不会调用**SetPortTimeOuts**。

 

 




