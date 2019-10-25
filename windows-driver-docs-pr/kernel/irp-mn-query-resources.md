---
title: IRP_MN_QUERY_RESOURCES
description: PnP 管理器使用此 IRP 获取设备的启动配置资源。总线驱动程序必须为需要硬件资源的子设备处理此请求。 函数和筛选器驱动程序不处理此 IRP。
ms.date: 08/12/2017
ms.assetid: b9a6f06b-07d9-4539-bd41-21cdccdc4b25
keywords:
- IRP_MN_QUERY_RESOURCES 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: df4f147781b3311c10cf5a62bf42c589995d1fda
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838568"
---
# <a name="irp_mn_query_resources"></a>IRP\_MN\_查询\_资源


PnP 管理器使用此 IRP 获取设备的启动配置资源。

总线驱动程序必须为需要硬件资源的子设备处理此请求。 函数和筛选器驱动程序不处理此 IRP。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)发送时间
---------

在枚举设备时，PnP 管理器会发送此 IRP。

PnP 管理器在任意线程上下文中以 IRQL 被动\_级别发送此 IRP。

## <a name="input-parameters"></a>输入参数


无

## <a name="output-parameters"></a>输出参数


在 i/o 状态块中返回。

## <a name="io-status-block"></a>I/O 状态块


处理此 IRP 的总线驱动程序将**irp&gt;IOSTATUS**状态设置为 "状态"\_成功或适当的错误状态。

成功时，总线驱动程序会将**Irp&gt;IoStatus**设置为指向[**CM\_资源**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_resource_list)的指针，\_列表中包含所请求的信息。 出现错误时，总线驱动程序会将**Irp&gt;IoStatus**设置为零。

<a name="operation"></a>操作
---------

如果总线驱动程序返回一个资源列表以响应此 IRP，它会从分页内存中分配一个[**CM\_资源\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_resource_list)。 当不再需要该缓冲区时，PnP 管理器将释放它。

如果设备不需要硬件资源，设备的父总线驱动程序将完成 IRP （[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)），而不会修改**irp&gt;IoStatus**或**irp-&gt;IoStatus**。

函数和筛选器驱动程序不会收到此 IRP。

请参阅[即插即用](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)，了解用于处理[即插即用次要 irp](plug-and-play-minor-irps.md)的一般规则。

**正在发送此 IRP**

保留供系统使用。 驱动程序不得发送此 IRP。

驱动程序可以调用[**IoGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)来获取设备的启动配置，同时采用原始格式和已翻译形式。

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


[**CM\_资源\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_resource_list)

[**IoGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)

 

 




