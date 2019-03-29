---
title: MB 接口模型补充程序
description: 本部分提供有关 MB 接口模型 (MBIM) 的补充信息
ms.assetid: 577BCF39-868B-44F5-A5C0-75E28689C2B6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cdbc2f5019b71faefb9b29343e41bb00ac7eaeac
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464087"
---
# <a name="mb-interface-model-supplement"></a>MB 接口模型补充


Microsoft OS 描述符分解成以下段：

-   一个 Microsoft 操作系统字符串描述符
-   一个或多个 Microsoft 操作系统功能描述符

若要支持的操作系统描述符，设备必须实现的字符串描述符。
**字符串描述符**

Microsoft OS 字符串描述符是存储在字符串索引 0xEE 的字符串。 此字符串的格式是定义完善的。

Microsoft 操作系统字符串描述符用于实现以下目标

-   Microsoft 操作系统字符串描述符存在向操作系统指示该设备已嵌入其中的 Microsoft 操作系统功能描述符的窗体中的信息。
-   Microsoft 操作系统字符串描述符具有一个嵌入式的签名字段，它用于区分从可能碰巧位于字符串索引 0xEE 在设备上的随机字符串。
-   Microsoft 操作系统字符串描述符还具有用于 Microsoft 操作系统描述符的未来版本的嵌入式的版本号码。

只有一个 Microsoft 操作系统字符串描述符存储在设备上。 以下部分介绍 Microsoft 操作系统字符串描述符和其检索过程的结构。
**OS 字符串的结构**

下面是字符串描述符的结构：

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
<th align="left">长度 （字节）</th>
<th align="left">ReplTest1</th>
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
<td align="left"><p>签名字段 (4D 00530046005400310030003000)</p></td>
</tr>
<tr class="even">
<td align="left"><p>bMS_VendorCode</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>供应商代码</p></td>
<td align="left"><p>供应商代码来提取其他操作系统功能描述符</p></td>
</tr>
<tr class="odd">
<td align="left"><p>bPad</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0x00</p></td>
<td align="left"><p>填充字段</p></td>
</tr>
</tbody>
</table>

 

Microsoft 操作系统字符串描述符的结构固定版本 1.00 之间的数值，具有 18 个字节的总长度。 中列出的 Microsoft 操作系统字符串描述符版本号**qwSignature**字段。 中存储的信息**bMS\_VendorCode**字段必须是单字节值。 它将用于检索 Microsoft 操作系统功能描述符，并且在使用此字节值**bmRequestType**字段所述，如下所示：

**检索 OS 字符串描述符**

若要检索的信息存储在字符串中，标准 GET\_描述符请求必须颁发给设备。 下面是请求的格式：

*标准 Get\_描述符字符串请求*

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
<td align="left"><p>返回的字符串</p></td>
</tr>
</tbody>
</table>

 

**BmRequestType**字段是由三个部分组成的位图，数据传输、 描述符类型和收件人的方向。 USB 规范的值根据**bmRequestType**设置为 1000年 0000b (0x80)。

为 GET\_描述符请求**wValue**字段拆分为两个部分。 高字节存储的描述符类型和低字节存储的描述符索引。 若要检索的 Microsoft 操作系统字符串描述符，应将高字节设置为检索字符串描述符 — 0x03。 由于 Microsoft 操作系统字符串描述符始终存储在索引 0xEE，此字符串索引应存储在的低字节**wValue**字段。

**WIndex**用于存储语言 ID，但必须将其设置为零的 Microsoft 操作系统字符串描述符。

**并将 wLength**字段用于指示要检索的字符串描述符的长度。 从 0x02 – 0xFF，设备应响应任何有效的范围。

如果设备不在相应的地址 (0xEE) 具有一个有效的描述符，它将响应的请求错误或停滞。 当设备不响应与停滞时，单结束零个重置将颁发给设备 （以便恢复它，如果它应进入未知状态）。

**验证操作系统描述符的完整性**

供应商有权使用的任何字符串 ID 来存储信息，因为操作系统必须验证索引 0xEE 中存储的字符串确实是 Microsoft 操作系统字符串描述符。 若要验证这一点，将进行以下测试。 失败的任何一个将会阻止 Microsoft 操作系统功能描述符的检索。

-   如果供应商将字符串存储在索引位置 0xEE，操作系统将检索字符串，并进行查询，以查看它是否是 Microsoft 操作系统字符串。 这可以通过比较以前指定的签名字段条目的字符串中的签名字段验证。 不匹配会阻止进一步分析的字符串。
-   第二个测试将包括基于签名字段中指定的版本号的字符串长度验证。 （在字符串"MSFT100"） 中指定的版本号为 1.00。 这对应于 18 字节字符串描述符。

**Microsoft OS 描述符约束字符串**

以下限制适用于 Microsoft OS 字符串描述符和其检索：

