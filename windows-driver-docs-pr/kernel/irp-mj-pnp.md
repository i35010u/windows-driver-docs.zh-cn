---
title: IRP_MJ_PNP
description: 所有驱动程序必须准备为 DispatchPnP 例程中 IRP_MJ_PNP 请求提供服务。
ms.date: 08/12/2017
ms.assetid: db838761-b838-44fd-bc77-c9d55d2c4a41
keywords:
- IRP_MJ_PNP Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: eeaf4ba1c289f3fa4aaa84bc14f9f0f758a7c6b6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534186"
---
# <a name="irpmjpnp"></a>IRP\_MJ\_PNP


所有驱动程序必须准备对服务**IRP\_MJ\_PNP**中的请求[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。

<a name="when-sent"></a>发送时间
---------

PnP 管理器将发送**IRP\_MJ\_PNP**枚举、 资源重新平衡，以及任何其他时间插活动期间请求发生在系统上。 驱动程序还可以发送某些**IRP\_MJ\_PNP**请求，具体取决于次要函数代码。

## <a name="input-parameters"></a>输入参数


取决于处的值**MinorFunction**中当前的 I/O 堆栈 IRP 的位置。 每个**IRP\_MJ\_PNP**请求指定了次要函数代码用于标识请求的即插即用操作。

## <a name="output-parameters"></a>输出参数


取决于处的值**MinorFunction**中当前的 I/O 堆栈 IRP 的位置。

<a name="operation"></a>操作
---------

请参阅[即插即用和播放次要 Irp](plug-and-play-minor-irps.md)有关详细信息**IRP\_MJ\_PNP**请求。

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


[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

 

 




