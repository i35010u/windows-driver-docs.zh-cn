---
title: IRP_MJ_SYSTEM_CONTROL
description: 所有驱动程序都必须提供一个 DispatchSystemControl 例程来处理 IRP_MJ_SYSTEM_CONTROL 请求，这些请求由 Windows Management Instrumentation （WMI）的内核模式组件发送。
ms.date: 08/12/2017
ms.assetid: 1b4dfc87-3f74-4e33-9dbb-72d4f72480fc
keywords:
- IRP_MJ_SYSTEM_CONTROL 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 711a11b7494461bb5c290321e0622b3ea88443e4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828102"
---
# <a name="irp_mj_system_control"></a>IRP\_MJ\_SYSTEM\_CONTROL


所有驱动程序都必须提供[*DispatchSystemControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程来处理**IRP\_MJ\_系统\_控制**请求，这些请求由[Windows Management Instrumentation](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-wmi) （WMI）的内核模式组件发送。

<a name="when-sent"></a>发送时间
---------

每当驱动程序成功注册为 WMI 数据的供应商时，WMI 内核模式组件都可以将**IRP\_MJ\_SYSTEM\_控制**请求随时发送到该请求。 通常在用户模式数据使用者请求 WMI 数据时发送 WMI Irp。

## <a name="input-parameters"></a>输入参数


依赖于 IRP 当前 i/o 堆栈位置中**MinorFunction**处的值。 每个**IRP\_MJ\_SYSTEM\_控制**请求指定用于标识所请求的 WMI 操作的次要函数代码。

## <a name="output-parameters"></a>输出参数


依赖于 IRP 当前 i/o 堆栈位置中**MinorFunction**处的值。

<a name="operation"></a>操作
---------

所有驱动程序都必须通过提供[*DispatchSystemControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程来支持**IRP\_MJ\_系统\_控制**请求。

支持[Windows Management Instrumentation](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-wmi) （WMI）的驱动程序必须通过处理与此主要函数代码关联的次要函数代码来处理**IRP\_MJ\_系统\_控制**请求。 有关 WMI 次要函数代码的信息，请参阅[Wmi 次要 irp](wmi-minor-irps.md)。

通过[注册为 wmi 数据提供程序](https://docs.microsoft.com/windows-hardware/drivers/kernel/registering-as-a-wmi-data-provider)而不支持 WMI 的驱动程序必须将**IRP\_MJ\_系统\_控制**请求传递到下一个较低的驱动程序。

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


[*DispatchSystemControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

 

 




