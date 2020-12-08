---
title: KSNODETYPE \_ 电话 \_ 双向
description: KSNODETYPE \_ 电话 \_ 双向节点表示电话呼叫 (双向) 的两侧。
keywords:
- KSNODETYPE_TELEPHONY_BIDI 音频设备
topic_type:
- apiref
api_name:
- KSNODETYPE_TELEPHONY_BIDI
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: edd7f6b498c95f9caa905c3af46327f507114303
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799111"
---
# <a name="ksnodetype_telephony_bidi"></a>KSNODETYPE \_ 电话 \_ 双向


KSNODETYPE \_ 电话 \_ 双向节点表示电话呼叫 (双向) 的两侧。

如果设备支持手机网络电话服务，则 \_ \_ 每个提供程序的 KSNODETYPE 电话服务双向终结点 (执行器) 是必需的。

## <a name="span-idcellular_telephony__spanspan-idcellular_telephony__spancellular-telephony"></a><span id="CELLULAR_TELEPHONY__"></span><span id="cellular_telephony__"></span>移动电话服务


此收音机堆栈具有一种提供程序 Id (执行器 Id) 和调用类型 (数据包/线路) ，以将电话呼叫实例连接到特定的硬件路径。

驱动程序将提供程序 Id 关联到波形筛选器。 还将在关联的移动电话流式处理终结点上设置此提供程序 Id。 在运行时，wave 筛选器的提供程序 Id 不得更改。 音频堆栈将使用 [**KSPROPERTY \_ 电话服务 \_ PROVIDERID**](ksproperty-telephony-providerid.md)从驱动程序查询提供程序 Id。 此后，该提供程序 Id 的所有调用都将发送到特定的波形筛选器。

**开始和结束移动电话呼叫**

通过向提供程序的波形筛选器发送 [**KSPROPERTY \_ 电话 \_ CALLCONTROL**](ksproperty-telephony-callcontrol.md) ，开始和停止调用。 此属性将) 启用或禁用) 到驱动程序时，将调用类型 (数据包交换/线路交换和调用控制 (操作通信。 如果调用控制操作为禁用，则忽略调用类型。

一旦启用呼叫， \_ \_ 驱动程序就会激活关联的 KSNODETYPE 电话呼叫的插孔状态，呼叫状态将更新为 *\_ \_ 启用电话服务 CALLSTATE*。 终止呼叫后，终结点的插孔状态将更改为 "已拔出"，呼叫状态将更新为 " *电话服务 \_ CALLSTATE \_ 已禁用*"。

 

 





