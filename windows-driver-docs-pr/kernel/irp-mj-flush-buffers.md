---
title: IRP_MJ_FLUSH_BUFFERS
description: 对于包含数据的内部缓存的设备的驱动程序，维护数据的内部缓冲区的驱动程序必须在 DispatchFlushBuffers 例程中处理此请求。
ms.date: 08/12/2017
ms.assetid: c1023999-0c80-4c09-a9ea-a9422184bba7
keywords:
- IRP_MJ_FLUSH_BUFFERS 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 4aaa0a47ad4cd013883d5d1b988f026791bac342
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838606"
---
# <a name="irp_mj_flush_buffers"></a>IRP\_MJ\_刷新\_缓冲区


对于包含数据的内部缓存的设备的驱动程序，维护数据的内部缓冲区的驱动程序必须在[*DispatchFlushBuffers*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程中处理此请求。

<a name="when-sent"></a>发送时间
---------

接收刷新请求指示驱动程序应刷新设备的缓存或其内部缓冲区，或者可能会在其内部缓冲区中丢弃数据。

## <a name="input-parameters"></a>输入参数


无

## <a name="output-parameters"></a>输出参数


无

<a name="operation"></a>操作
---------

驱动程序会传输当前缓存在设备中的所有数据，或在完成刷新请求之前保存在驱动程序的内部缓冲区中。 在内部缓冲数据的仅输入设备的驱动程序可能只在完成刷新 IRP 之前丢弃当前缓冲的设备数据，具体取决于其设备的性质。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Wdm .h （包括 Wdm、Ntddk 或 Ntifs）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[*DispatchFlushBuffers*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

 

 




