---
title: Irql 规则集 (KMDF)
description: 使用这些规则验证你的驱动程序是否在所需的 IRQL 上进行 DDI 调用。不遵循 IRQL 规则的驱动程序可能会导致在操作过程中出现严重问题，从而导致死锁情况或计算机崩溃。
ms.assetid: B02D196F-E8D5-4FE9-8983-AD08EAE00DE5
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4507e1dcccb97e3902fc2108c7c73964cd81e9e5
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90105402"
---
# <a name="irql-rule-set-kmdf"></a>Irql 规则集 (KMDF)


使用这些规则验证你的驱动程序是否在所需的 IRQL 上进行 DDI 调用。

不遵循 IRQL 规则的驱动程序可能会导致在操作过程中出现严重问题，从而导致死锁情况或计算机崩溃。

## <a name="in-this-section"></a>在本节中


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="kmdf-kmdfirql.md" data-raw-source="[&lt;strong&gt;KmdfIrql&lt;/strong&gt;](kmdf-kmdfirql.md)"><strong>KmdfIrql</strong></a></p></td>
<td align="left"><p><a href="kmdf-kmdfirql.md" data-raw-source="[&lt;strong&gt;KmdfIrql&lt;/strong&gt;](kmdf-kmdfirql.md)"><strong>KmdfIrql</strong></a>规则指定驱动程序以小于或等于该方法的最大 IRQL 的 irql 调用框架方法。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-kmdfirql2.md" data-raw-source="[&lt;strong&gt;KmdfIrql2&lt;/strong&gt;](kmdf-kmdfirql2.md)"><strong>KmdfIrql2</strong></a></p></td>
<td align="left"><p><a href="kmdf-kmdfirql2.md" data-raw-source="[&lt;strong&gt;KmdfIrql2&lt;/strong&gt;](kmdf-kmdfirql2.md)"><strong>KmdfIrql2</strong></a>规则指定驱动程序以小于或等于该方法的最大 IRQL 的 irql 调用框架方法。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-usbkmdfirql.md" data-raw-source="[&lt;strong&gt;UsbKmdfIrql&lt;/strong&gt;](kmdf-usbkmdfirql.md)"><strong>UsbKmdfIrql</strong></a></p></td>
<td align="left"><p><a href="kmdf-usbkmdfirql.md" data-raw-source="[&lt;strong&gt;UsbKmdfIrql&lt;/strong&gt;](kmdf-usbkmdfirql.md)"><strong>UsbKmdfIrql</strong></a>规则指定 KMDF 驱动程序不会在错误的 IRQL 级别 (DDI) 中调用特定于 USB 的设备驱动程序接口。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-usbkmdfirql2.md" data-raw-source="[&lt;strong&gt;UsbKmdfIrql2&lt;/strong&gt;](kmdf-usbkmdfirql2.md)"><strong>UsbKmdfIrql2</strong></a></p></td>
<td align="left"><p><a href="kmdf-usbkmdfirql2.md" data-raw-source="[&lt;strong&gt;UsbKmdfIrql2&lt;/strong&gt;](kmdf-usbkmdfirql2.md)"><strong>UsbKmdfIrql2</strong></a>规则指定 KMDF 驱动程序不应在错误的 IRQL 级别调用特定于 USB 的 DDIs。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="usbkmdfirqlexplicit.md" data-raw-source="[&lt;strong&gt;UsbKmdfIrqlExplicit&lt;/strong&gt;](usbkmdfirqlexplicit.md)"><strong>UsbKmdfIrqlExplicit</strong></a></p></td>
<td align="left"><p><a href="usbkmdfirqlexplicit.md" data-raw-source="[&lt;strong&gt;UsbKmdfIrqlExplicit&lt;/strong&gt;](usbkmdfirqlexplicit.md)"><strong>UsbKmdfIrqlExplicit</strong></a>规则验证是否在正确的 IRQL 级别调用 KMDF DDIs。 此规则适用于所有 EvtIoCallback 函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdfrequestsendsyncatdispatch.md" data-raw-source="[&lt;strong&gt;WdfRequestSendSyncAtDispatch&lt;/strong&gt;](wdfrequestsendsyncatdispatch.md)"><strong>WdfRequestSendSyncAtDispatch</strong></a></p></td>
<td align="left"><p><a href="wdfrequestsendsyncatdispatch.md" data-raw-source="[&lt;strong&gt;WdfRequestSendSyncAtDispatch&lt;/strong&gt;](wdfrequestsendsyncatdispatch.md)"><strong>WdfRequestSendSyncAtDispatch</strong></a>规则验证<a href="/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend" data-raw-source="[&lt;strong&gt;WdfRequestSend&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)"><strong>WdfRequestSend</strong></a>函数是否以正确的 IRQL 优先级别发送。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdfrequestsendsyncatdispatch2.md" data-raw-source="[&lt;strong&gt;WdfRequestSendSyncAtDispatch2&lt;/strong&gt;](wdfrequestsendsyncatdispatch2.md)"><strong>WdfRequestSendSyncAtDispatch2</strong></a></p></td>
<td align="left"><p><a href="wdfrequestsendsyncatdispatch2.md" data-raw-source="[&lt;strong&gt;WdfRequestSendSyncAtDispatch2&lt;/strong&gt;](wdfrequestsendsyncatdispatch2.md)"><strong>WdfRequestSendSyncAtDispatch2</strong></a>规则验证<a href="/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend" data-raw-source="[&lt;strong&gt;WdfRequestSend&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)"><strong>WdfRequestSend</strong></a>函数是否以正确的 IRQL 优先级别发送。</p></td>
</tr>
</tbody>
</table>

 

**选择 Irql 规则集**

1.  选择你的驱动程序项目 () 在 Microsoft Visual Studio 中。 在 " **驱动程序** " 菜单中，单击 " **启动静态驱动程序验证程序 ...**"。

2.  单击 " **规则** " 选项卡。在 " **规则集**" 下，选择 **Irql**。

    若要从 Visual Studio 开发人员命令提示符窗口中选择默认规则集，请将 **sdv** 与 **/check** 选项一起指定。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:Irql.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅 [使用静态驱动程序验证器查找驱动程序中的缺陷](./using-static-driver-verifier-to-find-defects-in-drivers.md) 和 [静态驱动程序验证程序命令 (MSBuild) ](./-static-driver-verifier-commands--msbuild-.md)。

