---
title: Microsoft OS 1.0 描述符规范
description: Microsoft OS 1.0 描述符规范
ms.assetid: A2B00584-DDD5-42D2-BDBF-116637ABD192
ms.date: 07/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 40f398f445d0b90f24347b36735cffd7603138e7
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210625"
---
# <a name="microsoft-os-10-descriptors-specification"></a>Microsoft OS 1.0 描述符规范


USB 设备将标准描述符存储在设备的固件中，并存储其接口和终结点。 独立硬件供应商（Ihv）还可以存储类和供应商特定的描述符。 但是，这些描述符可以包含的信息的类型会受到限制。 Ihv 通常必须使用 Windows 更新或媒体（如 CD）为其用户提供各种特定于设备的信息，如图片、图标、自定义驱动程序等。

为了帮助 Ihv 解决此问题，Microsoft 定义了 Microsoft OS 描述符。 Ihv 可以使用这些描述符在固件中存储现在通常提供给客户的大部分信息。 可识别 Microsoft OS 描述符的 Windows 版本使用控制请求来检索信息，并使用它来安装和配置设备，而无需任何用户交互。 本白皮书介绍 Microsoft 操作系统描述符，其中介绍了如何存储和检索它们。

**注意：**"扩展兼容 ID OS 功能描述符规范" 的附录1中兼容和不兼容的 Id 表在规范写入时是最新的，但可能已更改。 下表包含兼容和不兼容的兼容 Id 的最新列表。 所有 Id 都必须为8个字节，因此所有未使用的字符都将用 NULLs 填充。

<table border="0" cellpadding="0" cellspacing="0" class="grid" width="100%" summary="table">
<thead>
<tr align="left" valign="top">
<td>
<strong>CompatibleID</strong>
</td>
<td>
<strong>与子兼容的 ID</strong>
</td>
<td>
<strong>描述</strong>
</td>
</tr>
</thead>
<tbody>
<tr align="left" valign="top">
<td>（0x00 0x00 0x00 0x00 0x00 0x00 0x00 0x00）</td>
<td>（0x00 0x00 0x00 0x00 0x00 0x00 0x00 0x00）</td>
<td>没有兼容或不兼容的 ID</td>
</tr>
<tr align="left" valign="top">
<td>RNDIS<br>（0x52 0x4E 0x44 0x49 0x53 0x00 0x00 0x00）</td>
<td>（0x00 0x00 0x00 0x00 0x00 0x00 0x00 0x00）</td>
<td>远程网络驱动程序接口标准（RNDIS）</td>
</tr>
<tr align="left" valign="top">
<td>PTP<br>（0x50 0x54 0x50 0x00 0x00 0x00 0x00</td>
<td>（0x00 0x00 0x00 0x00 0x00 0x00 0x00 0x00）</td>
<td>图片传输协议（PTP）</td>
</tr>
<tr align="left" valign="top">
<td>MTP<br>（0x4D 0x54 0x50 0x00 0x00 0x00 0x00</td>
<td>（0x00 0x00 0x00 0x00 0x00 0x00 0x00 0x00）</td>
<td>媒体传输协议（MTP）</td>
</tr>
<tr align="left" valign="top">
<td>"XUSB20"<br>（0x58 0x55 0x53 0x42 0x32 0x30 0x00 0x00）</td>
<td>（0x00 0x00 0x00 0x00 0x00 0x00 0x00 0x00）</td>
<td>XNACC (Krypton)</td>
</tr>
<tr align="left" valign="top">
<td>"BLUTUTH"<br>（0x42 0x4C 0x55 0x54 0x55 0x54 0x48 0x00）</td>
<td>
<div class="contentTableWrapper"><table border="0" cellpadding="0" cellspacing="0" class="grid" width="100%" summary="table">
<tbody>
<tr align="left" valign="top">
<td>11x17<br>（0x31 0x31 0x00 0x00 0x00 0x00 0x00）</td>
<td>兼容的蓝牙无线电收发器与 Microsoft 驱动程序堆栈兼容</td>
</tr>
<tr align="left" valign="top">
<td>10<br>（0x31 0x32 0x00 0x00 0x00 0x00 0x00）</td>
<td>兼容的蓝牙无线电收发器与 Microsoft 驱动程序堆栈兼容</td>
</tr>
<tr align="left" valign="top">
<td>EDR<br>（0x45 0x44 0x52 0x00 0x00 0x00 0x00</td>
<td>符合 v2.0 + EDR 标准并与 Microsoft 驱动程序堆栈兼容的蓝牙无线收发器</td>
</tr>
</tbody>
</table></div>
<p>
<br>
</p>
</td>
<td>“蓝牙”</td>
</tr>
<tr align="left" valign="top">
<td>检测<br>（0x53 0x43 0x41 向 0x4E 0x00 0x00 0x00 0x00）</td>
<td>
<p>格式，如下所示：2字母供应商代码 + 1-5 ASCII 字符 * + 0x00</p>
<p>* ASCII 限制为大写字母、数字和下划线。</p>
</td>
<td>Scan</td>
</tr>
<tr align="left" valign="top">
<td>"3DPRINT"<br>（0x33 0x44 0x50 0x52 0x49 0x4E 0x54 0x00）</td>
<td>变化不定</td>
<td>MS3DPRINT G-3D 打印机</td>
</tr>
</tbody>
</table>

  

