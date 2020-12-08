---
title: 设置端口超时值
description: 设置端口超时值
keywords:
- 端口管理 WDK 打印，超时值
- 超时 WDK 打印
- OpenPort
- SetPortTimeOuts
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 209e30f5742693decb6429c6a933d48f13c9e300
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806915"
---
# <a name="setting-port-time-out-values"></a>设置端口超时值





如果要为具有可修改超时值的端口编写端口监视器，应从监视器的 [**OpenPort**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-openport) 函数中初始化超时值。 例如，Localmon.dll 中的 **OpenPort** 函数， [示例端口监视器](sample-port-monitor.md)调用 Microsoft Windows SDK 文档中所述的 **SetCommTimeouts** 函数来实现此目的。

此外，端口监视器可以选择提供 [**SetPortTimeOuts**](/previous-versions/ff562630(v=vs.85)) 函数，该函数可以由语言监视器调用。 此函数由 [示例语言监视器](sample-language-monitor.md)Pjlmon.dll 调用。 打印后台处理程序不会调用 **SetPortTimeOuts**。

 

