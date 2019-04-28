---
title: TTD 位置对象
description: 本部分介绍与时间旅行调试关联的位置模型对象。
ms.date: 12/19/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b0fc92625a91645eb807b2ebfae44420ca5e089
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349002"
---
# <a name="ttd-position-objects"></a>TTD 位置对象
## <a name="description"></a>描述
*位置*对象用于描述时间旅行跟踪中的位置。 两个由冒号分隔的十六进制数字通常所描述的位置对象。 十六进制数字的第一个是*序列*，第二个*步骤*。

FFFFFFFFFFFFFFFE:0 中的位置指示跟踪的末尾。

## <a name="properties"></a>属性

| 属性 | 描述 |
| --- | --- |
| 序列 | 与位置相关的序列化点。 |
| 步骤 | 从该线程便可转到此位置中的序列点的步骤数。 |

## <a name="methods"></a>方法

| 方法 | 描述 |
| --- | --- |
| SeekTo() | 时间转移到此位置在跟踪中。 |

## <a name="example-usage"></a>示例用法
*挂起的信息*



## <a name="see-also"></a>请参阅

[时间旅行调试-时间旅行调试对象简介](time-travel-debugging-object-model.md)

[按照时间顺序逐个调试-概述](time-travel-debugging-overview.md)

---


