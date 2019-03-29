---
title: IRP_MN_QUERY_BUS_INFORMATION
description: PnP 管理器使用此 IRP 请求设备的父总线类型和实例数。总线驱动程序应处理此请求为其子设备 (PDOs)。 函数和筛选器驱动程序不处理此 IRP。
ms.date: 08/12/2017
ms.assetid: a7ea1a81-7f03-41c7-8861-a2e1813c15cf
keywords:
- IRP_MN_QUERY_BUS_INFORMATION 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: ecc14699760e5904e484a58d5f7f128f105d7ed9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565165"
---
# <a name="irpmnquerybusinformation"></a>IRP\_MN\_查询\_总线\_信息


PnP 管理器使用此 IRP 请求设备的父总线类型和实例数。

总线驱动程序应处理此请求为其子设备 (PDOs)。 函数和筛选器驱动程序不处理此 IRP。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md) When Sent
---------

PnP 管理器将发送此 IRP，枚举设备时。

PnP 管理器将此 IRP 发送在 IRQL 被动\_级别在任意线程上下文中。

## <a name="input-parameters"></a>输入参数


无

## <a name="output-parameters"></a>输出参数


返回在 I/O 状态块中。

## <a name="io-status-block"></a>I/O 状态块


总线驱动程序设置**Irp-&gt;IoStatus.Status**于状态\_成功或相应的错误状态。

如果成功，总线驱动程序设置**Irp-&gt;IoStatus.Information**为指向已完成[ **PNP\_总线\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff559608)结构。 （请参阅"操作"部分，了解详细信息。）发生错误时，总线驱动程序设置**Irp-&gt;IoStatus.Information**为零。

函数和筛选器驱动程序不处理此 IRP。

<a name="operation"></a>操作
---------

为此 IRP 的响应中返回的信息可供设备在总线上的函数和筛选器驱动程序。 函数和筛选器驱动程序可以调用[ **IoGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff549203)请求**DevicePropertyBusTypeGuid**， **DevicePropertyLegacyBusType**，或**DevicePropertyBusNumber**。 支持多个总线的设备的函数和筛选器驱动程序可以使用此信息来确定特定设备所驻留的总线上。

如果总线驱动程序对此 IRP 响应中返回的信息，它会分配**PNP\_总线\_信息**从分页内存的结构。 当不再需要时，即插即用管理器释放结构。

一个**PNP\_总线\_信息**结构具有以下格式：

```cpp
typedef struct _PNP_BUS_INFORMATION {
    GUID BusTypeGuid;
    INTERFACE_TYPE LegacyBusType;
    ULONG BusNumber;
} PNP_BUS_INFORMATION, *PPNP_BUS_INFORMATION;
```

结构的成员的定义，如下所示：

<a href="" id="bustypeguid"></a>**BusTypeGuid**  
总线驱动程序设置**BusTypeGuid**到设备所驻留的总线类型的 GUID。 Wdmguid.h 中列出的标准的总线类型 Guid。 对于使用 Uuidgen 其他总线类型，驱动程序编写器应生成 Guid。

<a href="" id="legacybustype"></a>**LegacyBusType**  
即插即用总线驱动程序设置**LegacyBusType**到[**接口\_类型**](https://msdn.microsoft.com/library/windows/hardware/ff547839)的父总线。 中 wdm.h 中定义的接口类型。 某些总线具有特定**接口\_类型**值，例如**PCMCIABus**， **PCIBus**，或**PNPISABus**。 对于其他总线，尤其是较新总线喜欢 USB、 总线驱动程序将此成员设置为**PNPBus**。

**LegacyBusType**指定用来与设备通信的接口。 这可能会或可能不对应的父总线类型。 例如，插入到 PCI CardBus 控制器 CardBus 卡的界面是**PCIBus**。 但是，在 PCI CardBus 控制器上的 PCMCIA 卡的界面是**PCMCIABus**。

<a href="" id="busnumber"></a>**BusNumber**  
总线驱动程序设置**BusNumber**为区分总线与相同类型的计算机上其他总线数字。 总线编号方案是总线特定的。 总线编号可能是虚拟的但必须匹配由旧式界面如任何编号[ **IoReportResourceUsage**](https://msdn.microsoft.com/library/windows/hardware/ff549616)。

请参阅[插](https://msdn.microsoft.com/library/windows/hardware/ff547125)处理的常规规则[即插即用次要 Irp](plug-and-play-minor-irps.md)。

**发送此 IRP**

保留供系统使用。 驱动程序必须发送此 IRP。

调用[ **IoGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff549203)以获取有关设备附加到的总线的信息。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wdm.h 中 （包括 wdm.h 中、 Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**IoGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff549203)

 

 