-   若要存储符合 Microsoft 操作系统描述符规范，设备信息必须有一个并仅 Microsoft 操作系统字符串符合中概述的信息的描述符[Microsoft OS 描述符](https://go.microsoft.com/fwlink/p/?linkid=308932)。
-   设备供应商可免费使用中的任何值**bMS\_VendorCode**中的 Microsoft 操作系统字符串描述符字段

**功能描述符**

功能描述符是已定义用于特定用途的固定格式说明符。

**检索操作系统功能描述符**

若要检索的 Microsoft 操作系统功能描述符特殊 GET\_MS\_描述符请求需要颁发给设备。 下面是请求的格式：

*标准版设备的请求格式*

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

 

**BmRequestType**字段是由三个部分组成的位图 — 数据传输、 描述符类型和收件人的方向，并符合 USB 规范。 Microsoft 操作系统功能描述符是特定于供应商的描述符和数据传输的方向是从设备到主机。 因此，值**bmRequestType**设置为 1100年 0000b (0xC0)。

**BRequest**字段用于指示请求的格式。 若要检索 Microsoft 操作系统功能描述符**bRequest**字段中应填充使用特殊 GET\_MS\_描述符字节。 此字节的值将由**bMS\_VendorCode**，这从 Microsoft 字符串描述符。 有关 Microsoft 操作系统字符串描述符检索的详细信息，请参阅**检索 OS 字符串描述符**。

**WValue**字段放到特殊用途和分解成高字节和低字节。 高字节用于存储接口数量。 这是必需的存储功能描述符基于每个接口，尤其是对于复合设备，或使用的设备[多个接口](https://msdn.microsoft.com/library/windows/hardware/ff537102)。 在大多数情况下，将使用接口 0。 低字节用于存储页面数量。 此功能可防止描述符具有大小为 64 KB 边界 (设置的大小的限制**并将 wLength**字段)。 描述符将提取与页面值最初设置为零。 如果完整描述符 （大小为 64 KB） 是接收页值将递增 1 并将再次发送描述符请求 （这与递增一次页面值）。 此过程将重复，直到收到大小小于 64 KB 的描述符。 请注意最大页面数为 255，这将描述符大小限制为 16 MB。

**WIndex**字段存储中要检索的 Microsoft 操作系统功能描述符功能索引号。 Microsoft 将维护此列表的 Microsoft 操作系统功能描述符和索引。 若要了解有关 Microsoft 操作系统功能描述符的详细信息，请参阅[Microsoft OS 描述符](https://go.microsoft.com/fwlink/p/?linkid=308932)。

**并将 wLength**字段指定要提取的描述符的长度。 如果描述符长于中所述的字节数**并将 wLength**返回的字段中，仅描述符的初始字节数。 如果比中指定的值短**并将 wLength**字段中，则返回一个简短的数据包。

如果不存在特定的操作系统描述符，则设备将发出的请求错误或停滞。

**Microsoft 操作系统功能描述符约束**

以下限制适用于 Microsoft 操作系统功能描述符和检索。

-   所有 Microsoft 操作系统功能描述符定义和标准化。 供应商不允许修改、 追加、 或从 Microsoft 创建而无需直接许可的 Microsoft 操作系统功能描述符。
-   所有 Microsoft 操作系统功能描述符将都具有嵌入大小和版本数量。 这些值始终应报告给系统的正确信息。
-   设备可以有多个 Microsoft 操作系统功能描述符嵌入在其固件中。
-   某些 Microsoft 操作系统功能描述符存储在每个接口级别中，而有些则是唯一的设备。 设备级 Microsoft 操作系统功能描述符应将 wValue 字段的高位字节设置为零。

**功能描述符的结构**

若要将自己标识为能够支持 MBIM，设备还必须支持扩展的配置描述符，这是一个已定义的特征描述符。 此描述符的结构如下所示。

**标头部分**

标头部分存储信息的扩展的配置描述符的其余部分。 **DwLength**字段包含整个扩展的配置描述符的长度。 标头部分还包含版本号，都将最初设置为 1.00 (0100 H)。 此说明符的未来版本可能会在后面的阶段发布。 请注意扩展的配置描述符的未来版本可能还需要增加标头部分中的条目数，因此请验证此数字准确地存储在设备和操作系统读取。

*扩展的配置描述符标头部分*

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
<th align="left">偏移量</th>
<th align="left">字段</th>
<th align="left">大小</th>
<th align="left">值</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>dwLength</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>无符号的 DWORD</p></td>
<td align="left"><p>长度字段描述了扩展的配置描述符，以字节为单位的长度。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>bcdVersion</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>BCD</p></td>
<td align="left"><p>扩展二进制编码的十进制 （例如，版本 1.00 是 0100 H） 中配置描述符发行版号。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>6</p></td>
<td align="left"><p>wIndex</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>WORD</p></td>
<td align="left"><p>固定 = 0x0004</p></td>
</tr>
<tr class="even">
<td align="left"><p>8</p></td>
<td align="left"><p>bCount</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>BYTE</p></td>
<td align="left"><p>后续的标头部分的函数部分的总数 = 0x01</p></td>
</tr>
<tr class="odd">
<td align="left"><p>9</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>7</p></td>
<td align="left"><p></p></td>
<td align="left"><p>保留</p></td>
</tr>
</tbody>
</table>

 

**函数的部分**

函数部分提供了两个条重要信息。 它为函数组，具有类似用途的连续接口进行分组，并为每个函数提供兼容和 subcompatible Id。

下面是函数部分，其中包括应由 MBIM 设备的值的格式：

*扩展的配置描述符函数部分*

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
<th align="left">Offset¹</th>
<th align="left">字段</th>
<th align="left">大小</th>
<th align="left">值</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>bFirstInterfaceNumber</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>Byte</p></td>
<td align="left"><p>启动此函数的接口数量 = 0x00</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>bInterfaceCount</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>Byte</p></td>
<td align="left"><p>必须包含到此函数的接口的总数 = 0x01</p></td>
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
<td align="left"><p>保留</p></td>
<td align="left"><p>6</p></td>
<td align="left"><p></p></td>
<td align="left"><p>保留 = 0</p></td>
</tr>
</tbody>
</table>

 

自定义属性部分 ¹Offset 具有已重置为零。 若要计算的偏移量从一开始扩展的配置描述符字段，请添加在其之前的部分的长度。

*兼容和 Subcompatible Id 基于公开 MBIM 函数的配置*

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
<p>(0x41 0x4C 0x54 0x52 0x43 0x46 0x47 0x00)</p></td>
<td align="left"><p>20000000</p>
<p>(0x32 0x00 0x00 0x00 0x00 0x00 0x00 0x00)</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>ALTRCFG</p>
<p>(0x41 0x4C 0x54 0x52 0x43 0x46 0x47 0x00)</p></td>
<td align="left"><p>30000000</p>
<p>(0x33 0x00 0x00 0x00 0x00 0x00 0x00 0x00)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p>ALTRCFG</p>
<p>(0x41 0x4C 0x54 0x52 0x43 0x46 0x47 0x00)</p></td>
<td align="left"><p>40000000</p>
<p>(0x34 0x00 0x00 0x00 0x00 0x00 0x00 0x00)</p></td>
</tr>
</tbody>
</table>

 

-   **bConfiguration**是指**bConfiguration**公开 MBIM 函数的配置的 USB 配置描述符中的值。 **bConfiguration**不能为 1，因为这是公开只有 CDROM 函数的默认配置。 **bConfiguration**不能大于 4; 也就是说，MBIM 函数不应公开前四个配置中。
-   compatibleID 将保持不变的所有配置。 根据配置 subcompatibleID 更改

**示例**

此表显示了一个示例多配置方案。 表列出了可在每个配置和不同版本的操作系统采用这些配置的每个操作中的函数：

*多重配置的移动宽带设备的示例*

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
<th align="left">1 （Windows 7 配置）</th>
<th align="left">2 （IHV-NCM-1.0-配置）</th>
<th align="left">3 （Windows 8 配置）</th>
<th align="left">3 （IHV-NCM-2.0-配置）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>显示功能</p></td>
<td align="left"><p>CDROM</p>
<p>SD</p></td>
<td align="left"><p>CD-ROM</p>
<p>SD</p>
<p>NCM1.0</p>
<p>调制解调器</p>
<p>TV</p>
<p>GPS</p>
<p>FP</p>
<p>PC/SC 智能卡</p>
<p>语音</p>
<p>诊断工具</p></td>
<td align="left"><p>CD-ROM</p>
<p>SD</p>
<p>MBIM</p></td>
<td align="left"><p>CD-ROM</p>
<p>SD</p>
<p>NCM2.0</p>
<p>调制解调器</p>
<p>TV</p>
<p>GPS</p>
<p>FP</p>
<p>PC/SC 智能卡</p>
<p>语音</p>
<p>诊断工具</p></td>
</tr>
</tbody>
</table>

 

下表显示了使用 Microsoft 操作系统字符串描述符的值和 Microsoft 操作系统扩展前面的示例多配置方案的配置功能描述符。

*多重配置的移动宽带设备的示例*

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">字段</th>
<th align="left">长度 （字节）</th>
<th align="left">ReplTest1</th>
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
<td align="left"><p>‘MSFT100’</p>
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
<th align="left">偏移量</th>
<th align="left">字段</th>
<th align="left">大小</th>
<th align="left">ReplTest1</th>
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
<td align="left"><p>保留</p></td>
<td align="left"><p>7</p></td>
<td align="left"><p></p></td>
</tr>
</tbody>
</table>

 

*扩展的配置功能描述符函数的示例 Microsoft 操作系统*

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Offset²</th>
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
<td align="left"><p>保留</p></td>
<td align="left"><p>6</p></td>
<td align="left"><p></p></td>
</tr>
</tbody>
</table>

 

自定义属性部分 ²Offset 具有已重置为零。 若要计算的偏移量从一开始扩展的配置描述符字段，请添加在其之前的部分的长度。

 

 





