---
title: TTD 位置对象
description: 本部分介绍与时间行程调试关联的位置模型对象。
ms.date: 12/19/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6daeb58ece76fa37453bb0e1aa26002aff8c7e3a
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916182"
---
# <a name="ttd-position-objects"></a>TTD 位置对象

## <a name="description"></a>描述

*Position*对象用于描述时间行程跟踪中的位置。 位置对象通常由用冒号分隔的两个十六进制数字描述。 第一个十六进制数字是*序列*，第二个是*步骤*。

FFFFFFFFFFFFFFFE 的位置：0指示跟踪的结束。

## <a name="properties"></a>“属性”

| 属性 | 描述 |
| --- | --- |
| 序列 | 与位置相关的序列点。 |
| 步骤 | 此线程中的序列点要从此位置获取的步骤数。 |

## <a name="methods"></a>方法

| 方法 | 描述 |
| --- | --- |
| SeekTo() | 时间转移到跟踪中的此位置。 |

## <a name="example-usage"></a>示例用法

*待处理信息*



## <a name="see-also"></a>另请参阅

[旅行调试-时间行程调试对象简介](time-travel-debugging-object-model.md)

[行程调试-概述](time-travel-debugging-overview.md)
