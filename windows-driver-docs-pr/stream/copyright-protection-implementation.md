---
title: 版权保护实现
description: 版权保护实现
ms.assetid: 42d91ad3-615a-461a-846b-4876ac8decea
keywords:
- DVD 解码器微型驱动程序 WDK，版权保护
- 解码器微型驱动程序 WDK DVD，版权保护
- 版权保护的 WDK DVD 解码器
- 内容加密系统 WDK DVD 解码器
- CSS WDK DVD 解码器
- DVD decrypters WDK
- 密钥交换的 WDK DVD 解码器
- 解密 WDK DVD 解码器
- 加密 WDK DVD 解码器
- 加密 WDK DVD 解码器
- 身份验证的 WDK DVD 解码器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 596b6f7fc46f4300e78602b8b55b292e62890088
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534356"
---
# <a name="copyright-protection-implementation"></a>版权保护实现





Microsoft 提供了简化了身份验证过程的软件所需的系统在混合内容 (CSS) 方案，从而允许进行身份验证和传输与 DVD 解密的密钥的 DVD-ROM 驱动器。 Microsoft 不提供 DVD 解密。 相反，Microsoft 提供了将充当代理以允许进行身份验证的硬件或软件 decrypters 操作系统代码。

密钥交换过程是启动并受 DVD 拆分器导航器/筛选器。 DVD 解码器微型驱动程序只需实现下一节中列出的属性。 由其他组件，其余部分进行处理。

每个 DVD 输入的流接收版权保护属性。 即使所有 DVD 流都控制的相同硬件，这是如此。

视频端口属性集的 GUID 是[KSPROPSETID\_CopyProt](https://msdn.microsoft.com/library/windows/hardware/ff566572)。 提供了以下属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565140" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_CHLG_KEY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565140)"><strong>KSPROPERTY_DVDCOPY_CHLG_KEY</strong></a></p></td>
<td><p>此属性支持 get 和 set。 获取属性请求解码器来提供其总线质询密钥。 设置属性使用中的 DVD 驱动器的总线质询密钥提供解码器。 此属性中传递的数据是类型的结构<a href="https://msdn.microsoft.com/library/windows/hardware/ff567636" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_CHLGKEY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567636)"> <strong>KS_DVDCOPY_CHLGKEY</strong></a>。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565145" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_DVD_KEY1&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565145)"><strong>KSPROPERTY_DVDCOPY_DVD_KEY1</strong></a></p></td>
<td><p>仅限组的属性。 此属性提供给解码器的 DVD 驱动器总线密钥 1。 传递的数据是类型的结构<a href="https://msdn.microsoft.com/library/windows/hardware/ff567635" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_BUSKEY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567635)"> <strong>KS_DVDCOPY_BUSKEY</strong></a>。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565142" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_DEC_KEY2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565142)"><strong>KSPROPERTY_DVDCOPY_DEC_KEY2</strong></a></p></td>
<td><p>只读属性。 此属性将请求解码器&#39;s 总线密钥 2 将转移到其中的 DVD 驱动器。 传递的数据是类型的结构<a href="https://msdn.microsoft.com/library/windows/hardware/ff567635" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_BUSKEY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567635)"> <strong>KS_DVDCOPY_BUSKEY</strong></a>。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565148" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_TITLE_KEY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565148)"><strong>KSPROPERTY_DVDCOPY_TITLE_KEY</strong></a></p></td>
<td><p>仅限组的属性。 从当前内容，这提供标题键。 该密钥是类型的结构<a href="https://msdn.microsoft.com/library/windows/hardware/ff567640" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_TITLEKEY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567640)"> <strong>KS_DVDCOPY_TITLEKEY</strong></a>。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565144" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_DISC_KEY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565144)"><strong>KSPROPERTY_DVDCOPY_DISC_KEY</strong></a></p></td>
<td><p>仅限组的属性。 这提供了光盘密钥。</p>
<div>
 
</div>
该密钥是类型的结构<a href="https://msdn.microsoft.com/library/windows/hardware/ff567637" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_DISCKEY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567637)"> <strong>KS_DVDCOPY_DISCKEY</strong></a>。</td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565114" data-raw-source="[&lt;strong&gt;KSPROPERTY_COPY_MACROVISION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565114)"><strong>KSPROPERTY_COPY_MACROVISION</strong></a></p></td>
<td><p>仅限组的属性。 该密钥是类型的结构<a href="https://msdn.microsoft.com/library/windows/hardware/ff567316" data-raw-source="[&lt;strong&gt;KS_COPY_MACROVISION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567316)"> <strong>KS_COPY_MACROVISION</strong></a>。 这是模拟 NTSC 视频流，很快就会处理 NTSC macrovision 属性。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565146" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_REGION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565146)"><strong>KSPROPERTY_DVDCOPY_REGION</strong></a></p></td>
<td><p>只读属性。 DVD 微型驱动程序都适合一个区域位。 该密钥是类型的结构<a href="https://msdn.microsoft.com/library/windows/hardware/ff567638" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_REGION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567638)"> <strong>KS_DVDCOPY_REGION</strong></a>。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565147" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_SET_COPY_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565147)"><strong>KSPROPERTY_DVDCOPY_SET_COPY_STATE</strong></a></p></td>
<td><p>获取组的唯一属性。 该密钥是类型的结构<a href="https://msdn.microsoft.com/library/windows/hardware/ff567639" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_SET_COPY_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567639)"> <strong>KS_DVDCOPY_SET_COPY_STATE</strong></a>。 此属性使用</p>
<p>KS_DVDCOPYSTATE_AUTHENTICATION_NOT_REQUIRED,</p>
<p>KS_DVDCOPYSTATE_AUTHENTICATION_REQUIRED，</p>
<p>KS_DVDCOPYSTATE_INITIALIZE，和</p>
<p>KS_DVDCOPYSTATE_INITIALIZE_TITLE。</p></td>
</tr>
</tbody>
</table>

 

按以下顺序重复的每个打开 DVD 输入插针上解码器。 解码器按以下顺序接收密钥：

获取 KSPROPERTY\_DVDCOPY\_CHLG\_密钥

Set KSPROPERTY\_DVDCOPY\_DVD\_KEY1

设置 KSPROPERTY\_DVDCOPY\_CHLG\_密钥

Get KSPROPERTY\_DVDCOPY\_DEC\_KEY2

Set KSPROPERTY\_DVDCOPY\_DISC\_KEY

然后，接收以下项：

获取 KSPROPERTY\_DVDCOPY\_CHLG\_密钥

Set KSPROPERTY\_DVDCOPY\_DVD\_KEY1

设置 KSPROPERTY\_DVDCOPY\_CHLG\_密钥

Get KSPROPERTY\_DVDCOPY\_DEC\_KEY2

设置 KSPROPERTY\_DVDCOPY\_标题\_密钥

此序列还重复的每个打开 DVD 输入插针上解码器。 在任何时候 DVD 光盘密钥已成功建立并可能会出现不止一次每个光盘密钥后，它可能会发生。 每当读取包含标题键的扇区时，必须成功完成身份验证过程。 如果身份验证失败，会阻止读取并返回相应的错误消息。

 

 




