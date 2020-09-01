---
title: 筛选器引擎
description: 筛选器引擎
ms.assetid: 87bf23c7-4086-4016-b712-a083d3d69bbe
keywords:
- 筛选引擎 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: abd5e833a0d1823448490dbfc3589b3c40ab5e0c
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210189"
---
# <a name="filter-engine"></a>筛选器引擎


*筛选器引擎*是 Windows 筛选平台的组件，用于存储筛选器并执行筛选器仲裁。 [筛选器将添加](filter.md) 到指定 [筛选层](filtering-layer.md) 的筛选器引擎中，以便筛选器引擎可以 (允许、删除或标注) 执行所需的筛选操作。 如果筛选器引擎中的筛选器为筛选器操作指定了 [标注](callout.md) ，则筛选器引擎将调用标注的 [*classifyFn*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0) 函数，以便标注能够处理网络数据。

 

