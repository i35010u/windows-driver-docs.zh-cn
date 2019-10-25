---
title: IRP_MN_QUERY_BUS_INFORMATION
description: PnP 管理器使用此 IRP 来请求设备的父总线的类型和实例编号。总线驱动程序应为其子设备（PDOs）处理此请求。 函数和筛选器驱动程序不处理此 IRP。
ms.date: 08/12/2017
ms.assetid: a7ea1a81-7f03-41c7-8861-a2e1813c15cf
keywords:
- IRP_MN_QUERY_BUS_INFORMATION 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: d46b41d07a6cd4408c505824251e1136bf494d1a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828031"
---
# <a name="irp_mn_query_bus_information"></a>IRP\_MN\_查询\_总线\_信息


PnP 管理器使用此 IRP 来请求设备的父总线的类型和实例编号。

总线驱动程序应为其子设备（PDOs）处理此请求。 函数和筛选器驱动程序不处理此 IRP。

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


总线驱动程序将**Irp&gt;的 IoStatus**设置为 STATUS\_SUCCESS 或适当的错误状态。

成功时，总线驱动程序将**Irp&gt;IoStatus**设置为指向已完成的[**PNP\_总线\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_pnp_bus_information)结构的指针。 （有关详细信息，请参阅 "操作" 一节。）出现错误时，总线驱动程序会将**Irp&gt;IoStatus**设置为零。

函数和筛选器驱动程序不处理此 IRP。

<a name="operation"></a>操作
---------

为响应此 IRP 而返回的信息可用于总线上设备的函数和筛选器驱动程序。 函数和筛选器驱动程序可以调用[**IoGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)来请求**DevicePropertyBusTypeGuid**、 **DevicePropertyLegacyBusType**或**DevicePropertyBusNumber**。 支持多个总线设备的函数和筛选器驱动程序可以使用此信息来确定特定设备所在的总线。

如果总线驱动程序返回信息以响应此 IRP，则会从分页内存中分配**PNP\_总线\_信息**结构。 当不再需要该结构时，PnP 管理器会将其释放。

**PNP\_总线\_信息**结构具有以下格式：

```cpp
typedef struct _PNP_BUS_INFORMATION {
    GUID BusTypeGuid;
    INTERFACE_TYPE LegacyBusType;
    ULONG BusNumber;
} PNP_BUS_INFORMATION, *PPNP_BUS_INFORMATION;
```

结构的成员定义如下：

<a href="" id="bustypeguid"></a>**BusTypeGuid**  
总线驱动程序将**BusTypeGuid**设置为设备所在总线类型的 GUID。 Wdmguid 中列出了标准总线类型的 Guid。 驱动程序编写器应该使用 Uuidgen.exe 为其他总线类型生成 Guid。

<a href="" id="legacybustype"></a>**LegacyBusType**  
PnP 总线驱动程序将**LegacyBusType**设置为父总线[ **\_类型的接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_interface_type)。 接口类型在 Wdm. h 中定义。 某些总线具有特定的**接口\_类型**值，如**PCMCIABus**、 **PCIBus**或**PNPISABus**。 对于其他总线，尤其是较新的总线（如 USB），总线驱动程序将此成员设置为**PNPBus**。

**LegacyBusType**指定用于与设备进行通信的接口。 这不一定对应于父总线的类型。 例如，插入到 PCI CardBus 控制器中的 CardBus 卡的接口为**PCIBus**。 但是，PCI CardBus 控制器上 PCMCIA 卡的接口为**PCMCIABus**。

<a href="" id="busnumber"></a>**BusNumber**  
总线驱动程序将**BusNumber**设置为一个数字，该数字将总线与计算机上相同类型的其他总线区分开来。 总线编号方案是特定于总线的。 总线编号可能是虚拟的，但必须与旧接口（如[**IoReportResourceUsage**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)）使用的任何编号匹配。

请参阅[即插即用](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)，了解用于处理[即插即用次要 irp](plug-and-play-minor-irps.md)的一般规则。

**正在发送此 IRP**

保留供系统使用。 驱动程序不得发送此 IRP。

调用[**IoGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)可获取有关设备所连接到的总线的信息。

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


[**IoGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)

 

 




