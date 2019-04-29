---
title: AV/C 流式处理协议驱动程序函数代码
description: AV/C 流式处理协议驱动程序函数代码
ms.assetid: c76662fc-8bb9-411a-8672-d00a4533e952
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56185b3b2b2cb69df674caf50bf844e4c008e852
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323521"
---
# <a name="avc-streaming-protocol-driver-function-codes"></a>AV/C 流式处理协议驱动程序函数代码


## <span id="ddk_av_c_streaming_protocol_driver_function_codes_ks"></span><span id="DDK_AV_C_STREAMING_PROTOCOL_DRIVER_FUNCTION_CODES_KS"></span>


AV/C 流式处理筛选器驱动程序截获 Irp 沿着设备堆栈上。

要与其*avcstrm.sys*，子单元驱动程序必须设置其 IRP **IoControlCode**成员添加到 IOCTL\_AVCSTRM\_类。

若要发出 I/O 请求，包括标头文件*avcstrm.h*，包括与 Microsoft Windows Driver Kit (WDK)。

 

 





