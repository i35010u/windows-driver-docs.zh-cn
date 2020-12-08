---
title: 'JobHistory 元素 (必需的) '
description: 必需的 JobHistory 元素包含一个 JobSummary 元素列表，这些元素描述扫描设备中最近完成的作业。
keywords:
- JobHistory 元素图像设备
topic_type:
- apiref
api_name:
- wscn JobHistory
api_type:
- Schema
ms.date: 07/06/2020
ms.localizationpriority: medium
ms.openlocfilehash: e8f799386d18204072a699dbafe89cd975e72ea3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834537"
---
# <a name="jobhistory-element-required"></a>JobHistory 元素 (必需的) 

必需的 **JobHistory** 元素包含一个 [**JobSummary**](jobsummary.md) 元素列表，这些元素描述扫描设备中最近完成的作业。

## <a name="usage"></a>使用情况

```xml
<wscn:JobHistory>
  child elements
</wscn:JobHistory>
```

## <a name="attributes"></a>特性

没有特性。

## <a name="child-elements"></a>子元素

| 元素 |
|--|
| [**JobSummary**](jobsummary.md) |

## <a name="parent-elements"></a>父元素

| 元素 |
|--|
| [**GetJobHistoryResponse**](getjobhistoryresponse.md) |

## <a name="remarks"></a>备注

对于扫描仪最近完成的每个作业， **JobHistory** 元素都包含一个 [**JobSummary**](jobsummary.md) 元素。 如果 WSD 扫描服务没有最近完成的作业的记录，则 **JobHistory** 为空。 扫描服务从 [**GetJobHistoryResponse**](getjobhistoryresponse.md)返回此列表。

WSD 扫描服务存储和返回的作业历史记录量是特定于实现的。

## <a name="see-also"></a>请参阅

[**GetJobHistoryResponse**](getjobhistoryresponse.md)

[**JobSummary**](jobsummary.md)
