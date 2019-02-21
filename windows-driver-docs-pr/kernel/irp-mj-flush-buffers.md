---
title: IRP_MJ_FLUSH_BUFFERS
description: 具有内部缓存中对数据的设备驱动程序和维护数据的内部缓冲区的驱动程序必须处理此请求 DispatchFlushBuffers 例程中。
ms.date: 08/12/2017
ms.assetid: c1023999-0c80-4c09-a9ea-a9422184bba7
keywords:
- IRP_MJ_FLUSH_BUFFERS 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: dafd90b42a77ddaa816278fd6b484ce6a664d6f6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523561"
---
# <a name="irpmjflushbuffers"></a>IRP\_MJ\_刷新\_缓冲区


与内部缓存的数据和维护内部缓冲区的数据必须处理此请求中的驱动程序的设备的驱动程序[ *DispatchFlushBuffers* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。

<a name="when-sent"></a>发送时间
---------

刷新请求回执指示驱动程序应刷新设备的缓存或其内部缓冲区或，可能是，应放弃其内部缓冲区中的数据。

## <a name="input-parameters"></a>输入参数


无

## <a name="output-parameters"></a>输出参数


无

<a name="operation"></a>操作
---------

该驱动程序将传输当前缓存在设备中或完成刷新请求之前保存在驱动程序的内部缓冲区中的任何数据。 驱动程序只在内部缓冲的数据的设备可能会只是放弃当前缓冲的设备数据完成刷新 IRP，具体取决于其设备的特性之前。

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
<td>Wdm.h 中 （包括 wdm.h 中、 Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[*DispatchFlushBuffers*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

 

 




