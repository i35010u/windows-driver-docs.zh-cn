---
title: MB 接口型号补充
description: '本部分提供了 MB 接口型号 (MBIM 的补充信息) '
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c54449ab155ed16fa59ba55acf6077b104586f99
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801645"
---
# <a name="mb-interface-model-supplement"></a>MB 接口模型补充


Microsoft OS 描述符分为以下几个部分：

-   一个 Microsoft 操作系统字符串描述符
-   一个或多个 Microsoft OS 功能描述符

若要支持操作系统描述符，设备必须实现字符串说明符。
**字符串描述符**

Microsoft OS 字符串描述符是在字符串索引0xEE 存储的字符串。 此字符串的格式定义正确。

Microsoft OS 字符串描述符用于实现以下目标

-   如果存在 Microsoft 操作系统字符串描述符，则会向操作系统显示设备嵌入信息的操作系统，其形式为 Microsoft OS 功能描述符。
-   Microsoft OS 字符串描述符具有嵌入的签名字段，该字段用于将其与在字符串索引0xEE 的设备上可能发生的随机字符串区分开来。
-   Microsoft 操作系统字符串描述符还具有嵌入的版本号，可供将来的 Microsoft 操作系统描述符版本使用。

设备上只存储一个 Microsoft OS 字符串描述符。 以下各节描述了 Microsoft 操作系统字符串描述符及其检索过程的结构。
**OS 字符串的结构**

以下是字符串描述符的结构：

*字符串描述符结构*

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">字段</th>
<th align="left">长度 (字节) </th>
<th align="left">“值”</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>bLength</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x12</p></td>
<td align="left"><p>描述符的长度</p></td>
</tr>
<tr class="even">
<td align="left"><p>bDescriptorType</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x03</p></td>
<td align="left"><p>字符串描述符</p></td>
</tr>
<tr class="odd">
<td align="left"><p>qwSignature</p></td>
<td align="left"><p>14</p></td>
<td align="left"><p>"MSFT100"</p></td>
<td align="left"><p>签名字段 (4D00530046005400310030003000) </p></td>
</tr>
<tr class="even">
<td align="left"><p>bMS_VendorCode</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>供应商代码</p></td>
<td align="left"><p>用于提取其他 OS 功能描述符的供应商代码</p></td>
</tr>
<tr class="odd">
<td align="left"><p>bPad</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x00</p></td>
<td align="left"><p>填充字段</p></td>
</tr>
</tbody>
</table>

 

Microsoft 操作系统字符串描述符的结构在版本1.00 中是固定的，总长度为18个字节。 Microsoft OS 字符串描述符的版本号在 **qwSignature** 字段中列出。 存储在 **bMS \_ VendorCode** 字段中的信息必须是单字节值。 它将用于检索 Microsoft OS 功能描述符，在 **bmRequestType** 字段中使用此字节值，如下所述：

**检索 OS 字符串描述符**

若要检索存储在字符串中的信息， \_ 必须向设备发出标准 GET 描述符请求。 下面是请求的格式：

*标准 Get \_ 描述符字符串请求*

<table style="width:100%;">
<colgroup>
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">bmRequestType</th>
<th align="left">bRequest</th>
<th align="left">wValue</th>
<th align="left">wIndex</th>
<th align="left">wLength</th>
<th align="left">数据</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1000 0000b</p></td>
<td align="left"><p>GET_DESCRIPTOR</p></td>
<td align="left"><p>0x03EE</p></td>
<td align="left"><p>0x0000</p></td>
<td align="left"><p>0x12</p></td>
<td align="left"><p>返回字符串 </p></td>
</tr>
</tbody>
</table>

 

**BmRequestType** 字段是由三个部分组成的位图：数据传输方向、描述符类型和接收方。 根据 USB 规范， **bmRequestType** 的值设置为 1000 0000b (0x80) 。

对于 GET \_ 描述符请求， **wValue** 字段分为两部分。 高字节存储描述符类型并且低字节存储描述符索引。 若要检索 Microsoft OS 字符串描述符，应将高位字节设置为检索字符串描述符（0x03）。 由于 Microsoft 操作系统字符串描述符始终存储在索引0xEE 上，因此，此字符串索引应存储在 **wValue** 字段的下一个字节。

**WIndex** 用于存储语言 ID，但对于 Microsoft OS 字符串描述符，它必须设置为零。

**WLength** 字段用于指示要检索的字符串描述符的长度。 设备应响应0x02 –0xFF 中的任何有效范围。

如果设备在相应的地址上没有有效的描述符 (0xEE) ，则它将响应请求错误或停止。 如果设备未使用延迟进行响应，则会将单结束的零重置发送到设备 (进行恢复，如果它应进入未知状态) 。

