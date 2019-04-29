---
title: IRP_MJ_SYSTEM_CONTROL
description: 所有驱动程序必须提供处理 IRP_MJ_SYSTEM_CONTROL 请求，由内核模式组件的 Windows Management Instrumentation (WMI) 发送一个 DispatchSystemControl 例程。
ms.date: 08/12/2017
ms.assetid: 1b4dfc87-3f74-4e33-9dbb-72d4f72480fc
keywords:
- IRP_MJ_SYSTEM_CONTROL Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: c0db08fa71ee399d4193e297dab91d51a37ebdaf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368406"
---
# <a name="irpmjsystemcontrol"></a>IRP\_MJ\_SYSTEM\_CONTROL


所有驱动程序必须提供[ *DispatchSystemControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)处理例程**IRP\_MJ\_系统\_控制**请求它发送的内核模式组件[Windows Management Instrumentation](https://msdn.microsoft.com/library/windows/hardware/ff547139) (WMI)。

<a name="when-sent"></a>发送时间
---------

WMI 内核模式组件可以发送**IRP\_MJ\_系统\_控制**请求驱动程序的成功注册后的 WMI 数据供应商作为任何时间。 通常 WMI Irp 会在用户模式下的数据使用者已请求 WMI 数据。

## <a name="input-parameters"></a>输入参数


取决于处的值**MinorFunction**中当前的 I/O 堆栈 IRP 的位置。 每个**IRP\_MJ\_系统\_控制**请求指定了次要函数代码用于标识请求的 WMI 操作。

## <a name="output-parameters"></a>输出参数


取决于处的值**MinorFunction**中当前的 I/O 堆栈 IRP 的位置。

<a name="operation"></a>操作
---------

所有驱动程序必须支持**IRP\_MJ\_系统\_控制**请求通过提供[ *DispatchSystemControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程.

支持的驱动程序[Windows Management Instrumentation](https://msdn.microsoft.com/library/windows/hardware/ff547139) (WMI) 必须处理**IRP\_MJ\_系统\_控制**请求通过处理次要函数与此主要函数代码相关联的代码。 有关 WMI 次要函数代码的信息，请参阅[WMI 次要 Irp](wmi-minor-irps.md)。

不支持通过 WMI 的驱动程序[注册为 WMI 数据提供程序](https://msdn.microsoft.com/library/windows/hardware/ff560870)必须传递**IRP\_MJ\_系统\_控制**到下一个较低的驱动程序的请求。

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


[*DispatchSystemControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

 

 




