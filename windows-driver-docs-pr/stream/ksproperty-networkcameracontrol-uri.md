---
title: KSPROPERTY_NETWORKCAMERACONTROL_URI
description: 从 Onvif 协议相机启用获取流 URI 有效负载。
ms.date: 10/05/2020
ms.localizationpriority: medium
ms.openlocfilehash: 50404887c70cdbe570fd74980b695145bfbe1fe4
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733227"
---
# <a name="ksproperty_networkcameracontrol_uri"></a>KSPROPERTY_NETWORKCAMERACONTROL_URI

KSPROPERTY_NETWORKCAMERACONTROL_URI 属性允许从 Onvif 协议相机获取流 URI 负载。 有效负载是一个宽字符、以 null 结尾的字符串，表示流式处理 URI (RSTP/HTTP URI) 。

## <a name="usage-summary-table"></a>使用情况摘要表

| 获取 | 设置 | 属性描述符类型 | 属性值类型 |
|--|--|--|--|
| 是 | 否 | [KSPROPERTY_NETWORKCAMERACONTROL_PROPERTY](/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_networkcameracontrol_property) | LONG |

## <a name="requirements"></a>要求

**标头：** ksmedia (包含 ksmedia) 