此信息适用于 windows XP 及更高版本的 Windows。

**继续之前，请阅读许可协议。**

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td style="text-align: center;"><strong><br />
Microsoft OS 描述符规范</strong><br />
</td>
</tr>
<tr class="even">
<td style="text-align: center;"><div style="font-size: 100%; border: thin inset; height: 400px; overflow: scroll; text-align: left; padding: 10px;">
<h3 id="microsoft-os-descriptor-specification-license-agreement">Microsoft 操作系统描述符规范许可协议</h3>
<p>这是您（个人或单个实体）（"你"）和 Microsoft Corporation （"Microsoft"）的一种法律协议（"协议"），适用于该规范。下载、复制或以其他方式使用规范即表示您同意遵守本协议的条款。   </p>
<p><strong>第1部分定义。</strong></p>
<p>（a） "您的实现" 是指实施规范中所述的操作系统描述符集以与支持 Microsoft 操作系统描述符的操作系统或 Microsoft 授权的其他系统进行交互的：（i）固件和/或硬件;和（ii）软件驱动程序，该规范中所述的操作系统描述符集只与 Windows Vista 或 Windows 7 操作系统结合在一起。</p>
<p>（b） "你的被许可方" 表示第三方许可你使用你的实现。</p>
<p>（c） "规范" 表示 Microsoft 的操作系统描述符规范和任何随附的资料。</p>
<p>第<strong>2 节授予许可证</strong>。</p>
<p>的    <strong>版权许可</strong>。Microsoft 特此授予你，该规范中的 Microsoft 的版权，是一种非专用、免版税、nontransferable、非 sublicensable 的个人全球许可证，可在内部为你和你的承包商使用开发您的实现。</p>
<p>b   <strong>专利许可证</strong>。Microsoft 特此授予您在 Microsoft 的专利范围内唯一的、免版税、nontransferable 的全球许可，这些专利仅限在规范内，并由 Microsoft 拥有或许可以进行销售、销售和直接或间接分发到你的实现。你可以根据相同的条款和条件将此专利许可证发放给你的许可证。</p>
<p>ansi-c    <strong>保留权限</strong>。Microsoft 保留了该规范中的所有其他权利、其实现以及其中的任何知识产权。对于任何其他 Microsoft 专利、商标、版权或其他知识产权，本文档不向您或任何其他实体授予任何许可。 </p>
<p><strong>第3部分：其他限制和义务</strong>。</p>
<p>（a）对规范的许可权限是根据你不创建、修改或分发你的许可实现的方式进行的，因为这种创建、修改或分发可能（a）创建、或声称创建、Microsoft 的义务根据规范（或知识产权）或（b）向任何第三方授予对该规范中的知识产权或专有权利的任何权利或 immunities。</p>
<p>（b）不损害任何其他权利，如果你未能遵守本协议的条款和条件，则 Microsoft 可能会终止本协议。 在这种情况中，必须销毁规范的所有副本，并且不得进一步分发公司实现。</p>
<p><strong>第4节免责声明。</strong></p>
<p>该规范 "按原样" 提供，不提供任何形式的保证。 在适用法律允许的最大范围内，Microsoft 会进一步拒绝所有担保，包括但不限于针对特定用途的适销性和适用性的任何默示保证，以及对标题和非侵害性的保证。 与规范的使用或性能引起的全部风险仍随你一起提供。</p>
<p><strong>第5部分：排除偶然、间接和某些其他损害。</strong></p>
<p><strong>对于适用法律允许的最大范围，在任何情况下，Microsoft 或其供应商对任何必然的都不承担责任，因使用或不能使用规范而导致的偶然、直接、间接、特殊、惩罚性或其他损害（包括但不限于业务利润损失、业务中断、业务信息丢失或其他 pecuniary 损失），即使 Microsoft 已被告知此类损失的可能性。由于某些州/管辖权不允许对间接或偶然损害的责任进行排除或限制，因此上述限制可能不适用于您。</strong></p>
<p><strong>第6节限制责任和补偿。</strong></p>
<p><strong>无论如何，无论出于何种原因（包括但不限于以上提到的所有损害以及所有直接或常规损失），都可能会对 Microsoft 及其所有供应商承担任何责任，适用于上述所有条款的协议和您的专有补偿应限制为您为规范或美国 $ 5.00 实际支付的金额。上述限制、排除项和免责声明应该适用于适用法律允许的最大范围，即使任何补救措施未能满足其基本目的。</strong></p>
<p>第<strong>7 部分适用的法律</strong>。</p>
<p>如果在美国中获得此规范，则本协议受华盛顿州法律的管辖。 根据本协议中可能出现的任何争议，你同意位于华盛顿州金县的州和联邦法院。</p>
<p><strong>第8节赋值。</strong></p>
<p>如果没有参与方事先书面批准，任何一方都不能分配此协议。</p>
</div>
<p><br />
<a href="https://download.microsoft.com/download/9/C/5/9C5B2167-8017-4BAE-9FDE-D599BAC8184A/OS_Desc_Ext_Prop.zip">我接受，下载</a></p></td>
</tr>
</tbody>
</table>