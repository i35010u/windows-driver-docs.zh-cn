---
title: IRP_MN_QUERY_RESOURCE_REQUIREMENTS
description: PnP 管理器使用此 IRP 获取设备的资源需求列表。总线驱动程序必须为需要硬件资源的子设备处理此请求。
ms.date: 08/12/2017
ms.assetid: 5a77f8d6-2b6b-4eff-8d48-e7942976ec52
keywords:
- IRP_MN_QUERY_RESOURCE_REQUIREMENTS 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 2e42098dd6e7869e0e562bbcca7b756f8e86ed9e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827988"
---
# <a name="irp_mn_query_resource_requirements"></a>IRP\_MN\_查询\_资源\_要求


PnP 管理器使用此 IRP 获取设备的资源需求列表。

总线驱动程序必须为需要硬件资源的子设备处理此请求。 总线筛选器驱动程序可以处理此请求。 函数和筛选器驱动程序不处理此 IRP。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)发送时间
---------

在将资源分配给设备之前以及当驱动程序报告其设备的资源要求已更改时，PnP 管理器会发送此 IRP。

PnP 管理器在任意线程上下文中以 IRQL 被动\_级别发送此 IRP。

## <a name="input-parameters"></a>输入参数


无

## <a name="output-parameters"></a>输出参数


在 i/o 状态块中返回。

## <a name="io-status-block"></a>I/O 状态块


处理此 IRP 的驱动程序将**irp&gt;IOSTATUS**状态设置为状态\_成功或相应的错误状态。

成功时，驱动程序将**Irp&gt;IoStatus**设置为指向[**IO\_资源\_要求\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_resource_requirements_list)的指针，该列表包含所请求的信息。 出现错误时，驱动程序将**Irp&gt;IoStatus**设置为零。

<a name="operation"></a>操作
---------

如果总线驱动程序返回一个资源要求列表以响应此 IRP，则会从分页内存中 **\_列表分配 IO\_资源\_需求**。 当不再需要该缓冲区时，PnP 管理器将释放它。

如果设备不需要硬件资源，设备的总线驱动程序将完成 IRP （[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)），而不会修改**irp&gt;IoStatus**或**irp-&gt;IoStatus**。

如果总线筛选器驱动程序处理此 IRP，则它会修改总线驱动程序创建的资源需求列表。 总线筛选器驱动程序会修改 IRP 上的列表备份设备堆栈。 总线筛选器驱动程序必须保留资源需求列表中资源的顺序，并且不得更改其不处理的资源标记。 如果总线筛选器驱动程序更改了资源需求列表的大小，则驱动程序必须从分页内存中分配一个新的结构，并释放以前的结构。 如果总线筛选器驱动程序向列表中添加了新的资源要求，并向设备分配了资源，则驱动程序必须筛选 IRP\_MN 中的新资源[ **\_启动\_设备**](irp-mn-start-device.md)IRP，使其不会传递给总线驱动程序。

函数和非总线筛选器驱动程序不处理此 IRP;它们将其传递到下一个较低的驱动程序，并且不会对**Irp&gt;IoStatus**进行任何更改。

请参阅[即插即用](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)，了解用于处理[即插即用次要 irp](plug-and-play-minor-irps.md)的一般规则。

**正在发送此 IRP**

保留供系统使用。 驱动程序不得发送此 IRP。

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


[**IO\_资源\_需求\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_resource_requirements_list)

 

 




