---
title: IrpProcessing 规则集 (KMDF)
description: 使用这些规则来验证您的驱动程序正确处理 I/O 请求数据包 (IRP)。
ms.assetid: B403F21E-FE35-4A57-92DB-C78FDC1488BD
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 88d1558914e06d08435645db2d088b4889518cc1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565529"
---
# <a name="irpprocessing-rule-set-kmdf"></a>IrpProcessing 规则集 (KMDF)


使用这些规则来验证您的驱动程序正确处理 I/O 请求数据包 (IRP)。

## <a name="in-this-section"></a>本节内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="kmdf-fwdirptoioqueuevalid.md" data-raw-source="[&lt;strong&gt;FwdIrpToIoQueueValid&lt;/strong&gt;](kmdf-fwdirptoioqueuevalid.md)"><strong>FwdIrpToIoQueueValid</strong></a></p></td>
<td align="left"><p>该规则<a href="kmdf-fwdirptoioqueuevalid.md" data-raw-source="[&lt;strong&gt;FwdIrpToIoQueueValid&lt;/strong&gt;](kmdf-fwdirptoioqueuevalid.md)"> <strong>FwdIrpToIoQueueValid</strong> </a>指定驱动程序将 IRP 发送到一个 I/O 排队，请使用<a href="https://msdn.microsoft.com/library/windows/hardware/hh451105" data-raw-source="[&lt;strong&gt;WdfDeviceWdmDispatchIrpToIoQueue&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451105)"> <strong>WdfDeviceWdmDispatchIrpToIoQueue</strong> </a>方法从<a href="https://msdn.microsoft.com/library/windows/hardware/hh406404" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpDispatch&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406404)"> <em>EvtDeviceWdmIrpDispatch</em> </a>回调或<a href="https://msdn.microsoft.com/library/windows/hardware/ff540925" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540925)"> <em>EvtDeviceWdmIrpPreprocess</em> </a>回调。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-setcompletionroutinefromdispatch.md" data-raw-source="[&lt;strong&gt;SetCompletionRoutineFromDispatch&lt;/strong&gt;](kmdf-setcompletionroutinefromdispatch.md)"><strong>SetCompletionRoutineFromDispatch</strong></a></p></td>
<td align="left"><p><a href="kmdf-setcompletionroutinefromdispatch.md" data-raw-source="[&lt;strong&gt;SetCompletionRoutineFromDispatch&lt;/strong&gt;](kmdf-setcompletionroutinefromdispatch.md)"> <strong>SetCompletionRoutineFromDispatch</strong> </a>规则验证该驱动程序未指定完成例程上从 IRP 其<a href="https://msdn.microsoft.com/library/windows/hardware/hh406404" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpDispatch&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406404)"> <em>EvtDeviceWdmIrpDispatch</em></a>回调函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-miniportonlywdmdevice.md" data-raw-source="[&lt;strong&gt;MiniportOnlyWdmDevice&lt;/strong&gt;](kmdf-miniportonlywdmdevice.md)"><strong>MiniportOnlyWdmDevice</strong></a></p></td>
<td align="left"><p><a href="kmdf-miniportonlywdmdevice.md" data-raw-source="[&lt;strong&gt;MiniportOnlyWdmDevice&lt;/strong&gt;](kmdf-miniportonlywdmdevice.md)"> <strong>MiniportOnlyWdmDevice</strong> </a>规则指定 WDF 驱动程序不应使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff548397" data-raw-source="[&lt;strong&gt;IoCreateDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548397)"> <strong>IoCreateDevice</strong> </a>和<a href="https://msdn.microsoft.com/library/windows/hardware/ff548407" data-raw-source="[&lt;strong&gt;IoCreateDeviceSecure&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548407)"> <strong>IoCreateDeviceSecure</strong> </a>函数来创建裸机 WDM 设备对象。 这将导致计算机崩溃如果有人试图将 IRP 发送到 WDM 设备。 这是因为设备的 IRP 调度条目已设置为特定于 WDF 的条目，但该框架尚未创建 WDF 设备。 但是，微型端口驱动程序可以使用 DDIs，因为驱动程序调度入口点不为其设置。</p></td>
</tr>
</tbody>
</table>

 

**若要选择 IrpProcessing 规则集**

1.  Microsoft Visual Studio 中选择您的驱动程序项目 (.vcxProj)。 从**驱动程序**菜单上，单击**启动 Static Driver Verifier...**.

2.  单击**规则**选项卡。下**规则集**，选择**IrpProcessing**。

    若要选择的默认规则集从 Visual Studio 开发人员命令提示符窗口，请指定**IrpProcessing.sdv**与 **/check**选项。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:IrpProcessing.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅[以找到缺陷驱动程序中使用 Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/hh454281)并[Static Driver Verifier 命令 (MSBuild)](https://msdn.microsoft.com/library/windows/hardware/hh466459)。

 

 





