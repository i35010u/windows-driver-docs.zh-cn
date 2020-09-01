---
title: 流式处理类 SRB 参考
description: 流式处理类 SRB 参考
ms.assetid: fdd2de58-8825-429a-937a-0bd27a180f2a
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1d21754c9d0dc0daf02c3571a4ac06ebe0f4344
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186267"
---
# <a name="stream-class-srb-reference"></a>流式处理类 SRB 参考


## <span id="ddk_stream_class_srb_reference_ks"></span><span id="DDK_STREAM_CLASS_SRB_REFERENCE_KS"></span>


类驱动程序使用 [**HW \_ 流 \_ 请求 \_ 块**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block) 结构将 SRB 请求传递到微型驱动程序。 在本参考部分中，pSRB 指的是指向 HW \_ STREAM \_ REQUEST \_ BLOCK 对象的指针。 流类驱动程序在调用微型驱动程序提供的回调时传递此指针。

SRB 请求是设备/实例特定的或特定于流的。 根据 SRB 命令，可在 HW \_ 流请求块中传递其他参数 \_ \_ 。

请参阅 [特定于设备的命令代码](device-specific-command-codes.md) 和 [特定于流的命令代码](stream-specific-command-codes.md)。

 

