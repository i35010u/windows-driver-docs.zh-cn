---
title: 筛选器引擎
description: 筛选器引擎
ms.assetid: 87bf23c7-4086-4016-b712-a083d3d69bbe
keywords:
- 筛选引擎 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85a876b83206b0285f12054b8f8399f951c5977c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834709"
---
# <a name="filter-engine"></a>筛选器引擎


*筛选器引擎*是 Windows 筛选平台的组件，用于存储筛选器并执行筛选器仲裁。 [筛选器将添加](filter.md)到指定[筛选层](filtering-layer.md)的筛选器引擎中，以便筛选器引擎可以执行所需的筛选操作（允许、删除或标注）。 如果筛选器引擎中的筛选器为筛选器操作指定了[标注](callout.md)，则筛选器引擎将调用标注的[*classifyFn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0)函数，以便标注能够处理网络数据。

 

 





