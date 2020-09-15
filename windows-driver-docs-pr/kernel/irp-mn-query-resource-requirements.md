---
title: IRP_MN_QUERY_RESOURCE_REQUIREMENTS
description: PnP 管理器使用此 IRP 获取设备的资源需求列表。总线驱动程序必须为需要硬件资源的子设备处理此请求。
ms.date: 08/12/2017
ms.assetid: 5a77f8d6-2b6b-4eff-8d48-e7942976ec52
keywords:
- IRP_MN_QUERY_RESOURCE_REQUIREMENTS 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 84ad93505f20d4f1c1e41bfb998ec28cec617cb0
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104080"
---
# <a name="irp_mn_query_resource_requirements"></a>IRP \_ MN \_ 查询 \_ 资源 \_ 需求


PnP 管理器使用此 IRP 获取设备的资源需求列表。

总线驱动程序必须为需要硬件资源的子设备处理此请求。 总线筛选器驱动程序可以处理此请求。 函数和筛选器驱动程序不处理此 IRP。

## <a name="value"></a>值

0x0B

<a name="major-code"></a>主要代码
----------

[**IRP \_ MJ \_ PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>发送时间
---------

在将资源分配给设备之前以及当驱动程序报告其设备的资源要求已更改时，PnP 管理器会发送此 IRP。

PnP 管理器在 \_ 任意线程上下文中以 IRQL 被动级别发送此 IRP。

## <a name="input-parameters"></a>输入参数


无

## <a name="output-parameters"></a>输出参数


在 i/o 状态块中返回。

## <a name="io-status-block"></a>I/o 状态块


处理此 IRP 的驱动程序将 **irp &gt; IoStatus** 设置为状态 " \_ 成功" 或相应的错误状态。

成功时，驱动程序将 ** &gt; IoStatus** 设置为指向包含所请求信息的 [**IO \_ 资源 \_ 需求 \_ 列表**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_resource_requirements_list) 的指针。 出现错误时，驱动程序将 **Irp- &gt; IoStatus** 设置为零。

<a name="operation"></a>操作
---------

如果总线驱动程序返回资源要求列表以响应此 IRP，则它会从分页内存中分配 **IO \_ 资源 \_ 需求 \_ 列表** 。 当不再需要该缓冲区时，PnP 管理器将释放它。

如果设备不需要硬件资源，设备的总线驱动程序将完成 IRP ([**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)) ，而无需修改 **irp- &gt; IoStatus** 或 **irp- &gt; IoStatus**。

如果总线筛选器驱动程序处理此 IRP，则它会修改总线驱动程序创建的资源需求列表。 总线筛选器驱动程序会修改 IRP 上的列表备份设备堆栈。 总线筛选器驱动程序必须保留资源需求列表中资源的顺序，并且不得更改其不处理的资源标记。 如果总线筛选器驱动程序更改了资源需求列表的大小，则驱动程序必须从分页内存中分配一个新的结构，并释放以前的结构。 如果总线筛选器驱动程序向列表中添加新的资源要求，并将资源分配给设备，则驱动程序必须筛选 [**IRP \_ MN \_ 启动 \_ 设备**](irp-mn-start-device.md) irp 之外的新资源，以使其不会传递给总线驱动程序。

函数和非总线筛选器驱动程序不处理此 IRP;它们将其传递到下一个较低的驱动程序，并且不会更改 ** &gt; IoStatus**。

请参阅 [即插即用](./introduction-to-plug-and-play.md) ，了解用于处理 [即插即用次要 irp](plug-and-play-minor-irps.md)的一般规则。

**正在发送此 IRP**

预留给系统使用。 驱动程序不得发送此 IRP。

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
<td>Wdm.h（包括 Wdm.h、Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**IO \_ 资源 \_ 需求 \_ 列表**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_resource_requirements_list)

 

