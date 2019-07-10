---
title: 1\.0 的 Microsoft 操作系统描述符规范
description: 1\.0 的 Microsoft 操作系统描述符规范
ms.assetid: A2B00584-DDD5-42D2-BDBF-116637ABD192
ms.date: 07/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: ba94eb0baf03f07e3ecc1acdacfdffd984f0abfa
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67717029"
---
# <a name="microsoft-os-10-descriptors-specification"></a>1\.0 的 Microsoft 操作系统描述符规范


USB 设备的设备，其接口和终结点的固件中存储标准描述符。 独立硬件供应商 (Ihv) 还可以存储类和特定于供应商的描述符。 但是，这些描述符可以包含的类型是信息的有限的。 Ihv 通常必须使用 Windows Update 或 CD 之类的介质要为其用户提供的各种特定于设备的信息，如图片、 图标、 自定义驱动程序，等等。

为了帮助 Ihv 解决此问题，Microsoft 还定义了 Microsoft OS 描述符。 Ihv 可以使用这些描述符在固件中存储大部分如今通常单独提供给客户的信息。 了解 Microsoft 操作系统描述符的 Windows 版本使用控制请求检索信息，并使用它来安装和配置设备，而无需任何用户交互。 本白皮书介绍 Microsoft 操作系统描述符，其中讨论了如何存储和检索它们。

**注意：** "扩展兼容 ID 操作系统功能描述符规范"的附录 1 中的兼容和次级兼容 Id 的表是最新的时间，该规范编写的但可能已经发生了变化。 下表包含最新的兼容和次级兼容 Id 列表。 所有 Id 必须都是 8 个字节，因此任何未使用的字符都使用 Null 填充。

<table border="0" cellpadding="0" cellspacing="0" class="grid" width="100%" summary="table">
<thead>
<tr align="left" valign="top">
<td>
<strong>CompatibleID</strong>
</td>
<td>
<strong>次级兼容 ID</strong>
</td>
<td>
<strong>说明</strong>
</td>
</tr>
</thead>
<tbody>
<tr align="left" valign="top">
<td>(0x00 0x00 0x00 0x00 0x00 0x00 0x00 0x00)</td>
<td>(0x00 0x00 0x00 0x00 0x00 0x00 0x00 0x00)</td>
<td>不兼容或次级兼容 ID</td>
</tr>
<tr align="left" valign="top">
<td>"RNDIS"<br>(0x52 0x4E 0x44 0x49 0x53 0x00 0x00 0x00)</td>
<td>(0x00 0x00 0x00 0x00 0x00 0x00 0x00 0x00)</td>
<td>远程网络驱动程序接口标准 (RNDIS)</td>
</tr>
<tr align="left" valign="top">
<td>"PTP"<br>(0x50 0x54 0x50 0x00 0x00 0x00 0x00 0x00)</td>
<td>(0x00 0x00 0x00 0x00 0x00 0x00 0x00 0x00)</td>
<td>图片传输协议 (PTP)</td>
</tr>
<tr align="left" valign="top">
<td>"MTP"<br>(0x4D 0x54 0x50 0x00 0x00 0x00 0x00 0x00)</td>
<td>(0x00 0x00 0x00 0x00 0x00 0x00 0x00 0x00)</td>
<td>媒体传输协议 (MTP)</td>
</tr>
<tr align="left" valign="top">
<td>"XUSB20"<br>(0x58 0x55 0x53 0x42 0x32 0x30 0x00 0x00)</td>
<td>(0x00 0x00 0x00 0x00 0x00 0x00 0x00 0x00)</td>
<td>XNACC (Krypton)</td>
</tr>
<tr align="left" valign="top">
<td>"BLUTUTH"<br>(0x42 0x4C 0x55 0x54 0x55 0x54 0x48 0x00)</td>
<td>
<div class="contentTableWrapper"><table border="0" cellpadding="0" cellspacing="0" class="grid" width="100%" summary="table">
<tbody>
<tr align="left" valign="top">
<td>"11"<br>(0x31 0x31 0x00 0x00 0x00 0x00 0x00 0x00)</td>
<td>符合版本 1.1 和与 Microsoft 驱动程序堆栈兼容的蓝牙无线</td>
</tr>
<tr align="left" valign="top">
<td>"12"<br>(0x31 0x32 0x00 0x00 0x00 0x00 0x00 0x00)</td>
<td>符合版本 1.2 规范且与 Microsoft 驱动程序堆栈兼容的蓝牙无线</td>
</tr>
<tr align="left" valign="top">
<td>"EDR"<br>(0x45 0x44 0x52 0x00 0x00 0x00 0x00 0x00)</td>
<td>符合 2.0 + edr 规范且与 Microsoft 驱动程序堆栈兼容的蓝牙无线</td>
</tr>
</tbody>
</table></div>
<p>
<br>
</p>
</td>
<td>蓝牙</td>
</tr>
<tr align="left" valign="top">
<td>"扫描"<br>(0x53 0x43 0x41 0x4E 0x00 0x00 0x00 0x00)</td>
<td>
<p>设置格式，如下所示：2 个字母组成的供应商代码 + 1-5 ASCII 字符 * + 0x00</p>
<p>\* ASCII 限制为大写字母、 数字、 下划线。</p>
</td>
<td>Scan</td>
</tr>
<tr align="left" valign="top">
<td>"3DPRINT"<br>(0x33 0x44 0x50 0x52 0x49 0x4E 0x54 0x00)</td>
<td>变化不定</td>
<td>MS3DPRINT G 代码 3D 打印机</td>
</tr>
</tbody>
</table>

  