**验证操作系统描述符的完整性**

由于允许供应商使用任意字符串 ID 来存储信息，因此操作系统必须验证存储在索引0xEE 中的字符串是否确实为 Microsoft OS 字符串描述符。 若要验证这一点，将执行以下测试。 否则，将不会阻止检索 Microsoft 操作系统功能描述符。

-   如果供应商将字符串存储在索引位置0xEE，则操作系统将检索该字符串，并对其进行查询以查看它是否为 Microsoft OS 字符串。 这可以通过将字符串中的签名字段与之前指定的签名字段项进行比较来进行验证。 不匹配将阻止进一步分析字符串。
-   第二个测试将根据在 "签名" 字段中指定的版本号，对字符串长度进行验证。 字符串 "MSFT100" ) 中指定 (的版本号为1.00。 这对应于18字节字符串说明符。

**Microsoft OS 字符串描述符约束**

以下约束适用于 Microsoft OS 字符串描述符及其检索：

-   若要存储符合 Microsoft OS 描述符规范的信息，该设备必须有一个且仅有一个 Microsoft 操作系统字符串描述符，该描述符符合 [MICROSOFT 操作系统描述符](/previous-versions/gg463179(v=msdn.10))中列出的信息。
-   设备供应商可以在 Microsoft OS 字符串描述符的 **bMS \_ VendorCode** 字段中随意使用任何值

**功能描述符**

功能描述符是已为特定目的定义的固定格式的描述符。

**检索 OS 功能描述符**

若要检索 Microsoft OS 功能描述符， \_ \_ 需要向设备发出特殊的 GET MS 描述符请求。 下面是请求的格式：

*标准设备请求格式*

<table style="width:100%;">
<colgroup>
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">bmRequestType</th>
<th align="left">bRequest</th>
<th align="left">wValue</th>
<th align="left">wIndex</th>
<th align="left">wLength</th>
<th align="left">数据</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1100 0000b</p></td>
<td align="left"><p>GET_MS_DESCRIPTOR</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>功能索引</p></td>
<td align="left"><p>长度</p></td>
<td align="left"><p>返回描述符</p></td>
</tr>
</tbody>
</table>

 

**BmRequestType** 字段是由三个部分组成的位图（数据传输方向、描述符类型和接收方），并且符合 USB 规范。 Microsoft OS 功能描述符是特定于供应商的描述符，数据传输方向是从设备到主机。 因此， **bmRequestType** 的值设置为 1100 0000B (0xC0) 。

**BRequest** 字段用于指示请求的格式。 若要检索 Microsoft OS 功能描述符，应 **bRequest** 使用特殊的 GET \_ MS 描述符字节填充 "bRequest" 字段 \_ 。 此字节的值由从 Microsoft 字符串说明符中检索的 **bMS \_ VendorCode** 表示。 有关检索 Microsoft OS 字符串描述符的详细信息，请参阅 **检索 OS 字符串描述符**。

" **WValue** " 字段设置为 "特殊用途"，并被分解为高字节和低字节。 高字节用于存储接口号。 这对于基于每个接口存储功能描述符至关重要，特别是对于复合设备或具有 [多个接口](/windows-hardware/drivers/ddi/index)的设备。 在大多数情况下，将使用 interface 0。 低字节用于存储页码。 此功能可防止描述符的大小边界为 64 KB (**wLength** 字段大小设置的限制) 。 将使用初始设置为零的页面值提取描述符。 如果收到 (大小为 64 KB) 的完整描述符，则页面值将以1递增，此时将再次发送对描述符的请求 (，并) 增加的页面值。 此过程将重复，直至收到大小小于 64 KB 的描述符。 请注意，最大页数为255，表示描述符大小限制为 16 MB。

**WIndex** 字段存储正在检索的 Microsoft OS 功能描述符的功能索引号。 Microsoft 将维护此 Microsoft OS 功能描述符和索引列表。 若要了解有关 Microsoft OS 功能描述符的详细信息，请参阅 [MICROSOFT Os 描述符](/previous-versions/gg463179(v=msdn.10))。

**WLength** 字段指定要提取的描述符的长度。 如果描述符的长度超过了在 **wLength** 字段中指定的字节数，则仅返回描述符的初始字节数。 如果其短于在 **wLength** 字段中指定的值，则返回短的数据包。

如果不存在特定的操作系统描述符，则设备将发出请求错误或停止。

**Microsoft OS 功能描述符约束**

以下约束适用于 Microsoft OS 功能描述符及其检索。

-   所有 Microsoft 操作系统功能描述符都定义并标准化。 不允许供应商在未经 Microsoft 直接同意的情况下修改、追加或创建 Microsoft OS 功能描述符。
-   所有 Microsoft 操作系统功能描述符都具有嵌入的大小和版本号。 这些值应始终向操作系统报告正确的信息。
-   一个设备可以将多个 Microsoft OS 功能描述符嵌入到其固件中。
-   某些 Microsoft OS 功能描述符存储在每个接口级别上，而另一些则在设备上是唯一的。 设备级 Microsoft OS 功能描述符应将 wValue 字段的高位字节设置为零。

**功能描述符的结构**

若要将自身标识为支持 MBIM，设备还必须支持扩展配置描述符，这是一个已定义的功能描述符。 此描述符的结构如下所示。

**标头部分**

标头部分存储有关扩展配置描述符的其余部分的信息。 **DwLength** 字段包含整个扩展配置描述符的长度。 标头部分还包含版本号，该版本号最初设置为 1.00 (0100H) 。 此描述符的将来版本可能会在以后发布。 请注意，扩展配置描述符的未来版本可能还需要增加 "标头" 部分中的条目数，因此请验证此数字是否准确存储在设备中，并由操作系统读取。

*扩展配置描述符标头部分*

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
<th align="left">Offset</th>
<th align="left">字段</th>
<th align="left">大小</th>
<th align="left">值</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>dwLength</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>无符号 DWORD</p></td>
<td align="left"><p>"长度" 字段描述扩展配置描述符的长度（以字节为单位）。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>bcdVersion</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>BCD</p></td>
<td align="left"><p>二进制编码的十进制 (中的扩展配置描述符版本号，例如，版本1.00 是 0100H) 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>6</p></td>
<td align="left"><p>wIndex</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>WORD</p></td>
<td align="left"><p>Fixed = 0x0004</p></td>
</tr>
<tr class="even">
<td align="left"><p>8</p></td>
<td align="left"><p>bCount</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>BYTE</p></td>
<td align="left"><p>在标头部分之后的函数部分的总数 = 0x01</p></td>
</tr>
<tr class="odd">
<td align="left"><p>9</p></td>
<td align="left"><p>RESERVED</p></td>
<td align="left"><p>7</p></td>
<td align="left"><p></p></td>
<td align="left"><p>RESERVED</p></td>
</tr>
</tbody>
</table>

 

**Function 部分**

函数部分提供了两个重要的信息片段。 它将与函数组相似的连续接口分组，并为每个函数提供兼容的和 subcompatible 的 Id。

下面是函数部分的格式，包括应由 MBIM 设备使用的值：

*扩展配置描述符函数部分*

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
<th align="left">偏移为¹</th>
<th align="left">字段</th>
<th align="left">大小</th>
<th align="left">值</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>bFirstInterfaceNumber</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>Byte</p></td>
<td align="left"><p>此函数的开始接口号 = 0x00</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>bInterfaceCount</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>Byte</p></td>
<td align="left"><p>此函数必须包含的接口总数 = 0x01</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>compatibleID</p></td>
<td align="left"><p>8</p></td>
<td align="left"><p>字节</p></td>
<td align="left"><p>兼容 ID</p></td>
</tr>
<tr class="even">
<td align="left"><p>10</p></td>
<td align="left"><p>subCompatibleID</p></td>
<td align="left"><p>8</p></td>
<td align="left"><p>字节</p></td>
<td align="left"><p>Subcompatible ID</p></td>
</tr>
<tr class="odd">
<td align="left"><p>18</p></td>
<td align="left"><p>RESERVED</p></td>
<td align="left"><p>6</p></td>
<td align="left"><p></p></td>
<td align="left"><p>RESERVED = 0</p></td>
</tr>
</tbody>
</table>

 

¹自定义属性部分的偏移量已重置为零。 若要计算字段相对于扩展配置描述符开头的偏移量，请添加其前面的部分的长度。

*基于公开 MBIM 函数的配置的兼容和 Subcompatible Id*

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">bConfiguration</th>
<th align="left">compatibleID</th>
<th align="left">subCompatibleID</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>ALTRCFG</p>
<p> (0x41 向 0x4C 0x54 0x52 0x43 0x46 0x47 0x00) </p></td>
<td align="left"><p>20000000</p>
<p> (0x32 0x00 0x00 0x00 0x00 0x00 0x00) </p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>ALTRCFG</p>
<p> (0x41 向 0x4C 0x54 0x52 0x43 0x46 0x47 0x00) </p></td>
<td align="left"><p>30000000</p>
<p> (0x33 0x00 0x00 0x00 0x00 0x00 0x00) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p>ALTRCFG</p>
<p> (0x41 向 0x4C 0x54 0x52 0x43 0x46 0x47 0x00) </p></td>
<td align="left"><p>40000000</p>
<p> (0x34 赋 0x00 0x00 0x00 0x00 0x00 0x00) </p></td>
</tr>
</tbody>
</table>

 

-   **bConfiguration** 引用用于公开 MBIM 函数的配置的 USB 配置描述符中的 **bConfiguration** 值。 **bConfiguration** 不能为1，因为这是仅公开 CDROM 函数的默认配置。 **bConfiguration** 不能大于 4;也就是说，MBIM 函数应在前四个配置内公开。
-   所有配置的 compatibleID 保持不变。 SubcompatibleID 会根据配置进行更改

**示例**

下表显示了一个示例多配置方案。 该表列出了每个配置中可用的功能，以及不同版本的操作系统对每个配置所采用的操作：

*多配置移动宽带设备的示例*

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
<th align="left">bConfiguration</th>
<th align="left">1 (Windows 7-配置) </th>
<th align="left">2 (IHV-NCM-1.0-配置) </th>
<th align="left">3 (Windows 8-配置) </th>
<th align="left">3 (IHV-NCM-2.0-Configuration) </th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>公开的函数</p></td>
<td align="left"><p>CDROM</p>
<p>SD</p></td>
<td align="left"><p>CD-ROM</p>
<p>SD</p>
<p>NCM 1。0</p>
<p>调制解调器</p>
<p>TV</p>
<p>GPS</p>
<p>FP</p>
<p>PC/SC 智能卡</p>
<p>语音</p>
<p>斜</p></td>
<td align="left"><p>CD-ROM</p>
<p>SD</p>
<p>MBIM</p></td>
<td align="left"><p>CD-ROM</p>
<p>SD</p>
<p>NCM 2。0</p>
<p>调制解调器</p>
<p>TV</p>
<p>GPS</p>
<p>FP</p>
<p>PC/SC 智能卡</p>
<p>语音</p>
<p>斜</p></td>
</tr>
</tbody>
</table>

 

下表显示了 Microsoft 操作系统字符串描述符使用的值，以及以前的示例多配置方案的 Microsoft 操作系统扩展配置功能描述符。

*多配置移动宽带设备的示例*

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">字段</th>
<th align="left">长度 (字节) </th>
<th align="left">“值”</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>bLength</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x12</p></td>
</tr>
<tr class="even">
<td align="left"><p>bDescriptorType</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x03</p></td>
</tr>
<tr class="odd">
<td align="left"><p>qwSignature</p></td>
<td align="left"><p>14</p></td>
<td align="left"><p>'MSFT100'</p>
<p>0x4D 0x00 0x53 0x00 0x46 0x00 0x54 0x00 0x31 0x00 0x30 0x00 0x30 0x00</p></td>
</tr>
<tr class="even">
<td align="left"><p>bMS_VendorCode</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0xA5</p></td>
</tr>
<tr class="odd">
<td align="left"><p>bPad</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x00</p></td>
</tr>
</tbody>
</table>

 

*示例 Microsoft 操作系统扩展配置功能描述符标头*

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Offset</th>
<th align="left">字段</th>
<th align="left">大小</th>
<th align="left">值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>dwLength</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>16</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>bcdVersion</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>0100H</p></td>
</tr>
<tr class="odd">
<td align="left"><p>6</p></td>
<td align="left"><p>wIndex</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>0x0004</p></td>
</tr>
<tr class="even">
<td align="left"><p>8</p></td>
<td align="left"><p>bCount</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>9</p></td>
<td align="left"><p>RESERVED</p></td>
<td align="left"><p>7</p></td>
<td align="left"><p></p></td>
</tr>
</tbody>
</table>

 

*示例 Microsoft OS 扩展配置功能描述符函数*

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">偏移²</th>
<th align="left">字段</th>
<th align="left">大小</th>
<th align="left">值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>bFirstInterfaceNumber</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p></p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>bInterfaceCount</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p></p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>compatibleID</p></td>
<td align="left"><p>8</p></td>
<td align="left"><p></p></td>
</tr>
<tr class="even">
<td align="left"><p>10</p></td>
<td align="left"><p>subCompatibleID</p></td>
<td align="left"><p>8</p></td>
<td align="left"><p></p></td>
</tr>
<tr class="odd">
<td align="left"><p>18</p></td>
<td align="left"><p>RESERVED</p></td>
<td align="left"><p>6</p></td>
<td align="left"><p></p></td>
</tr>
</tbody>
</table>

 

自定义属性部分的²偏移量已重置为零。 若要计算字段相对于扩展配置描述符开头的偏移量，请添加其前面的部分的长度。

