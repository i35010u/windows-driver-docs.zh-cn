---
title: IRP_MJ_SYSTEM_CONTROL
description: 所有驱动程序都必须提供一个 DispatchSystemControl 例程来处理 IRP_MJ_SYSTEM_CONTROL 请求，这些请求由 Windows Management Instrumentation (WMI) 的内核模式组件发送。
ms.date: 08/12/2017
ms.assetid: 1b4dfc87-3f74-4e33-9dbb-72d4f72480fc
keywords:
- IRP_MJ_SYSTEM_CONTROL 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 0216486538751d367dcae3aa92f837230de25ec4
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188247"
---
# <a name="irp_mj_system_control"></a>IRP\_MJ\_SYSTEM\_CONTROL


所有驱动程序都必须提供一个 [*DispatchSystemControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程来处理 **IRP \_ MJ \_ 系统 \_ 控制** 请求，这些请求由 [Windows Management Instrumentation](./implementing-wmi.md) (WMI) 的内核模式组件发送。

<a name="when-sent"></a>发送时间
---------

一旦驱动程序成功注册为 WMI 数据的提供程序，WMI 内核模式组件就可以随时发送 **IRP \_ MJ \_ 系统 \_ 控制** 请求。 通常在用户模式数据使用者请求 WMI 数据时发送 WMI Irp。

## <a name="input-parameters"></a>输入参数


依赖于 IRP 当前 i/o 堆栈位置中 **MinorFunction** 处的值。 每个 **IRP \_ MJ \_ 系统 \_ 控制** 请求指定一个用于标识所请求的 WMI 操作的次要函数代码。

## <a name="output-parameters"></a>输出参数


依赖于 IRP 当前 i/o 堆栈位置中 **MinorFunction** 处的值。

<a name="operation"></a>操作
---------

所有驱动程序都必须通过提供[*DispatchSystemControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程来支持**IRP \_ MJ \_ 系统 \_ 控制**请求。

支持 [Windows Management Instrumentation](./implementing-wmi.md) (WMI) 的驱动程序必须通过处理与此主要函数代码关联的次要函数代码来处理 **IRP \_ MJ \_ 系统 \_ 控制** 请求。 有关 WMI 次要函数代码的信息，请参阅 [Wmi 次要 irp](wmi-minor-irps.md)。

通过 [注册为 wmi 数据提供程序](./registering-as-a-wmi-data-provider.md) 不支持 WMI 的驱动程序必须将 **IRP \_ MJ \_ 系统 \_ 控制** 请求传递到下一个较低版本的驱动程序。

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
<td>Wdm.h（包括 Wdm.h、Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[*DispatchSystemControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

 

