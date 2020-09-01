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
ms.openlocfilehash: a1b49d4ed7b244a2af388416097eb5b0d1ef87e4
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216338"
---
# <a name="setting-port-time-out-values"></a>设置端口超时值





如果要为具有可修改超时值的端口编写端口监视器，应从监视器的 [**OpenPort**](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-openport) 函数中初始化超时值。 例如，Localmon.dll 中的 **OpenPort** 函数， [示例端口监视器](sample-port-monitor.md)调用 Microsoft Windows SDK 文档中所述的 **SetCommTimeouts** 函数来实现此目的。

此外，端口监视器可以选择提供 [**SetPortTimeOuts**](/previous-versions/ff562630(v=vs.85)) 函数，该函数可以由语言监视器调用。 此函数由 [示例语言监视器](sample-language-monitor.md)Pjlmon.dll 调用。 打印后台处理程序不会调用 **SetPortTimeOuts**。

 

