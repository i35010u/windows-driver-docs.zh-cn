---
title: 筛选器引擎
description: 筛选器引擎
keywords:
- 筛选引擎 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b569f2ef1f55f5472b29881372f80d723b8ab7aa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788361"
---
# <a name="filter-engine"></a>筛选器引擎


*筛选器引擎* 是 Windows 筛选平台的组件，用于存储筛选器并执行筛选器仲裁。 [筛选器将添加](filter.md) 到指定 [筛选层](filtering-layer.md) 的筛选器引擎中，以便筛选器引擎可以 (允许、删除或标注) 执行所需的筛选操作。 如果筛选器引擎中的筛选器为筛选器操作指定了 [标注](callout.md) ，则筛选器引擎将调用标注的 [*classifyFn*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0) 函数，以便标注能够处理网络数据。

 

