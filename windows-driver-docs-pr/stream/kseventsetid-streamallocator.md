---
title: KSEVENTSETID \_ StreamAllocator
description: KSEVENTSETID \_ StreamAllocator 事件集指定两个事件。
keywords:
- KSEVENTSETID_StreamAllocator 流媒体设备
topic_type:
- apiref
api_name:
- KSEVENTSETID_StreamAllocator
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe061612be05a5c51ffbee4f830a1b41cb26fcd0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840583"
---
# <a name="kseventsetid_streamallocator"></a>KSEVENTSETID \_ StreamAllocator


KSEVENTSETID \_ StreamAllocator 事件集指定两个事件。 在默认的分配器实现内部使用一个事件来处理通过 IRP 接口发出的未完成的分配请求。 另一种是公共事件，用于通知客户端的可用帧可用性。

KSEVENTSETID \_ StreamAllocator 事件集包括：

[**KSEVENT \_ STREAMALLOCATOR \_ INTERNAL \_ FREEFRAME**](ksevent-streamallocator-internal-freeframe.md)

[**KSEVENT \_ STREAMALLOCATOR \_ FREEFRAME**](ksevent-streamallocator-freeframe.md)

 

 





