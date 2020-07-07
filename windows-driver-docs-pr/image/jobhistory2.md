---
title: JobHistory 元素（可选）
description: 可选的 JobHistory 元素包含有关扫描作业的信息，这些作业最近完成了处理。
ms.assetid: 7f46044e-ac34-4181-9a35-62dea5ec8c82
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
ms.openlocfilehash: 118664d5e1d033084dcbcc65531b0b4a755f6daf
ms.sourcegitcommit: 40d7d538756767d26bbda636589f614f85a6fab3
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86020046"
---
# <a name="jobhistory-element-optional"></a>JobHistory 元素（可选）

可选的**JobHistory**元素包含有关扫描作业的信息，这些作业最近完成了处理。

## <a name="usage"></a>使用情况

```xml
<wscn:JobHistory>
  child elements
</wscn:JobHistory>
```

## <a name="attributes"></a>属性

没有特性。

## <a name="child-elements"></a>子元素

| 元素 |
|--|
| [**作业**](job.md) |
| [**JobSummary**](jobsummary.md) |

## <a name="parent-elements"></a>父元素

| 元素 |
|--|
| [**GetJobHistoryResponse**](getjobhistoryresponse.md) |
| [**JobTable**](jobtable.md) |

## <a name="remarks"></a>注解

**JobHistory**元素包含已完成处理的最新作业的子集。 由于其他原因，这些作业可以扫描、中止或失败。 此列表中的最大作业数取决于设备。

客户端可以通过[**GetJobHistoryRequest**](getjobhistoryrequest.md)操作元素请求作业历史记录。 WSD 扫描服务在[**GetJobHistoryResponse**](getjobhistoryresponse.md)操作元素中返回此历史记录。

## <a name="see-also"></a>另请参阅

[**GetJobHistoryRequest**](getjobhistoryrequest.md)

[**GetJobHistoryResponse**](getjobhistoryresponse.md)

[**作业**](job.md)

[**JobSummary**](jobsummary.md)

[**JobTable**](jobtable.md)
