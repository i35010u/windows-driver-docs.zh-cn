---
title: 功能冲突优先级
description: 功能冲突优先级
keywords:
- 打印机功能 WDK Unidrv，冲突优先级
- 冲突优先级 WDK 打印机功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05fd399b03aefeb7da3570f597b587364fc2e609
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797087"
---
# <a name="feature-conflict-priority"></a>功能冲突优先级





功能的冲突优先级标识当 Unidrv 的用户界面代码强制 [选项约束](option-constraints.md)时，功能应具有的优先级。

GPD 分析器从最高优先级到最低优先级，按以下顺序向功能分配冲突优先级：

1.  实际安装的可安装功能。  (参阅 [处理可安装功能和选项](handling-installable-features-and-options.md)。 ) 

2.  \*FeatureType 设置为 PRINTER 属性的功能 \_ 。

3.  \* **FeatureType** 设置为 DOC \_ 属性或作业属性的功能 \_ 。

根据为该功能的 ConflictPriority 属性指定的值，为每个功能类型中的功能分配了相对优先级 \* 。 例如， \_ \* **ConflictPriority** 属性为1的打印机属性功能具有比 \_ \* *_ConflictPriority_* 属性为3的文档属性功能更高的优先级。 没有 ConflictPriority 属性的功能的 \* *_ConflictPriority_* 优先级要低于那些功能。

有关 \* *_FeatureType_* 和 \* *_ConflictPriority_* 特性的详细信息，请参阅 [功能特性](feature-attributes.md)。

 

 




