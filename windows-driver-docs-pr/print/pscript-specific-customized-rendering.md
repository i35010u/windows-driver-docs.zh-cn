---
title: Pscript 特定的自定义渲染
description: Pscript 特定的自定义渲染
ms.assetid: e984f0f0-1435-4cfd-9a99-297f6a9521f5
keywords:
- 呈现插件 WDK 打印 Pscript5
- Pscript WDK 打印、 自定义呈现
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ebca7cc64b90826bf20a286b4f188a2b4e12a8a2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356002"
---
# <a name="pscript-specific-customized-rendering"></a>Pscript 特定的自定义渲染





Pscript5 允许特定于设备的自定义的代码，用于将 Postscript 命令注入到 Pscript5 驱动程序将发送到打印机设备的数据流。 如果你想要提供此类型的自定义代码，必须提供插件的呈现实现[ **IPrintOemPS::Command** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemps-command)方法。

Pscript5 调用**IPrintOemPS::Command**方法在不同的打印作业的数据流中的点。 函数的参数之一指定一个索引值，表示在数据流中的当前点。 每次调用该函数时，可以检查的索引值，并且可以或不提供额外的流数据。

 

 




