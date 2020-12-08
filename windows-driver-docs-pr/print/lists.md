---
title: 列表
description: 列表
keywords:
- GPD 文件条目 WDK Unidrv，列表
- 列出属性 WDK GPD 文件
- LIST 关键字
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7155ce107f85a1835ee980c67d8ce565006990da
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807939"
---
# <a name="lists"></a>列表





若要将一组值分配给某个属性，请使用 LIST 关键字。 格式为：

**LIST** ( *Value1* ， *Value2* ， *Value3* ，...， *ValueN*) 

其中 *Value1*， *Value2*， *Value3*，...， *ValueN* 表示一个或多个值的集合，这些值均为该属性指定的类型。 例如，可以按如下所示指定打印机的颜色平面数据的发送顺序：

```cpp
*ColorPlaneOrder: LIST(YELLOW, MAGENTA, CYAN, BLACK)
```

 

 




