---
title: KSNODETYPE\_电话\_BIDI
description: KSNODETYPE\_电话\_BIDI 节点表示电话呼叫的两面 （双向）。
ms.assetid: 748AC39F-0C15-44A3-BF7B-109A1CB7D145
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
ms.openlocfilehash: b074cdf5a6c501fdea8713461012769e3ce45362
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527130"
---
# <a name="ksnodetypetelephonybidi"></a>KSNODETYPE\_电话\_BIDI


KSNODETYPE\_电话\_BIDI 节点表示电话呼叫的两面 （双向）。

如果设备支持移动电话的电话服务则 KSNODETYPE\_电话\_BIDI 终结点的每个提供程序 （执行器） 是必需的。

## <a name="span-idcellulartelephonyspanspan-idcellulartelephonyspancellular-telephony"></a><span id="CELLULAR_TELEPHONY__"></span><span id="cellular_telephony__"></span>移动电话的电话服务


单选堆栈有一个提供程序 Id (执行程序 Id) 和调用类型 （数据包/线路） 电话呼叫实例连接到特定硬件路径的概念。

该驱动程序将批筛选器的提供者 Id 相关联。 此外将流式处理终结点关联的移动电话上设置此提供程序 Id。 用于批筛选器的提供程序 Id 必须在运行时更改。 音频堆栈将通过使用查询从驱动程序的提供程序 Id [ **KSPROPERTY\_电话\_PROVIDERID**](ksproperty-telephony-providerid.md)。 在此之后，该提供程序 Id 的所有调用都将都发送到特定批筛选器。

**起始和结束移动电话呼叫**

启动和停止调用可通过发送[ **KSPROPERTY\_电话\_CALLCONTROL** ](ksproperty-telephony-callcontrol.md)到批筛选器提供程序。 此属性将调用类型 （数据包交换/线路切换） 进行通信并调用控制操作 （启用或禁用） 驱动程序。 调用控制操作为 Disable 时，将忽略调用类型。

调用启用后，关联 KSNODETYPE\_电话\_BIDI 的插孔状态将进入活动状态的驱动程序和调用状态将更新为*电话\_CALLSTATE\_已启用*. 终止调用、 终结点的插孔状态将更改为拔出和呼叫状态将更新为时*电话\_CALLSTATE\_禁用*。

 

 