此信息适用于 Windows XP 和更高版本的 Windows。

**请阅读许可协议，然后再继续。**

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td style="text-align: center;"><strong><br />
Microsoft 操作系统描述符规范</strong><br />
</td>
</tr>
<tr class="even">
<td style="text-align: center;"><div style="font-size: 100%; border: thin inset; height: 400px; overflow: scroll; text-align: left; padding: 10px;">
<h3 id="microsoft-os-descriptor-specification-license-agreement">Microsoft 操作系统描述符规范许可协议</h3>
<p>这是您 （任一个人或单个实体） 之间的法律协议 （"协议"） （"您"），和规范的 Microsoft Corporation ("Microsoft")。  下载、 复制或使用本规范，表示你同意遵守本协议的条款。   </p>
<p><strong>第 1 部分定义。</strong></p>
<p>（a）"您的实现"意味着您: (i) 固件和/或实现以便与 Microsoft 操作系统描述符启用操作系统，规范中描述的操作系统描述符集或 Microsoft 授权检索其他系统的硬件和使用此信息;(ii) 软件驱动程序实现的操作系统描述符集规范中描述为仅在与 Windows Vista 或 Windows 7 中的接口的操作系统。</p>
<p>（b）"你方"是指第三方许可您使用您的实现。</p>
<p>（c）"规范"是指 Microsoft 操作系统描述符规范和相关附件资料。</p>
<p><strong>第 2 节授予许可</strong>。</p>
<p>(a)    <strong>版权许可证</strong>。  Microsoft 特此授予您版权声明在规范中，非独占的、 免版税的、 不可转让、 不可转授、 个人全球范围内的许可，以在内部为您的规范的副本和应用在开发您的实现中的承包商使用。</p>
<p>(b)   <strong>专利许可证</strong>。  Microsoft 特此授予您非排他性、 免版税的、 不可转让、 全球范围内下规范中仅包含于 Microsoft 的专利许可证并且拥有或许可由 Microsoft 进行、 使用、 导入、 提供销售、 销售和将直接或间接地分发给您的许可证持有人你实现。  可能会向你的许可接受方相同条款和条件此专利许可权利转授。</p>
<p>(c)    <strong>权利保留</strong>。  Microsoft 保留它可能在其中具有在规范中，其实现和任何知识产权的所有其他权利。  本文档并未授予您或任何其他实体任何许可给任何其他 Microsoft 专利、 商标、 版权或其他知识产权。 </p>
<p><strong>第 3 节其他限制和责任</strong>。</p>
<p>（a） 您的许可证规范的权限取决于你不创建、 修改或分发您获得许可的实现，此类创建、 修改或分发可能采用了 (a) 创建，或声称创建，Microsoft 的义务遵照规范 (或知识产权其中) 或 (b) 授予或 purport，向授予任何第三方的任何权限或 immunities 到 Microsoft 的知识产权或规范中的专有权利。</p>
<p>（b） 在不损害任何其他权利，Microsoft 可能会终止本协议，如果您未遵守本协议的条款。 在这种情况必须销毁规范的所有副本，不得进一步分发公司实现。</p>
<p><strong>第 4 节担保免责声明。</strong></p>
<p>提供规范&quot;原样&quot;无任何形式的保证。 到适用法律允许的最大范围内，Microsoft 进一步拒绝所有担保，包括但不限于任何暗示的适销性或适用于某种特定用途，以及标题和不侵权的担保。 与你保持因使用或执行本规范而产生的全部风险。</p>
<p><strong>第 5 节偶发、 继发排除和其他一些损害赔偿。</strong></p>
<p><strong>适用法律允许的最大范围内，在任何 Microsoft 或其供应商应承担责任的任何后果性损害、 附带性、 直接、 间接、 特殊、 惩罚性或其他损害 （包括但不限于，损失业务利润损失、 业务中断、 业务信息丢失或其他 pecuniary 丢失） 因使用或不能使用规范，即使 Microsoft 已被告知此类损害的可能性。由于某些州/法律辖区不允许排除或限制对后果性损害或意外损害的责任，上述限制可能对您不适用。</strong></p>
<p><strong>第 6 节责任和补偿的限制。</strong></p>
<p><strong>尽管任何损害，则可能会产生因任何原因 （包括但不限制上述损害，所有直接或一般损害），Microsoft 和任何下的任何预配其供应商的全部责任应限制为较大的协议和所有上述规定您因此而获得的实际由你支付的规范或 5.00 美元的金额。即使任何补救措施失败其基本目的，前面提到的限制、 排除和免责声明应适用于适用法律允许的最大范围内。</strong></p>
<p><strong>第 7 节适用法律</strong>。</p>
<p>如果您购买的本规范在美国，本协议受华盛顿州的法律。 有关本协议可能会出现任何争议，您同意的状态和在华盛顿州金县的联邦法院的管辖权。</p>
<p><strong>第 8 节转让。</strong></p>
<p>任何一方不得转让本协议而无需事先书面批准的另一方。</p>
</div>
<p><br />
<a href="http://download.microsoft.com/download/9/C/5/9C5B2167-8017-4BAE-9FDE-D599BAC8184A/OS_Desc_Ext_Prop.zip">我接受，下载</a></p></td>
</tr>
</tbody>
</table>