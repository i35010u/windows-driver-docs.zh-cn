---
title: Bug 检查 0xF1 SCSI_VERIFIER_DETECTED_VIOLATION
description: SCSI_VERIFIER_DETECTED_VIOLATION bug 检查具有 0x000000F1 值。 这是 bug 检查代码的所有驱动程序验证工具 SCSI 验证冲突。
ms.assetid: babc33f9-a467-4b19-b1a2-1898d0224d4d
keywords:
- Bug 检查 0xF1 SCSI_VERIFIER_DETECTED_VIOLATION
- SCSI_VERIFIER_DETECTED_VIOLATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- SCSI_VERIFIER_DETECTED_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 753d8e9a91414b9df2ab136ed81b8d4487748941
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238662"
---
# <a name="bug-check-0xf1-scsiverifierdetectedviolation"></a>Bug 检查 0xF1：SCSI\_VERIFIER\_检测到\_冲突


SCSI\_VERIFIER\_检测到\_冲突错误检查的值为 0x000000F1。 这是所有驱动程序验证程序的 bug 检查代码**SCSI 验证**冲突。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="scsiverifierdetectedviolation-parameters"></a>SCSI\_VERIFIER\_检测到\_冲突参数


参数 1 标识冲突的类型。

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
<td align="left"><p>0x1000</p></td>
<td align="left"><p>第一个参数传递</p></td>
<td align="left"><p>第二个参数传递</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>微型端口驱动程序传递到参数错误<strong>ScsiPortInitialize</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1001</p></td>
<td align="left"><p>延迟，以微秒为单位</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>微型端口驱动程序调用<strong>ScsiPortStallExecution</strong>和指定的延迟大于 0.1 秒，停止太长处理器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1002</p></td>
<td align="left"><p>花费了太长时间的例程的地址</p></td>
<td align="left"><p>微型端口的 HW_DEVICE_EXTENSION 地址</p></td>
<td align="left"><p>例程，以微秒为单位的持续时间</p></td>
<td align="left"><p>由端口驱动程序调用的微型端口例程花的时间超过 0.5 秒的时间来执行。</p>
<p>（0.5 秒是大部分例程的限制。 但是， <strong>HwInitialize</strong>例程允许 5 秒，并且<strong>FindAdapter</strong>例程不受限制。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1003</p></td>
<td align="left"><p>微型端口的 HW_DEVICE_EXTENSION 地址</p></td>
<td align="left"><p>SRB 的地址</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>微型端口驱动程序不止一次完成一个请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1004</p></td>
<td align="left"><p>SRB 的地址</p></td>
<td align="left"><p>微型端口的 HW_DEVICE_EXTENSION 地址</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>微型端口驱动程序完成无效的 SRB 状态的请求。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1005</p></td>
<td align="left"><p>微型端口的 HW_DEVICE_EXTENSION 地址</p></td>
<td align="left"><p>LOGICAL_UNIT_EXTENSION 的地址</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>微型端口驱动程序调用<strong>ScsiPortNotification</strong>寻求<strong>NextLuRequest</strong>，但未标记的请求仍处于活动状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1006</p></td>
<td align="left"><p>微型端口的 HW_DEVICE_EXTENSION 地址</p></td>
<td align="left"><p>虚拟地址无效</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>微型端口驱动程序传递到的虚拟地址无效<strong>ScsiPortGetPhysicalAddress</strong>。</p>
<p>（这通常意味着提供的地址不会映射到常见的缓冲区区域。）</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1007</p></td>
<td align="left"><p>ADAPTER_EXTENSION 的地址</p></td>
<td align="left"><p>微型端口的 HW_DEVICE_EXTENSION 地址</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>重置保存期结束，总线但微型端口驱动程序仍有未完成的请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2001</p></td>
<td align="left"><p>延迟，以微秒为单位</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>Storport 微型端口驱动程序调用<strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff567508" data-raw-source="[StorPortStallExecution](https://msdn.microsoft.com/library/windows/hardware/ff567508)">StorPortStallExecution</a></strong>和指定的延迟超过 0.1 秒，拖延症的处理器的时间过多的时间。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2002</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p><strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff567103" data-raw-source="[StorPortGetUncachedExtension](https://msdn.microsoft.com/library/windows/hardware/ff567103)">StorPortGetUncachedExtension</a></strong> 从微型端口驱动程序未调用<strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff557390" data-raw-source="[HwStorFindAdapter](https://msdn.microsoft.com/library/windows/hardware/ff557390)">HwStorFindAdapter</a></strong>例程。 <strong>StorPortGetUncachedExtension</strong>仅从微型端口驱动程序调用例程<strong>HwStorFindAdapter</strong>例程和仅为主机总线适配器。 Storport 微型端口驱动程序必须设置<strong>SrbExtensionSize</strong>的<strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff557459" data-raw-source="[HW_INITIALIZATION_DATA](https://msdn.microsoft.com/library/windows/hardware/ff557459)">HW_INITIALIZATION_DATA</a></strong> (Storport) 结构，然后才能调用<strong>StorPortGetUncachedExtension</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2003</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>无效的地址传递给<strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff567080" data-raw-source="[StorPortGetDeviceBase](https://msdn.microsoft.com/library/windows/hardware/ff567080)">StorPortGetDeviceBase</a></strong>例程。 <strong>StorPortGetDeviceBase</strong>例程支持分配给驱动程序的系统插即用 (PnP) 管理器的地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2004</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>Storport 微型端口驱动程序完成相同的 I/O 请求超过一次。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2005</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>Storport 微型端口驱动程序的其中一个传递了无效的虚拟地址<strong>StorPortRead</strong><em>xxx</em>或<strong>StorPortWrite</strong><em>xxx</em>例程。 这通常意味着提供的地址不会映射到常见的缓冲区区域。 指定<em>注册</em>或<em>端口</em>必须在映射的内存空间范围内返回<strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff567080" data-raw-source="[StorPortGetDeviceBase](https://msdn.microsoft.com/library/windows/hardware/ff567080)">StorPortGetDeviceBase</a></strong>例程。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

请参阅每个代码的原因的说明的 Parameters 节中的说明。

<a name="resolution"></a>分辨率
----------

当驱动程序验证程序已指示，若要监视一个或多个驱动程序时，才会发生此错误检查。 如果您不打算使用驱动程序验证程序，应停用它。 您可以考虑删除该驱动程序导致此问题。

如果你是驱动程序编写器，使用通过此 bug 检查获取的信息以在代码中修复的错误。

Driver Verifier **SCSI 验证**选项是仅适用于 Windows XP 及更高版本。 Driver Verifier **Storport 验证**选项是仅适用于 Windows 7 及更高版本。 有关驱动程序验证程序的完整详细信息，请参阅 Windows 驱动程序工具包。

 

 




