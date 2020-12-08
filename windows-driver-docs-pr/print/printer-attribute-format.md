---
title: 打印机属性格式
description: 打印机属性格式
keywords:
- 打印机属性 WDK Unidrv，格式
- 格式化 WDK 打印机属性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 578e449b7433e13f5b67eebdfdfe4b56f026471d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807375"
---
# <a name="printer-attribute-format"></a>打印机属性格式





若要在 GPD 文件中指定打印机属性项，请使用以下格式：

\**AttributeName* ： *AttributeValue*

其中， *AttributeName* 是属于某个 [属性类型](attribute-types.md)的预定义名称，而 *AttributeValue* 是 [GPD 值类型](gpd-value-types.md)之一。

例如， \* ModelName 属性用于指定描述打印机硬件的文本字符串。 若要为此属性指定值，可以在 GPD 文件中放置以下行：

```cpp
*ModelName: "Canon Bubble-Jet BJC-600"
```

所有属性名称都是预定义的，并由 Unidrv 的 GPD 分析程序识别。

 

 




