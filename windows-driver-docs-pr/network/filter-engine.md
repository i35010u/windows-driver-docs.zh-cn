---
title: 筛选器引擎
description: 筛选器引擎
ms.assetid: 87bf23c7-4086-4016-b712-a083d3d69bbe
keywords:
- 筛选器引擎 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9b66cd33d868881790bb538310ca6524e77f0ff
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521295"
---
# <a name="filter-engine"></a>筛选器引擎


*筛选器引擎*是 Windows 筛选平台存储筛选器并执行筛选器约束性仲裁的组件。 [筛选器](filter.md)添加到筛选器引擎在指定[筛选层](filtering-layer.md)，以便筛选器引擎可以执行所需的筛选操作 （允许、 drop 或标注）。 如果指定了筛选器引擎中的筛选器[标注](callout.md)筛选器的操作筛选器引擎将调用的标注[ *classifyFn* ](https://msdn.microsoft.com/library/windows/hardware/ff544890)函数，以便可以标注处理网络数据。

 

 





