---
title: SRB\_未知\_设备\_命令
description: SRB\_未知\_设备\_命令
ms.assetid: 89bc2176-e384-48bf-82d8-4a8ab2bd5159
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b7864c4ee05783fbb261ebb4b45c1b47fa9ee5a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837701"
---
# <a name="srb_unknown_device_command"></a>SRB\_未知\_设备\_命令


## <span id="ddk_srb_unknown_device_command_ks"></span><span id="DDK_SRB_UNKNOWN_DEVICE_COMMAND_KS"></span>


类驱动程序将发送此请求，以将不知道如何处理的 Irp 传递到微型驱动程序。 *pSrb*-&gt;**irp**指向未处理的 irp。 请参阅[**HW\_STREAM\_请求\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)。

此请求可用作 stream 类不理解的 irp 的 IRP 传递机制，但微型驱动程序可能。 例如，stream 类不处理多个即插即用（PnP） Irp，但1394照相机驱动程序会这样做。

如果微型驱动程序不支持 SRB\_未知\_设备\_命令或不处理 IRP，则应将&gt;pSRB 状态设置为 "状态"\_\_未实现。

 

 





