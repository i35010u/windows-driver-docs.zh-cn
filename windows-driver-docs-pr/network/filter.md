---
title: 筛选器
description: 筛选器
keywords:
- 筛选 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4319e8f0bfa60d150d177a9d94477d65771229b0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805221"
---
# <a name="filter"></a>筛选器


*筛选器* 定义用于筛选 tcp/ip 网络数据的多个筛选条件，以及在所有筛选条件都为 true 时要对数据执行的操作。 如果筛选器需要额外处理网络数据，则可以指定筛选器操作的 [标注](callout.md) 。 如果此类筛选器的筛选条件全部为 true，则 [筛选器引擎](filter-engine.md) 会将网络数据传递到指定的标注进行其他处理。

 

 





