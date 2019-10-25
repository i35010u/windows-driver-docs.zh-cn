---
title: IRP_MJ_PNP
description: 所有驱动程序必须准备好在 DispatchPnP 例程中处理 IRP_MJ_PNP 请求。
ms.date: 08/12/2017
ms.assetid: db838761-b838-44fd-bc77-c9d55d2c4a41
keywords:
- IRP_MJ_PNP 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 50bb59535a4cd7726b8e490b910e22d621f4d47f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838602"
---
# <a name="irp_mj_pnp"></a>IRP\_MJ\_PNP


所有驱动程序都必须做好准备，以便在[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程中\_PNP 请求的服务**IRP\_MJ** 。

<a name="when-sent"></a>发送时间
---------

PnP 管理器将**IRP\_MJ\_PnP**请求在枚举、资源重新平衡以及系统上的任何其他时间即插即用活动之间发送。 驱动程序还可以发送某些**IRP\_MJ\_PNP**请求，具体取决于次要函数代码。

## <a name="input-parameters"></a>输入参数


依赖于 IRP 当前 i/o 堆栈位置中**MinorFunction**处的值。 每个**IRP\_MJ\_PNP**请求指定一个用于标识所请求的 PNP 操作的次要函数代码。

## <a name="output-parameters"></a>输出参数


依赖于 IRP 当前 i/o 堆栈位置中**MinorFunction**处的值。

<a name="operation"></a>操作
---------

请参阅[即插即用次 irp](plug-and-play-minor-irps.md) ，获取有关**IRP\_MJ\_PNP**请求的详细信息。

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


[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

 

 




