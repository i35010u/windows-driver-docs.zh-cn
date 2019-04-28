---
title: 流式处理类 SRB 参考
description: 流式处理类 SRB 参考
ms.assetid: fdd2de58-8825-429a-937a-0bd27a180f2a
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd87f49a4c10ee036c03699b051b6f5969fa21cf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339839"
---
# <a name="stream-class-srb-reference"></a>流式处理类 SRB 参考


## <span id="ddk_stream_class_srb_reference_ks"></span><span id="DDK_STREAM_CLASS_SRB_REFERENCE_KS"></span>


类驱动程序将使用[ **HW\_流\_请求\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff559702)结构传递 SRB 请求微型驱动程序。 本参考部分 pSRB 是指指向 HW\_流\_请求\_块对象。 当调用微型驱动程序提供的回调，stream 类驱动程序将此指针传递。

SRB 请求是特定于实例的设备/或特定于流。 在硬件中可能会根据 SRB 命令中，传递其他参数\_流\_请求\_阻止。

请参阅[特定于设备的命令代码](device-specific-command-codes.md)并[Stream 特定命令代码](stream-specific-command-codes.md)。

 

 





