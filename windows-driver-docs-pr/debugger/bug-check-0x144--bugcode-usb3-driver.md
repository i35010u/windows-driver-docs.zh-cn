---
title: Bug 检查 0x144 BUGCODE_USB3_DRIVER
description: BUGCODE_USB3_DRIVER bug 检查具有 0x00000144 值。 这是所使用的所有 USB 3 bug 检查代码。
ms.assetid: 39414287-3E20-405B-846A-B7F9F8AEE078
keywords:
- Bug 检查 0x144 BUGCODE_USB3_DRIVER
- BUGCODE_USB3_DRIVER
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- BUGCODE_USB3_DRIVER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d6f7fd5c66c5a0b02bea1e8b1b3355e544f6c5f1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533717"
---
# <a name="bug-check-0x144-bugcodeusb3driver"></a>Bug 检查 0x144:BUGCODE\_USB3\_DRIVER


**BUGCODE\_USB3\_驱动程序**bug 检查的值为 0x00000144。 这是所使用的所有 USB 3 bug 检查代码。 参数 1 指定 USB 3 检查错误，类型和其他参数的含义都依赖于参数 1。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="bugcodeusb3driver-parameters"></a>BUGCODE\_USB3\_驱动程序参数


<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 1</th>
<th align="left">参数 2</th>
<th align="left">参数 3</th>
<th align="left">参数 4</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>可选。 指向用于重新发送 URB IRP</p></td>
<td align="left"><p>指向 URB</p></td>
<td align="left"><p>指向客户端驱动程序&#39;s 设备对象</p></td>
<td align="left"><p>客户端驱动程序使用它以前发送到 core 堆栈 URB。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>指向启动设备的物理设备对象 (PDO)</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>启动映像或分页设备未能重新枚举。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3</p></td>
<td align="left"><p>可选。 指向用于发送 URB IRP</p></td>
<td align="left"><p>指向已损坏 URB</p></td>
<td align="left"><p>指向客户端驱动程序&#39;s 设备对象</p></td>
<td align="left"><p>客户端驱动程序发送到 core 堆栈损坏的 URB。 因为客户端驱动程序没有分配 URB 使用发生这种情况<strong>USBD_<em>xxx</em>UrbAllocate</strong>或因为客户端驱动程序缓冲区不足 URB。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x800</p></td>
<td align="left"><p>打开的静态流请求已发送的 IRQL</p></td>
<td align="left"><p>指向打开的静态流 IRP</p></td>
<td align="left"><p>指向客户端驱动程序&#39;s 设备对象</p></td>
<td align="left"><p>打开的静态流请求已发送在 IRQL&gt;被动级别。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x801</p></td>
<td align="left"><p>指向打开的静态流 IRP</p></td>
<td align="left"><p>指向打开的静态流 URB</p></td>
<td align="left"><p>指向客户端驱动程序&#39;s 设备对象</p></td>
<td align="left"><p>客户端驱动程序尝试打开的流功能在查询之前静态流。 客户端驱动程序不能打开直到静态流后它已成功查询流功能。 有关详细信息，请参阅备注。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x802</p></td>
<td align="left"><p>静态客户端驱动程序尝试打开的流数</p></td>
<td align="left"><p>已向客户端驱动程序授予的静态流数</p></td>
<td align="left"><p>指向客户端驱动程序&#39;s 设备对象</p></td>
<td align="left"><p>客户端驱动程序尝试打开的静态流数无效。 流的数量不能为 0，不能大于为 USB 功能调用的查询中的客户端驱动程序返回的值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x803</p></td>
<td align="left"><p>指向打开的静态流 IRP</p></td>
<td align="left"><p>指向打开的静态流 URB</p></td>
<td align="left"><p>指向客户端驱动程序&#39;s 设备对象</p></td>
<td align="left"><p>客户端驱动程序尝试打开已打开的静态流的终结点的静态流。 在打开之前静态流，客户端驱动程序必须关闭以前打开的静态流。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x804</p></td>
<td align="left"><p>泄漏的句柄上下文中。 运行<strong>！ usbanalyze v</strong>以获取有关已泄漏的句柄和 URBs 的信息。 为客户端驱动程序，必须启用驱动程序验证程序。</p></td>
<td align="left"><p>设备对象传递给 <strong><a href="https://msdn.microsoft.com/library/windows/hardware/hh406241" data-raw-source="[USBD_CreateHandle](https://msdn.microsoft.com/library/windows/hardware/hh406241)">USBD_CreateHandle</a></strong>。</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>客户端驱动程序忘记关闭之前使用它创建的句柄<strong><a href="https://msdn.microsoft.com/library/windows/hardware/hh406241" data-raw-source="[USBD_CreateHandle](https://msdn.microsoft.com/library/windows/hardware/hh406241)">USBD_CreateHandle</a></strong>或忘记释放它分配 URB。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x805</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542962" data-raw-source="[WDFREQUEST](https://msdn.microsoft.com/library/windows/hardware/ff542962)">WDFREQUEST</a>句柄关闭静态流 URB</p></td>
<td align="left"><p>指向关闭静态流 URB</p></td>
<td align="left"><p>指向客户端驱动程序&#39;s 设备对象</p></td>
<td align="left"><p>客户端驱动程序 （例如，在处理之后 D0 退出） 关闭的静态流 URB 发送处于无效状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x806</p></td>
<td align="left"><p>指向 IRP</p></td>
<td align="left"><p>指向 URB</p></td>
<td align="left"><p>指向客户端驱动程序&#39;s 设备对象</p></td>
<td align="left"><p>客户端驱动程序试图发送连锁<strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff554414" data-raw-source="[MDL](https://msdn.microsoft.com/library/windows/hardware/ff554414)">MDL</a></strong>查询链接在一起的之前<strong>MDL</strong>功能。 客户端驱动程序无法发送其链式<strong>MDL</strong>直到之后它已成功查询的连锁<strong>MDL</strong>功能。 有关详细信息，请参阅备注。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x807</p></td>
<td align="left"><p>指向连锁 <strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff554414" data-raw-source="[MDL](https://msdn.microsoft.com/library/windows/hardware/ff554414)">MDL</a></strong></p></td>
<td align="left"><p>指向 URB</p></td>
<td align="left"><p>指向客户端驱动程序&#39;s 设备对象，如果可用</p></td>
<td align="left"><p>客户端驱动程序发送 URB core 堆栈使用传输到缓冲区长度超过字节数 (由 <strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff554530" data-raw-source="[MmGetMdlByteCount](https://msdn.microsoft.com/library/windows/hardware/ff554530)">MmGetMdlByteCount</a></strong>) 的 <strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff554414" data-raw-source="[MDL](https://msdn.microsoft.com/library/windows/hardware/ff554414)">MDL</a></strong>中传递。 有关详细信息，请参阅备注。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1001</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>XHCI 控制器添加 HSE 位，这表示主机系统错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1002</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>XHCI 控制器添加 HCE 位，指示主机控制器错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1003</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>XHCI 停止终结点命令返回了未处理的完成代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1004</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>XHCI 终结点状态后颁发的 xHCI 终结点停止命令接收上下文状态错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1005</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>设置取消排队失败期间尝试清除停滞控制终结点上的指针。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1006</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>重置 EP 尝试清除控制终结点上的停止期间失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1007</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>重置的过程中失败的 xHCI 控制器重置恢复。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1008</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>重新启动过程中失败 xHCI 控制器重置恢复。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1009</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>XHCI 控制器命令无法完成后的命令超时中止。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x100A</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>设置取消排队失败期间尝试设置终结点停止完成后，取消排队指针的指针。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x100B</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>停止过程中失败的 xHCI 控制器重置恢复。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x100C</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>不支持在 xHCI 控制器的固件。 在此控制器上不会加载 xHCI 驱动程序，除非更新固件。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x100D</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>控制器检测到要以物理方式删除。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x100E</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>驱动程序检测到已启用的流终结点上的错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x100F</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>中的 xHCI 控制器的固件已过时。 XHCI 驱动程序将继续使用此控制器，但可能会遇到一些问题。 建议的固件更新。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1010</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>传输事件 TRB 完成，但未处理的完成代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1011</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>在控制器报告事件环已满。 控制器也称为要删除事件时出现这种情况。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1012</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>控制器已完成无序的命令。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1013</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>命令中止完成后，取消排队的命令环指针由控制器报告不正确。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1014</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>完成操作后启用槽，控制器为我们提供错误的槽 id。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1015</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>控制器无法与 BSR1 SetAddress 命令。 这是意外。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1016</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>控制器未能 usbdevice 重置期间启用一个槽。 这是意外。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1017</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>控制器失败终结点配置的命令，我们已在其中 deconfiguring 终结点。 这是意外。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1018</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>控制器无法禁用槽命令。 这是意外。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1019</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>控制器失败 USB 设备重置命令。 这是意外。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x101A</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>终结点重置后，将取消排队的指针的命令失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x101B</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>XHCI 重置终结点命令返回了一个未处理的完成代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x101C</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>对于 xHCI D0Entry 失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x101D</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>暂时删除和添加流终结点 （如两个命令） 时在请求取消过程而不设置取消排队的指针使用配置的终结点命令失败。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x101E</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>在控制器指示未挂起的传输完成在控制器上。 EventData = = 1 (取消引用传输事件 TRB&#39;s 指针可能会造成错误检查)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x101F</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>在控制器指示未挂起的传输完成在控制器上。 EventData = = 0 （在传输事件 TRB 不匹配的逻辑地址）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1020</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>在控制器指示未挂起的传输完成在控制器上。 EventData = = 0 （在传输事件 TRB 不匹配的逻辑地址） 传输事件 TRB 可能是冗余 （点几乎最近已完成的请求）。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1021</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>暂时删除和添加流终结点 （作为两个命令） 失败，使用配置的终结点命令重置时不会暂停的终结点的一部分时。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1022</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>删除和添加相同的终结点 （作为一个命令中） 失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3000</p></td>
<td align="left"><p>USBHUB3_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>表现不正常的中心已成功重置中心驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3001</p></td>
<td align="left"><p>USBHUB3_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>表现不正常的中心无法成功重置中心驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3002</p></td>
<td align="left"><p>USBHUB3_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>中心驱动程序被禁用的非函数 SuperSpeed 集线器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3003</p></td>
<td align="left"><p>USBHUB3_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>USB 设备未能枚举。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

若要查询 USB 功能，客户端驱动程序必须调用[ **WdfUsbTargetDeviceQueryUsbCapability** ](https://msdn.microsoft.com/library/windows/hardware/hh439434)或[ **USBD\_QueryUsbCapability**](https://msdn.microsoft.com/library/windows/hardware/hh406230)

若要发送链接[ **MDL**](https://msdn.microsoft.com/library/windows/hardware/ff554414)，客户端驱动程序必须调用[ **USBD\_QueryUsbCapability** ](https://msdn.microsoft.com/library/windows/hardware/hh406230) ，并使用**URB\_函数\_大容量\_OR\_中断\_传输\_USING\_CHAINED\_MDL**或**URB\_函数\_ISOCH\_传输\_USING\_CHAINED\_MDL**。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[通用串行总线 (USB)](https://msdn.microsoft.com/library/windows/hardware/ff538930)

 

 




