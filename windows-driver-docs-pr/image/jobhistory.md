---
title: JobHistory 元素（必需）
description: 必需的 JobHistory 元素包含一个 JobSummary 元素列表，这些元素描述扫描设备中最近完成的作业。
ms.assetid: d1439e56-b2fe-4db8-b063-56537a3346c6
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
ms.openlocfilehash: 4f16fcbeec046dbeabc8af1d81ce4f83fb749a90
ms.sourcegitcommit: 40d7d538756767d26bbda636589f614f85a6fab3
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86020048"
---
# <a name="jobhistory-element-required"></a>JobHistory 元素（必需）

必需的**JobHistory**元素包含一个[**JobSummary**](jobsummary.md)元素列表，这些元素描述扫描设备中最近完成的作业。

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
| [**JobSummary**](jobsummary.md) |

## <a name="parent-elements"></a>父元素

| 元素 |
|--|
| [**GetJobHistoryResponse**](getjobhistoryresponse.md) |

## <a name="remarks"></a>注解

对于扫描仪最近完成的每个作业， **JobHistory**元素都包含一个[**JobSummary**](jobsummary.md)元素。 如果 WSD 扫描服务没有最近完成的作业的记录，则**JobHistory**为空。 扫描服务从[**GetJobHistoryResponse**](getjobhistoryresponse.md)返回此列表。

WSD 扫描服务存储和返回的作业历史记录量是特定于实现的。

## <a name="see-also"></a>另请参阅

[**GetJobHistoryResponse**](getjobhistoryresponse.md)

[**JobSummary**](jobsummary.md)
