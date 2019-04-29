---
title: 调试器数据模型-集合 Namespace
description: 提供用于创建和操作的对象的集合的方法。
ms.date: 12/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3814c3a8aabaed01abd2b1b26fccda31d0bb50dd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376077"
---
# <a name="the-collections-namespace"></a>集合 Namespace
## <a name="summary"></a>总结
该集合命名空间提供用于创建和操作的对象的集合的方法 (例如： 可迭代对象都)。 API 扩展将扩展具有以下属性和方法的现有集合命名空间：

## <a name="object-methods"></a>对象方法
|名称|签名|描述|
|--- |--- |--- |
|CreateArray|CreateArray([value]...)|创建一个可索引且可迭代数组超出传递给该方法的参数集。 此方法可用于创建查询的起点或平展|