---
title: 2\.0 的 Microsoft 操作系统描述符规范
description: 2\.0 的 Microsoft 操作系统描述符规范
ms.assetid: C5C5B14A-F39E-4A15-B8BC-615BD11FB630
ms.date: 07/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: db94578187f59bde663d0ebff9b947e29c3c5f2c
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67717025"
---
# <a name="microsoft-os-20-descriptors-specification"></a>2\.0 的 Microsoft 操作系统描述符规范

本文档定义，并描述了版本 2.0 的 Microsoft 操作系统描述符的实现。 Microsoft OS 2.0 描述符旨在解决的限制和可靠性问题的 1.0 版的操作系统描述符，并启用新的 USB 设备的特定于 Windows 的功能。

此信息适用于以下操作系统：

  - Windows 10
  - Windows 8.1 预览版

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
<td style="text-align: center;"><div style="font-size: 100%; border: thin inset; height: 400px; overflow: scroll; text-align: left; padding: 10px; background-color: white;">
<h3 id="microsoft-os-descriptor-specification-license-agreement">Microsoft 操作系统描述符规范许可协议</h3>
<p>这是您 （任一个人或单个实体） 之间的法律协议 （"协议"） （"您"），和规范的 Microsoft Corporation ("Microsoft")。  下载、 复制或使用本规范，表示你同意遵守本协议的条款。   </p>
<p><strong>第 1 部分定义。</strong></p>
<p>（a）"您的实现"意味着您: (i) 固件和/或实现以便与 Microsoft 操作系统描述符启用操作系统，规范中描述的操作系统描述符集或 Microsoft 授权检索其他系统的硬件和使用此信息;(ii) 实现的操作系统描述符集的软件驱动程序与 Windows 8.1 为仅结合接口规范中描述。</p>
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
<a href="http://download.microsoft.com/download/3/5/6/3563ED4A-F318-4B66-A181-AB1D8F6FD42D/MS_OS_2_0_desc.docx">我接受，下载</a></p></td>
</tr>
</tbody>
</table>