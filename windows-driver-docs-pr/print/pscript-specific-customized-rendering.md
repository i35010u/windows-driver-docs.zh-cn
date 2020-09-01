---
title: Pscript 特定的自定义渲染
description: Pscript 特定的自定义渲染
ms.assetid: e984f0f0-1435-4cfd-9a99-297f6a9521f5
keywords:
- 呈现插件 WDK 打印，Pscript5
- Pscript WDK 打印，自定义呈现
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83c5a2f37e04ae60e2804daa7488e1c6d322a96b
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217108"
---
# <a name="pscript-specific-customized-rendering"></a>Pscript 特定的自定义渲染





Pscript5 允许设备特定的自定义代码将 Postscript 命令注入到 Pscript5 驱动程序发送到打印机设备的数据流。 如果要提供此类型的自定义代码，则必须提供实现 [**IPrintOemPS：： Command**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemps-command) 方法的呈现插件。

Pscript5 在打印作业的数据流中的各种点调用 **IPrintOemPS：：命令** 方法。 函数的一个参数指定一个索引值，该值表示数据流中的当前点。 每次调用函数时，它都可以检查索引值并提供额外的流数据。

 

