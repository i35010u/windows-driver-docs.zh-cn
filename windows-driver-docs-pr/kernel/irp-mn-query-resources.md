---
title: IRP_MN_QUERY_RESOURCES
description: PnP 管理器使用此 IRP 获取设备的启动配置资源。总线驱动程序必须为需要硬件资源的子设备处理此请求。 函数和筛选器驱动程序不处理此 IRP。
ms.date: 08/12/2017
ms.assetid: b9a6f06b-07d9-4539-bd41-21cdccdc4b25
keywords:
- IRP_MN_QUERY_RESOURCES 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 0603c886626c2e05c244115ab4d7e0310bb6e8c9
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191475"
---
# <a name="irp_mn_query_resources"></a>IRP \_ MN \_ 查询 \_ 资源


PnP 管理器使用此 IRP 获取设备的启动配置资源。

总线驱动程序必须为需要硬件资源的子设备处理此请求。 函数和筛选器驱动程序不处理此 IRP。

## <a name="value"></a>值

0x0A

<a name="major-code"></a>主要代码
----------

[**IRP \_ MJ \_ PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>发送时间
---------

在枚举设备时，PnP 管理器会发送此 IRP。

PnP 管理器在 \_ 任意线程上下文中以 IRQL 被动级别发送此 IRP。

## <a name="input-parameters"></a>输入参数


无

## <a name="output-parameters"></a>输出参数


在 i/o 状态块中返回。

## <a name="io-status-block"></a>I/o 状态块


处理此 IRP 的总线驱动程序将 **irp- &gt; IoStatus** 设置为状态 " \_ 成功" 或相应的 "错误" 状态。

成功时，总线驱动程序将 ** &gt; IoStatus** 设置为指向包含所请求信息的 [**CM \_ 资源列表 \_ **](/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_resource_list) 的指针。 出现错误时，总线驱动程序将 **Irp- &gt; IoStatus** 设置为零。

<a name="operation"></a>操作
---------

如果总线驱动程序返回资源列表以响应此 IRP，则会从分页内存中分配 [**CM \_ 资源 \_ 列表**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_resource_list) 。 当不再需要该缓冲区时，PnP 管理器将释放它。

如果设备不需要硬件资源，设备的父总线驱动程序将完成 IRP ([**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)) ，而不会修改 **irp- &gt; IoStatus** 或 **irp- &gt; IoStatus**。

函数和筛选器驱动程序不会收到此 IRP。

请参阅 [即插即用](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play) ，了解用于处理 [即插即用次要 irp](plug-and-play-minor-irps.md)的一般规则。

**正在发送此 IRP**

预留给系统使用。 驱动程序不得发送此 IRP。

驱动程序可以调用 [**IoGetDeviceProperty**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty) 来获取设备的启动配置，同时采用原始格式和已翻译形式。

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

## <a name="see-also"></a>另请参阅


[**CM \_ 资源列表 \_**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_resource_list)

[**IoGetDeviceProperty**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)

 

