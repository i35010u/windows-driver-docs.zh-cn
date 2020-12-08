---
title: 流式处理类 SRB 参考
description: 流式处理类 SRB 参考
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0230797c07401333b7a20276a3ed137b66ec3244
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839847"
---
# <a name="stream-class-srb-reference"></a>流式处理类 SRB 参考


## <span id="ddk_stream_class_srb_reference_ks"></span><span id="DDK_STREAM_CLASS_SRB_REFERENCE_KS"></span>


类驱动程序使用 [**HW \_ 流 \_ 请求 \_ 块**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block) 结构将 SRB 请求传递到微型驱动程序。 在本参考部分中，pSRB 指的是指向 HW \_ STREAM \_ REQUEST \_ BLOCK 对象的指针。 流类驱动程序在调用微型驱动程序提供的回调时传递此指针。

SRB 请求是设备/实例特定的或特定于流的。 根据 SRB 命令，可在 HW \_ 流请求块中传递其他参数 \_ \_ 。

请参阅 [特定于设备的命令代码](device-specific-command-codes.md) 和 [特定于流的命令代码](stream-specific-command-codes.md)。

 

