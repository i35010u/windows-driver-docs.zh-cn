---
title: AV/C 流式处理协议驱动程序函数代码
description: AV/C 流式处理协议驱动程序函数代码
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fec5632e6064e207ffe6357605c853a4be91cbe0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783773"
---
# <a name="avc-streaming-protocol-driver-function-codes"></a>AV/C 流式处理协议驱动程序函数代码


## <span id="ddk_av_c_streaming_protocol_driver_function_codes_ks"></span><span id="DDK_AV_C_STREAMING_PROTOCOL_DRIVER_FUNCTION_CODES_KS"></span>


AV/C 流式处理筛选器驱动程序会按设备堆栈的方式截获 Irp。

若要与 *avcstrm.sys* 通信，子单位驱动程序必须将其 IRP 的 **IoControlCode** 成员设置为 IOCTL \_ AVCSTRM \_ 类。

若要发出 i/o 请求，请包含头文件 *avcstrm*，该文件包含在 Microsoft Windows 驱动程序工具包 (WDK) 中。

 

 





