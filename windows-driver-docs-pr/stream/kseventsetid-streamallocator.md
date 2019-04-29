---
title: KSEVENTSETID\_StreamAllocator
description: KSEVENTSETID\_StreamAllocator 事件集指定两个事件。
ms.assetid: 2ca3914c-b3f3-467d-86ef-fe3331421e27
keywords:
- KSEVENTSETID_StreamAllocator 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSEVENTSETID_StreamAllocator
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd6adec10ae3f7e83ce5890d48b5755427a9425d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334035"
---
# <a name="kseventsetidstreamallocator"></a>KSEVENTSETID\_StreamAllocator


KSEVENTSETID\_StreamAllocator 事件集指定两个事件。 服务未完成的分配请求通过 IRP 接口的默认分配器实现内部使用一个事件。 公共事件，另一个，用于通知的免费帧可用性的客户端。

KSEVENTSETID\_StreamAllocator 事件集包括：

[**KSEVENT\_STREAMALLOCATOR\_INTERNAL\_FREEFRAME**](ksevent-streamallocator-internal-freeframe.md)

[**KSEVENT\_STREAMALLOCATOR\_FREEFRAME**](ksevent-streamallocator-freeframe.md)

 

 





