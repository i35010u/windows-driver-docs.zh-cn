---
title: IRP_MN_EJECT
description: 总线驱动程序通常处理此请求适用于支持设备弹出及其子设备 (子 PDOs)。 函数和筛选器驱动程序不会收到此请求。
ms.date: 08/12/2017
ms.assetid: 2807eeca-c614-469a-baeb-3d2d65416c57
keywords:
- IRP_MN_EJECT Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: 5efa871e04633f18ed23358146458d3fc4228089
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524064"
---
# <a name="irpmneject"></a>IRP\_MN\_EJECT


总线驱动程序通常处理此请求适用于支持设备弹出及其子设备 (子 PDOs)。 函数和筛选器驱动程序不会收到此请求。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md) When Sent
---------

PnP 管理器将发送此 IRP，若要指示相应的驱动程序或驱动程序，以弹出该设备时从其槽。

PnP 管理器将此 IRP 发送在 IRQL 被动\_级别在任意线程上下文中。

## <a name="input-parameters"></a>输入参数


无

## <a name="output-parameters"></a>输出参数


无

## <a name="io-status-block"></a>I/O 状态块


总线驱动程序设置**Irp-&gt;IoStatus.Status**于状态\_成功或相应的错误状态。

如果成功，总线驱动程序设置**Irp-&gt;IoStatus.Information**为零。

如果总线驱动程序不处理此 IRP，则将保留**Irp-&gt;IoStatus.Status**完成 IRP 和时。

<a name="operation"></a>操作
---------

对于要弹出的设备，设备必须在 D3 设备电源状态 （关闭） 并且 （如果设备支持锁定），必须锁定。

成功返回，对于此 IRP 任何驱动程序必须等待，直到完成 IRP 之前弹出该设备。

请参阅[插](https://msdn.microsoft.com/library/windows/hardware/ff547125)处理的常规规则[即插即用次要 Irp](plug-and-play-minor-irps.md)。

**发送此 IRP**

保留供系统使用。 驱动程序必须发送此 IRP。

相反，请参阅的参考页[ **IoRequestDeviceEject** ](https://msdn.microsoft.com/library/windows/hardware/ff549647)例程。

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


[**IoRequestDeviceEject**](https://msdn.microsoft.com/library/windows/hardware/ff549647)

 

 




