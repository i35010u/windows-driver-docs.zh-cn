---
title: 列表
description: 列表
ms.assetid: 69b928fa-8348-437a-ac4d-677f272615dd
keywords:
- GPD 文件条目 WDK Unidrv，列表
- 列出属性 WDK GPD 文件
- 列表关键字
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6c21fc24a8c9c36a0c97f74496a7ea1dfec64a6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519342"
---
# <a name="lists"></a>列表





若要将一组值分配到属性，请使用列表关键字。 格式为：

**列表**( *Value1* ， *Value2* ， *Value3* ，...， *ValueN*)

其中*Value1*， *Value2*， *Value3*，...， *ValueN*表示一组的一个或多个值，所有指定的属性的类型。 例如，可以按以下方式指定应发送打印机的颜色平面数据的顺序：

```cpp
*ColorPlaneOrder: LIST(YELLOW, MAGENTA, CYAN, BLACK)
```

 

 




