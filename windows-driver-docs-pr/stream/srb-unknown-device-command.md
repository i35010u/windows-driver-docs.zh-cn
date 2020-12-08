---
title: SRB \_ UNKNOWN \_ DEVICE \_ 命令
description: SRB \_ UNKNOWN \_ DEVICE \_ 命令
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4df3d91f82ed0faaeeeb152c32ee38472b1466f4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824869"
---
# <a name="srb_unknown_device_command"></a>SRB \_ UNKNOWN \_ DEVICE \_ 命令


## <span id="ddk_srb_unknown_device_command_ks"></span><span id="DDK_SRB_UNKNOWN_DEVICE_COMMAND_KS"></span>


类驱动程序将发送此请求，以将不知道如何处理的 Irp 传递到微型驱动程序。 *pSrb* - pSrb &gt;**Irp** 指向未处理的 irp。 请参阅 [**HW \_ 流 \_ 请求 \_ 块**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)。

此请求可用作 stream 类不理解的 irp 的 IRP 传递机制，但微型驱动程序可能。 例如，stream 类不处理的 (PnP) Irp 有多个即插即用，但1394照相机驱动程序会这样做。

如果微型驱动程序不支持 SRB \_ 未知 \_ 设备 \_ 命令或不处理 IRP，则应将 pSRB &gt; 状态设置为 "未实现的状态 \_ " \_ 。

 

