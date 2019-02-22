---
title: 打印机属性格式
description: 打印机属性格式
ms.assetid: 676e9220-4990-4581-8f23-79083afc311c
keywords:
- 打印机属性 WDK Unidrv，格式
- 格式 WDK 打印机属性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79c2d9dd6cae9cf39fd31f135b288ed2b6b452b8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547699"
---
# <a name="printer-attribute-format"></a>打印机属性格式





若要在 GPD 文件中指定打印机属性条目，请使用以下格式：

\* *AttributeName* :*AttributeValue*

其中*AttributeName*是一个预定义的名称的某一[属性类型](attribute-types.md)，并*AttributeValue*是之一[GPD 值类型](gpd-value-types.md).

例如， \*ModelName 属性用于指定描述打印机硬件的文本字符串。 若要将值分配给此属性，无法 GPD 文件中放置以下行：

```cpp
*ModelName: "Canon Bubble-Jet BJC-600"
```

所有特性名称都预定义和 Unidrv 的 GPD 分析器识别。

 

 




