---
title: IRP_MN_QUERY_BUS_INFORMATION
description: PnP 管理器使用此 IRP 来请求设备的父总线的类型和实例编号。总线驱动程序应为 (PDOs) 的子设备处理此请求。 函数和筛选器驱动程序不处理此 IRP。
ms.date: 08/12/2017
ms.assetid: a7ea1a81-7f03-41c7-8861-a2e1813c15cf
keywords:
- IRP_MN_QUERY_BUS_INFORMATION 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 9673449116dcd3a076e283fc20e3d2002d246306
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90106750"
---
# <a name="irp_mn_query_bus_information"></a>IRP \_ MN \_ 查询 \_ 总线 \_ 信息


PnP 管理器使用此 IRP 来请求设备的父总线的类型和实例编号。

总线驱动程序应为 (PDOs) 的子设备处理此请求。 函数和筛选器驱动程序不处理此 IRP。

## <a name="value"></a>值

0x15

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


总线驱动程序将 **Irp- &gt; IoStatus** 设置为 " \_ 成功" 或相应的 "错误" 状态。

成功时，总线驱动程序会将 **Irp &gt; IoStatus** 设置为指向已完成的 [**PNP \_ 总线 \_ 信息**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_pnp_bus_information) 结构的指针。  (参阅 "操作" 部分，了解详细信息。 ) 出错时，总线驱动程序将 ** &gt; IoStatus** 设置为零。

函数和筛选器驱动程序不处理此 IRP。

<a name="operation"></a>操作
---------

为响应此 IRP 而返回的信息可用于总线上设备的函数和筛选器驱动程序。 函数和筛选器驱动程序可以调用 [**IoGetDeviceProperty**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty) 来请求 **DevicePropertyBusTypeGuid**、 **DevicePropertyLegacyBusType**或 **DevicePropertyBusNumber**。 支持多个总线设备的函数和筛选器驱动程序可以使用此信息来确定特定设备所在的总线。

如果总线驱动程序返回信息以响应此 IRP，则会从分页内存中分配 **PNP \_ 总线 \_ 信息** 结构。 当不再需要该结构时，PnP 管理器会将其释放。

**PNP \_ 总线 \_ 信息**结构具有以下格式：

```cpp
typedef struct _PNP_BUS_INFORMATION {
    GUID BusTypeGuid;
    INTERFACE_TYPE LegacyBusType;
    ULONG BusNumber;
} PNP_BUS_INFORMATION, *PPNP_BUS_INFORMATION;
```

结构的成员定义如下：

<a href="" id="bustypeguid"></a>**BusTypeGuid**  
总线驱动程序将 **BusTypeGuid** 设置为设备所在总线类型的 GUID。 Wdmguid 中列出了标准总线类型的 Guid。 驱动程序编写器应该使用 Uuidgen.exe 为其他总线类型生成 Guid。

<a href="" id="legacybustype"></a>**LegacyBusType**  
PnP 总线驱动程序将 **LegacyBusType** 设置为父总线的 [**接口 \_ 类型**](/windows-hardware/drivers/ddi/wdm/ne-wdm-_interface_type) 。 接口类型在 Wdm. h 中定义。 某些总线具有特定的 **接口 \_ 类型** 值，如 **PCMCIABus**、 **PCIBus**或 **PNPISABus**。 对于其他总线，尤其是较新的总线（如 USB），总线驱动程序将此成员设置为 **PNPBus**。

**LegacyBusType**指定用于与设备进行通信的接口。 这不一定对应于父总线的类型。 例如，插入到 PCI CardBus 控制器中的 CardBus 卡的接口为 **PCIBus**。 但是，PCI CardBus 控制器上 PCMCIA 卡的接口为 **PCMCIABus**。

<a href="" id="busnumber"></a>**BusNumber**  
总线驱动程序将 **BusNumber** 设置为一个数字，该数字将总线与计算机上相同类型的其他总线区分开来。 总线编号方案是特定于总线的。 总线编号可能是虚拟的，但必须与旧接口（如 [**IoReportResourceUsage**](./mmcreatemdl.md)）使用的任何编号匹配。

请参阅 [即插即用](./introduction-to-plug-and-play.md) ，了解用于处理 [即插即用次要 irp](plug-and-play-minor-irps.md)的一般规则。

**正在发送此 IRP**

预留给系统使用。 驱动程序不得发送此 IRP。

调用 [**IoGetDeviceProperty**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty) 可获取有关设备所连接到的总线的信息。

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


[**IoGetDeviceProperty**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)

 

