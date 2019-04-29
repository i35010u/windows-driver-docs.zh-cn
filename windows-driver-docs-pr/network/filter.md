---
title: Filter
description: Filter
ms.assetid: eb8f0e55-eefd-48bb-abaa-0658bc977b5f
keywords:
- 筛选器 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4877b19762c72cf4d5c5d2de063229ceb4d34ec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380924"
---
# <a name="filter"></a>Filter


一个*筛选器*定义多个筛选条件来筛选 TCP/IP 网络数据和操作的所有筛选条件为真时要执行的数据。 如果筛选器需要进行其他处理的网络数据，它可以指定[标注](callout.md)筛选器的操作。 如果这样的筛选器的筛选条件都成立，[筛选器引擎](filter-engine.md)将网络数据传递给其他处理的指定标注。

 

 





