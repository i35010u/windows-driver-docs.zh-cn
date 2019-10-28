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
ms.openlocfilehash: b5479f5418904d41c102d3c5bf73fd9c1c756bd2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840409"
---
# <a name="setting-port-time-out-values"></a>设置端口超时值





如果要为具有可修改超时值的端口编写端口监视器，应从监视器的[**OpenPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-openport)函数中初始化超时值。 例如， **OpenPort**函数在 Localmon 中，[示例端口监视器](sample-port-monitor.md)调用 Microsoft Windows SDK 文档中所述的**SetCommTimeouts**函数以实现此目的。

此外，端口监视器可以选择提供[**SetPortTimeOuts**](https://docs.microsoft.com/previous-versions/ff562630(v=vs.85))函数，该函数可以由语言监视器调用。 函数由 Pjlmon （[示例语言监视器](sample-language-monitor.md)）调用。 打印后台处理程序不会调用**SetPortTimeOuts**。

 

 




