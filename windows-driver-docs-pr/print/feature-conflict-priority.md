---
title: 功能冲突优先级
description: 功能冲突优先级
ms.assetid: 1185f983-ed04-4610-8b93-684ae3e07e84
keywords:
- 打印机功能 WDK Unidrv，冲突优先级
- 冲突优先级 WDK 打印机功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aef16af3fd1d3b399110e941ef809c4d400a5075
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541325"
---
# <a name="feature-conflict-priority"></a>功能冲突优先级





一项功能的冲突优先级标识 Unidrv 的用户界面代码强制执行时，应具有一项功能的优先级[选项约束](option-constraints.md)。

从最高到最低优先级，GPD 分析器将冲突优先级分配给一项功能按以下顺序：

1.  实际安装的可安装功能。 (请参阅[处理可安装的功能和选项](handling-installable-features-and-options.md)。)

2.  使用功能\*FeatureType 设置为打印机\_属性。

3.  使用功能\* **FeatureType**设置为文档\_属性或作业\_属性。

在每个功能类型的功能分配基于为该功能的指定的值的相对优先级\*ConflictPriority 属性。 因此，对于示例中，打印机\_属性使用的功能\* **ConflictPriority**为 1 的属性的优先级高于 DOC\_属性功能\* **ConflictPriority** 3 的属性。 不具有的功能\* **ConflictPriority**属性具有较低的优先级比执行操作。

有关详细信息\* **FeatureType**并\* **ConflictPriority**特性，请参见[功能属性](feature-attributes.md)。

 

 




