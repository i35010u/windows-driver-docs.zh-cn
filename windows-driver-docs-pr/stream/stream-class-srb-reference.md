---
title: 流式处理类 SRB 参考
description: 流式处理类 SRB 参考
ms.assetid: fdd2de58-8825-429a-937a-0bd27a180f2a
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f325036947d7fbbd09bb0ab3ee6f96f56a795da
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837682"
---
# <a name="stream-class-srb-reference"></a>流式处理类 SRB 参考


## <span id="ddk_stream_class_srb_reference_ks"></span><span id="DDK_STREAM_CLASS_SRB_REFERENCE_KS"></span>


类驱动程序使用[**HW\_STREAM\_请求\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)结构将 SRB 请求传递到微型驱动程序。 在本参考部分中，pSRB 指的是指向 HW\_STREAM\_请求\_块对象的指针。 流类驱动程序在调用微型驱动程序提供的回调时传递此指针。

SRB 请求是设备/实例特定的或特定于流的。 根据 SRB 命令，其他参数可能会传入 HW\_STREAM\_请求\_块。

请参阅[特定于设备的命令代码](device-specific-command-codes.md)和[特定于流的命令代码](stream-specific-command-codes.md)。

 

 





