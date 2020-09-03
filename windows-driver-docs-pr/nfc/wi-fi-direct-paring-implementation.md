---
title: Wi-Fi direct 配对实现
description: 本部分提供外围设备的设计准则和要求，以便加入点击和设置并点击和重新连接用例。
ms.assetid: 1B729E9F-DF9F-4263-9F0B-5EDCF817D2C3
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: efeedecbbba5118fe49cae7cfec56c5e403a26e4
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384247"
---
# <a name="wi-fi-direct-pairing-implementation"></a>Wi-Fi direct 配对实现


本部分提供外围设备的设计准则和要求，以便加入点击和设置并点击和重新连接用例。

**注意**   本主题中所述的配对实现当前在 Windows 8.1 中受支持，仅用于配对到打印机设备。

 

**注意**   Windows 10 还支持通过 Wi-fi 联盟的 Wi-fi P2P 运营商配置记录进行的 Wi-fi Direct 静态连接。 有关详细信息，请参阅 [Wi-fi 联盟](https://www.wi-fi.org/)。

 

## <a name="peripheral-wi-fi-direct-device-pairing"></a>外设 Wi-fi Direct Device 配对


在点击过程中，NFP 从连接设备接收配对信息。 NFP 将配对信息传递给 Windows。 Wi-fi Direct 设备遵循 Wi-fi 联盟带外 (OOB) 配对过程和 NFC 论坛建议。 Windows 依赖于如下定义的专有配对消息。

Windows 将提示用户同意，如果提供，Windows 将尝试按顺序连接到每个地址，直到成功为止。 PC 中的 NFP 提供程序与连接设备之间没有进一步的交互。

使用 NFC 作为示例，通过将配对信息存储在静态或被动 NFC 标记中来完成单向安装， (静态模拟模式下的活动 NFC 标记也可以) 使用。 Windows 订阅此配对信息。 PC 上启用 NFC 的 NFP 提供程序接收来自标记的连接信息，并将其作为订户传递到 Windows。 收到连接信息后，Windows 将使用特定于设备类的技术来执行设备的实际安装。

## <a name="interoperability-requirements"></a>互操作性要求


为了确保与 NFP 提供程序之间的互操作性，应使用特定于提供程序的消息格式来封装配对信息。

如本文档的其他部分所述，对于不支持 NFC 的 NFP 提供程序的邻近技术，没有特定的要求。

Windows 要求启用了 NFC 的 NFP 提供程序支持特定 NFC 论坛定义的机制，用于传达用于单向配对的 Wi-fi Direct OOB 配对信息。 NDEF 消息包含 TNF 字段值为0x01 的第一条记录和等于 "Hs" 的类型字段，以及一个指向 Wi-fi 直接运营商配置记录的备用运营商记录。 在此方法中，将只使用 NDEF 记录的有效负载。

## <a name="unidirectional-pairing-using-nfc-for-wi-fi-direct"></a>使用 NFC 实现 Wi-fi 直接的单向配对


本部分提供了有关 NFC、Wi-fi Direct 和 Windows 如何协同工作以支持 Wi-fi Direct 设备（如打印机）的单向无线配对的更多详细信息。

### <a name="nfp-provider-references"></a>NFP 提供程序引用

通过使用 NFC 论坛标准化连接切换选择消息类型来完成 wi-fi 直接配对。 下图概述了连接切换选择消息如何应用于 Wi-fi Direct 设备配对，特别是 NDEF 记录3和4。 移交选择消息描述了一个或多个 "ac" 或 "备用运营商" 记录。 这些记录按顺序跟踪选择记录，每个记录都具有定义完善的类型。 最后，该消息将包含一个 Microsoft 定义的设备配对记录，该记录向 Windows 提供有关如何处理配对操作的信息。

![连接切换选择消息](images/handover.png)

### <a name="wi-fi-direct-device-pairing-message"></a>Wi-fi Direct 设备配对消息

在接下来的示例用例中，NFC 类型2标记用作演示示例。 如果需要使用不同的 NFC 标记类型，则必须根据标记定义正确地封装 NDEF 消息。

| 字段                 | 值                                            | 说明                                                               |
|-----------------------|--------------------------------------------------|---------------------------------------------------------------------------|
| TNF                   | 0x02                                             | 后面的类型字段的格式。 在 RFC 2046 中定义的媒体类型。 |
| 类型                  | "application/vnd.apple.mpegurl"             | 我们为此方案定义的新类型字符串。                              |
| OOB 数据的大小      | WORD                                             | 支持高达 64 KB 的 OOB 数据。                                        |
| Wi-fi Direct OOB 数据 | &lt;上一个字段指示的大小的 blob&gt; | 按如下定义的 wi-fi Direct OOB 数据。                                   |

 

### <a name="wi-fi-direct-oob-format"></a>Wi-fi Direct OOB 格式

下表描述了 WiFi 直接 OOB 数据的格式。 任何单向 P2P OOB 设备都可以传输 OOB 单向数据。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">属性</th>
<th align="left">属性 ID</th>
<th align="left">必需/可选</th>
<th align="left">备注</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>OOB 标头</p>
<p>请参阅 OOB 标头属性格式表。</p></td>
<td align="left">空值</td>
<td align="left">必选</td>
<td align="left">OOB 标头属性应该出现在 P2P OOB 数据 blob 中，并将其 OOB 类型值设置为 "OOB 单向预配数据"。</td>
</tr>
<tr class="even">
<td align="left"><p>OOB 设备信息</p>
<p>请参阅 OOB 设备信息属性格式表。</p></td>
<td align="left">1</td>
<td align="left">必须</td>
<td align="left">此特性必须存在。 它提供有关此 P2P 设备的信息。</td>
</tr>
<tr class="odd">
<td align="left"><p>OOB 设置信息</p>
<p></p></td>
<td align="left">2</td>
<td align="left">必选</td>
<td align="left">此特性必须存在。 它提供此 P2P 设备预期使用的设置信息。</td>
</tr>
<tr class="even">
<td align="left"><p>OOB 配置超时</p>
<p></p></td>
<td align="left">5</td>
<td align="left">必选</td>
<td align="left">此特性必须存在。 它提供有关此 P2P 设备等待一个基于 Wi-fi Direct 的响应的时间的信息。</td>
</tr>
</tbody>
</table>

 

### <a name="oob-header-attribute-format"></a>OOB 标头特性格式

| 字段名称        | 大小 (八进制)  | 值    | 说明                                                                                                    |
|-------------------|---------------|----------|----------------------------------------------------------------------------------------------------------------|
| 总数据长度 | 2             | 变量 | 整个 OOB 数据 Blob 的长度 (包括标题) 。                                                             |
| Length            | 2             | 变量 | OOB 标头中的以下字段的长度。                                                                  |
| 版本           | 1             | 0x10     | 标识此 P2P OOB 记录版本的值。                                                          |
| OOB 类型          | 1             | 变量 | 标识 OOB 事务类型的值。 特定值在 " *OOB 事务类型* " 表中定义。 |
| OUI               | 0或3        | 变量 | 特定于供应商的 OUI。 此值为可选值。 仅当 OOB 类型特定于供应商时，才能存在。         |
| OUI 类型          | 0 或 1        | 变量 | 供应商特定类型。 此值为可选值。 仅当 OOB 类型特定于供应商时，才能存在。        |

 

### <a name="oob-transaction-types"></a>OOB 事务类型

| OOB 类型 (Hex)  | 说明                          |
|----------------|--------------------------------------|
| 0x00           | OOB 单向预配数据 |
| 0x01           | OOB 预配侦听器数据       |
| 0x02           | OOB 预配连接器数据      |
| 0x03           | OOB Reinvoke 数据                    |
| 0x04-0xDC      | 预留                             |
| 0xDD           | 特定于供应商                      |
| 0xDE-0xFF      | 预留                             |

 

### <a name="oob-device-info-attribute-format"></a>OOB 设备信息特性格式

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">字段名称</th>
<th align="left">大小 (八进制) </th>
<th align="left">值</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">属性 ID</td>
<td align="left">1</td>
<td align="left">1</td>
<td align="left">标识 P2P OOB 特性的类型。 特定值在 " <em>P2P OOB 属性</em> " 表中定义。</td>
</tr>
<tr class="even">
<td align="left">Length</td>
<td align="left">2</td>
<td align="left">变量</td>
<td align="left">属性中以下字段的长度。</td>
</tr>
<tr class="odd">
<td align="left">P2P 设备地址</td>
<td align="left">6</td>
<td align="left">如 P2P 规范中所定义。</td>
<td align="left">用于唯一引用 P2P 设备的标识符。</td>
</tr>
<tr class="even">
<td align="left">Config 方法</td>
<td align="left">2</td>
<td align="left">如 P2P 规范中所定义。</td>
<td align="left"><p>此设备支持的 WSC 方法。</p>
<div class="alert">
<strong>注意</strong>   Config 方法字段中的字节排序应为大字节序。
</div>
<div>
 
</div></td>
</tr>
<tr class="odd">
<td align="left">主要设备类型</td>
<td align="left">8</td>
<td align="left">如 P2P 规范中所定义。</td>
<td align="left"><p>P2P 设备的主要设备类型。 仅包含 WSC 主设备类型属性的数据部分 (排除属性 ID 和长度字段) 。</p>
<div class="alert">
<strong>注意</strong>   "主要设备类型" 字段中的字节排序应为大字节序。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td align="left">设备功能位图</td>
<td align="left">1</td>
<td align="left">如 P2P 规范中所定义。</td>
<td align="left">指示 P2P 设备功能的一组参数。</td>
</tr>
<tr class="odd">
<td align="left">设备名称</td>
<td align="left">变量</td>
<td align="left">如 P2P 规范中所定义。</td>
<td align="left"><p>P2P 设备的友好名称。 包含整个 WSC 设备名称属性 TLV 格式。</p>
<div class="alert">
<strong>注意</strong>   设备名称字段中的字节排序应为大字节序。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

### <a name="p2p-oob-attributes"></a>P2P OOB 属性

| OOB 类型 (Hex)  | 说明               |
|----------------|---------------------------|
| 0x00           | OOB 状态                |
| 0x01           | OOB 设备信息           |
| 0x02           | OOB 设置信息     |
| 0x03           | OOB 组 ID              |
| 0x04           | OOB 侦听通道        |
| 0x05           | OOB 配置超时 |
| 0x06-0xDC      | 预留                  |
| 0xDD           | 供应商特定属性 |
| 0xDE-0xFF      | 预留                  |

 

### <a name="oob-provisioning-info-attribute-format"></a>OOB 设置信息属性格式

| 字段名称                   | 大小 (八进制)  | 值                   | 说明                                                                                                                                                             |
|------------------------------|---------------|-------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 属性 ID                 | 1             | 1                       | 标识 P2P OOB 特性的类型。 特定值在 *P2P OOB 属性* 表中定义。                                                                 |
| Length                       | 2             | 变量                | 属性中以下字段的长度。                                                                                                                        |
| 预配设置位图 | 1             | 变量                | 一组预配设置选项，定义为 *预配设置* 表。                                                                                   |
| 选择的配置方法       | 2             | 如 P2P 规范中所定义。 | 此 P2P 设备选择的用于预配的 WSC 方法。                                                                                                   |
| Pin 长度                   | 1             | 0 - 8                   | 以下 "PIN 数据" 字段中的字节数。 此字段设置为0表示没有额外的 PIN 数据。                                                                  |
| 固定数据                     | 变量      | n                       | 此字段是可选的。 仅当 PIN 长度字段不为0，并且包含表示要用于预配的 PIN 的八进制数组时，此字段才存在。 |

 

### <a name="provisioning-settings"></a>设置设置

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Bits (s) </th>
<th align="left">信息</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">0</td>
<td align="left">创建新组</td>
<td align="left">如果此预配信息用于使用目标 P2P 设备构成新组，则 "新建组位" 设置为 "1"。 否则，此设置信息用于加入现有组。</td>
</tr>
<tr class="even">
<td align="left">1</td>
<td align="left">强制执行组类型设置</td>
<td align="left">如果必须强制执行所需的组类型位，则 "强制组类型" 设置位设置为 1; 否则，所需的组类型位只是一个首选项。</td>
</tr>
<tr class="odd">
<td align="left">2</td>
<td align="left">所需的组类型</td>
<td align="left">如果所需的组类型为暂时性，则需要将所需的组类型设置为 0; 如果所需的组类型为永久，则应设置为1。</td>
</tr>
<tr class="even">
<td align="left">3 - 7</td>
<td align="left">预留</td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

### <a name="oob-configuration-timeout-attribute-format"></a>OOB 配置超时属性格式

| 字段名称                     | 大小 (八进制)  | 值   | 说明                                                                                                                                                        |
|--------------------------------|---------------|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 属性 ID                   | 1             | 5       | 标识 P2P OOB 特性的类型。 特定值在 *P2P OOB 属性* 表中定义。                                                            |
| Length                         | 2             | 1       | 属性中以下字段的长度。                                                                                                                   |
| 侦听器配置超时 | 1             | 0 - 255 | 此 P2P 设备在 OOB 数据传输之后等待 Wi-fi 直接通信的时间，单位为100毫秒。 )  (最大值为25.5 秒。 |

 

### <a name="windows-device-pairing-record"></a>Windows 设备配对记录

Windows 设备配对记录遵循 NDEF 规范。 它向 Windows 提供有关如何处理连接切换的其他信息选择消息。 必须根据 NDEF 规范指定 TNF 和 Type 字段。 以下其他字段将按顺序在 NDEF 记录的 "负载" 字段中列出。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">字段名称</th>
<th align="left">值</th>
<th align="left">长度值</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">TNF</td>
<td align="left">0x02</td>
<td align="left">3位</td>
<td align="left">后面的类型字段的格式。 在 RFC 2046 中定义的媒体类型。</td>
</tr>
<tr class="even">
<td align="left">类型</td>
<td align="left">"application/vnd.apple.mpegurl. ms-windows. devicepairing"</td>
<td align="left">0x28 字节</td>
<td align="left">我们为此方案定义的新类型字符串。</td>
</tr>
<tr class="odd">
<td align="left">MajorVersion</td>
<td align="left">0x1</td>
<td align="left">2 个字节</td>
<td align="left">主版本必须为0x1。</td>
</tr>
<tr class="even">
<td align="left">MinorVersion</td>
<td align="left">0x0</td>
<td align="left">2 个字节</td>
<td align="left">次要版本需要为0x0。</td>
</tr>
<tr class="odd">
<td align="left">Flags</td>
<td align="left">0x0 或0x01</td>
<td align="left">4 个字节</td>
<td align="left"><p>设置为0x0 可尝试所有传输。</p>
<p>设置为0x1，以按顺序尝试安装并在第一次成功后停止。 传输的首选项以备用运营商记录的顺序指示。</p>
<div class="alert">
<strong>注意</strong>   0x0002 到0x0064 的值是保留值。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td align="left">设备友好名称的长度</td>
<td align="left">设备友好名称字段的长度。</td>
<td align="left">1 个字节</td>
<td align="left">设备友好名称的长度。</td>
</tr>
<tr class="odd">
<td align="left">设备友好名称</td>
<td align="left">UTF-8 编码的字符串，最大为255字节。</td>
<td align="left">设备友好名称的长度</td>
<td align="left">设备的友好名称，该名称将显示在客户端上的同意 UI 中。</td>
</tr>
</tbody>
</table>

 

### <a name="wi-fi-direct-just-works-ceremony-static-connection-handover-tag-format"></a><a href="" id="wi-fi-direct--just-works--ceremony--static-connection-handover-tag-format"></a>Wi-fi Direct "只工作" 仪式，静态连接切换标记格式

例如，以下是 NFC 被动标记的典型实现。 这对应于静态连接切换事例，其中包含 Wi-fi 直接运营商记录、网络共享打印机和 ms 设备配对记录。

第一个表说明了标记的 Wi-fi 直接配对部分的格式。

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
<th align="left">内容</th>
<th align="left">长度</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">0</td>
<td align="left">0x91</td>
<td align="left">1</td>
<td align="left"><p>NDEF 记录标头：</p>
<p>MB = 1b，ME = 0b，CF = 0b，SR = 1b，IL = 0b，TNF = 001b</p></td>
</tr>
<tr class="even">
<td align="left">1</td>
<td align="left">0x02</td>
<td align="left">1</td>
<td align="left">记录类型长度：2个八位字节</td>
</tr>
<tr class="odd">
<td align="left">2</td>
<td align="left">0x0A</td>
<td align="left">1</td>
<td align="left">记录类型长度：10个八进制数</td>
</tr>
<tr class="even">
<td align="left">3</td>
<td align="left">0x48 0x73</td>
<td align="left">2</td>
<td align="left">记录类型： "Hs"</td>
</tr>
<tr class="odd">
<td align="left">5</td>
<td align="left">0x12</td>
<td align="left">1</td>
<td align="left">版本号：主编号 = 1，小调 = 2</td>
</tr>
<tr class="even">
<td align="left">6</td>
<td align="left">0xD1</td>
<td align="left">1</td>
<td align="left"><p>NDEF 记录标头：</p>
<p>MB = 1b，ME = 1b，CF = 0b，SR = 1b，IL = 0b，TNF = 001b</p></td>
</tr>
<tr class="odd">
<td align="left">7</td>
<td align="left">0x02</td>
<td align="left">1</td>
<td align="left">记录类型长度：2个八位字节</td>
</tr>
<tr class="even">
<td align="left">8</td>
<td align="left">0x04</td>
<td align="left">1</td>
<td align="left">负载长度：4个字节</td>
</tr>
<tr class="odd">
<td align="left">9</td>
<td align="left">0x61 0x63</td>
<td align="left">2</td>
<td align="left">记录类型： "ac"</td>
</tr>
<tr class="even">
<td align="left">11</td>
<td align="left">0x01</td>
<td align="left">1</td>
<td align="left">电信公司标志： CPS = 1，"主动"</td>
</tr>
<tr class="odd">
<td align="left">12</td>
<td align="left">0x01</td>
<td align="left">1</td>
<td align="left">电信公司数据引用长度：1个八进制数</td>
</tr>
<tr class="even">
<td align="left">13</td>
<td align="left">0x30</td>
<td align="left">1</td>
<td align="left">电信公司数据引用： "0"</td>
</tr>
<tr class="odd">
<td align="left">14</td>
<td align="left">0x00</td>
<td align="left">1</td>
<td align="left">辅助数据引用计数：0</td>
</tr>
<tr class="even">
<td align="left">15</td>
<td align="left">0x1A</td>
<td align="left">1</td>
<td align="left"><p>NDEF 记录标头：</p>
<p>MB = 0b，ME = 0b，CF = 0b，SR = 1b，IL = 1b，TNF = 010b</p></td>
</tr>
<tr class="odd">
<td align="left">16</td>
<td align="left">0x22</td>
<td align="left">1</td>
<td align="left">记录类型名称长度：34字节</td>
</tr>
<tr class="even">
<td align="left">17</td>
<td align="left">0x3E</td>
<td align="left">1</td>
<td align="left">负载长度：62个字节</td>
</tr>
<tr class="odd">
<td align="left">18</td>
<td align="left">0x01</td>
<td align="left">1</td>
<td align="left">Id 长度：1个八进制数</td>
</tr>
<tr class="even">
<td align="left">19</td>
<td align="left"><p>0x61 0x70 0x70 0x6C</p>
<p>0x69 0x63 0x61 0x74</p>
<p>0x69 0x6F 0x6E 0x2F</p>
<p>0x76 0x6E 0x64 0x2E</p>
<p>0x6D 0x73 0x2D 0x77</p>
<p>0x69 0x6E 0x64 0x6F</p>
<p>0x77 0x73 0x2E 0x77</p>
<p>0x66 0x64 0x2E 0x6F</p>
<p>0x6F 0x62</p></td>
<td align="left">34</td>
<td align="left">记录类型名称： "application/vnd.apple.mpegurl. ms-windows"</td>
</tr>
<tr class="odd">
<td align="left">53</td>
<td align="left">0x30</td>
<td align="left">1</td>
<td align="left">Id： "0"</td>
</tr>
<tr class="even">
<td align="left">54</td>
<td align="left">0x3E 0x00</td>
<td align="left">2</td>
<td align="left"><p>Wi-fi Direct OOB 数据长度：62个字节。 长度作为无符号短格式读取，并且包含</p>
<p>的。 包括2长度的八进制数。 此值必须存储为小字节序格式。</p></td>
</tr>
<tr class="odd">
<td align="left">56</td>
<td align="left">0x02，0x00</td>
<td align="left">2</td>
<td align="left">标头长度：2个八位字节</td>
</tr>
<tr class="even">
<td align="left">58</td>
<td align="left">0x10</td>
<td align="left">1</td>
<td align="left">版本：0x10</td>
</tr>
<tr class="odd">
<td align="left">59</td>
<td align="left">0x00</td>
<td align="left">1</td>
<td align="left">OOB 类型： 0x00 (单向) </td>
</tr>
<tr class="even">
<td align="left">60</td>
<td align="left">0x01</td>
<td align="left">1</td>
<td align="left">特性： 0x01 (设备信息特性) </td>
</tr>
<tr class="odd">
<td align="left">61</td>
<td align="left">0x22 0x00</td>
<td align="left">2</td>
<td align="left">设备信息长度：34字节</td>
</tr>
<tr class="even">
<td align="left">63</td>
<td align="left"><p>0x01 0x23 0x34 赋0xab</p>
<p>0xcd 0xef</p></td>
<td align="left">6</td>
<td align="left">Wi-fi Direct P2P 设备 MAC 地址： "01:23:34<span class="emoji" shortCode="ab">🆎</span>cd： ef"</td>
</tr>
<tr class="odd">
<td align="left">69</td>
<td align="left">0x01 0x00</td>
<td align="left">2</td>
<td align="left">配置类型</td>
</tr>
<tr class="even">
<td align="left">71</td>
<td align="left"><p>0x00 0x01 0x00 0x50</p>
<p>0xF2 0x00 0x00 0x00</p></td>
<td align="left">8</td>
<td align="left">主要设备类型</td>
</tr>
<tr class="odd">
<td align="left">79</td>
<td align="left">0x12</td>
<td align="left">1</td>
<td align="left">功能</td>
</tr>
<tr class="even">
<td align="left">80</td>
<td align="left">0x10 0x11</td>
<td align="left">2</td>
<td align="left">属性：设备名称</td>
</tr>
<tr class="odd">
<td align="left">82</td>
<td align="left">0x00 0x0d</td>
<td align="left">2</td>
<td align="left">设备名称长度：13个八进制数</td>
</tr>
<tr class="even">
<td align="left">84</td>
<td align="left"><p>0x43 0x6f 0x6e 0x74</p>
<p>0x6f 0x73 0x6f 0x20</p>
<p>0x4d 0x6f 0x75 0x73</p>
<p>0x65</p></td>
<td align="left">13</td>
<td align="left"><p>Utf-8 格式的设备友好名称。 请注意，没有 NULL 终止字符和 UTF-8</p>
<p>可以是每个字符一个或两个字节。 此示例读取 "Contoso 鼠标"</p></td>
</tr>
<tr class="odd">
<td align="left">97</td>
<td align="left">0x02</td>
<td align="left">1</td>
<td align="left">属性：设置信息</td>
</tr>
<tr class="even">
<td align="left">98</td>
<td align="left">0x0c 0x00</td>
<td align="left">2</td>
<td align="left">设置信息长度：12个八进制数</td>
</tr>
<tr class="odd">
<td align="left">100</td>
<td align="left">0x07</td>
<td align="left">1</td>
<td align="left">设置位图：新建组，强制持久</td>
</tr>
<tr class="even">
<td align="left">101</td>
<td align="left">0x01 0x00</td>
<td align="left">2</td>
<td align="left">Config 方法： pin 输入</td>
</tr>
<tr class="odd">
<td align="left">103</td>
<td align="left">0x08</td>
<td align="left">1</td>
<td align="left">Pin 长度：8个八进制数</td>
</tr>
<tr class="even">
<td align="left">104</td>
<td align="left"><p>0x01 0x02 0x03 0x04</p>
<p>0x05 0x06 0x07 0x08</p></td>
<td align="left">8</td>
<td align="left">Pin： "12345678"</td>
</tr>
<tr class="odd">
<td align="left">112</td>
<td align="left">0x05</td>
<td align="left">1</td>
<td align="left">属性：配置超时信息</td>
</tr>
<tr class="even">
<td align="left">113</td>
<td align="left">0x01 0x00</td>
<td align="left">2</td>
<td align="left">配置超时长度</td>
</tr>
<tr class="odd">
<td align="left">115</td>
<td align="left">0x64</td>
<td align="left">1</td>
<td align="left">10秒，以100毫秒为单位</td>
</tr>
</tbody>
</table>

 

此第二个表说明了标记的网络打印机配对部分的格式。

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
<th align="left">内容</th>
<th align="left">长度</th>
<th align="left">解释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">116</td>
<td align="left">0x12</td>
<td align="left">1</td>
<td align="left"><p>NDEF 记录标头：</p>
<p>MB = 0b，ME = 0b，CF = 0b，SR = 1b，IL = 0b，TNF = 010b</p></td>
</tr>
<tr class="even">
<td align="left">117</td>
<td align="left">0x29</td>
<td align="left">1</td>
<td align="left">类型长度字段</td>
</tr>
<tr class="odd">
<td align="left">118</td>
<td align="left">0x19</td>
<td align="left">1</td>
<td align="left">负载长度字段</td>
</tr>
<tr class="even">
<td align="left">119</td>
<td align="left"><p>0x61 0x70 0x70 0x6c</p>
<p>0x69 0x63 0x61 0x74</p>
<p>0x69 0x6f 0x6e 0x2f</p>
<p>0x76 0x6e 0x64 0x2e</p>
<p>0x6d 0x73 0x2d 0x77</p>
<p>0x69 0x6e 0x64 0x6f</p>
<p>0x77 0x73 0x2e 0x6e</p>
<p>0x77 0x70 0x72 0x69</p>
<p>0x6e 0x74 0x69 0x6e</p>
<p>0x67 0x2e 0x6f 0x6f</p>
<p>0x62</p></td>
<td align="left">41</td>
<td align="left">记录类型名称： "application/vnd.apple.mpegurl. ms-windows. nwprinting"</td>
</tr>
<tr class="odd">
<td align="left">160</td>
<td align="left"><p>0x5c 0x5c 0x70 0x72</p>
<p>0x69 0x6e 0x74 0x53</p>
<p>0x65 0x72 0x76 0x65</p>
<p>0x72 0x5c 0x70 0x72</p>
<p>0x69 0x6e 0x74 0x65</p>
<p>0x72 0x4e 0x61 0x6d</p>
<p>0x65</p></td>
<td align="left">25</td>
<td align="left">打印机名称： "\printServer\printerName"</td>
</tr>
</tbody>
</table>

 

此第三个表说明了标记的 MS 设备配对部分的格式。

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
<th align="left">内容</th>
<th align="left">长度</th>
<th align="left">解释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">185</td>
<td align="left">0x52</td>
<td align="left">1</td>
<td align="left"><p>NDEF 记录标头：</p>
<p>MB = 0b，ME = 1b，CF = 0b，SR = 1b，IL = 0b，TNF = 010b</p></td>
</tr>
<tr class="even">
<td align="left">186</td>
<td align="left">0x28</td>
<td align="left">1</td>
<td align="left">类型长度字段</td>
</tr>
<tr class="odd">
<td align="left">187</td>
<td align="left">0x15</td>
<td align="left">1</td>
<td align="left">负载长度字段</td>
</tr>
<tr class="even">
<td align="left">188</td>
<td align="left"><p>0x61 0x70 0x70 0x6c</p>
<p>0x69 0x63 0x61 0x74</p>
<p>0x69 0x6f 0x6e 0x2f</p>
<p>0x76 0x6e 0x64 0x2e</p>
<p>0x6d 0x73 0x2d 0x77</p>
<p>0x69 0x6e 0x64 0x6f</p>
<p>0x77 0x73 0x2e 0x64</p>
<p>0x65 0x76 0x69 0x63</p>
<p>0x65 0x70 0x61 0x69</p>
<p>0x72 0x69 0x6E 0x67</p></td>
<td align="left">40</td>
<td align="left">记录类型名称： "application/vnd.apple.mpegurl. ms-windows. devicepairing"</td>
</tr>
<tr class="odd">
<td align="left">228</td>
<td align="left">0x00 0x01 0x00 0x00</td>
<td align="left">4</td>
<td align="left">版本：主编 = 1，小调 = 0</td>
</tr>
<tr class="even">
<td align="left">232</td>
<td align="left">0x00</td>
<td align="left">1</td>
<td align="left">Flags：设置为0，尝试所有传输</td>
</tr>
<tr class="odd">
<td align="left">233</td>
<td align="left">0x0F</td>
<td align="left">1</td>
<td align="left">设备友好名称的长度</td>
</tr>
<tr class="even">
<td align="left">234</td>
<td align="left"><p>0x43 0x6f 0x6e 0x74</p>
<p>0x6f 0x73 0x6f 0x20</p>
<p>0x50 0x72 0x69 0x6e</p>
<p>0x74 0x65 0x72</p></td>
<td align="left">15</td>
<td align="left">向用户显示的设备友好名称： "Contoso Printer"</td>
</tr>
</tbody>
</table>

 

## <a name="wi-fi-direct-connectivity-requirements"></a>Wi-fi 直接连接要求


设备和客户端必须打开 Wi-fi 无线电。 否则，配对将会失败。

## <a name="handling-edge-cases"></a>处理边缘事例


如果用户之前已经配对了某个设备，但随后从设备列表中手动删除了该设备，再次点击会导致尝试安装或配对。

如果用户进入传动的范围，但随后在传输带外 (OOB) 信息之前突然离开，则设备可能会变为可连接，但 PC 不会查找设备。 在这种情况下，PC 中将不会有任何许可 UI，用户将需要再次点击。 如果设备再次再次被再次发现，则它应保持可检测的，并应重置超时期限。

对于 Wi-fi Direct 设备，如果 Wi-fi 无线电关闭，安装将不会成功。

如果用户几乎同时点击两个设备，则只会尝试使用第一次接收的 OOB 信息配对。

尝试在运行不支持点击以进行设置或点击以进行重新连接的操作系统的系统上点击设备可能会导致设备进入可连接模式，但不会发生配对。 用户需要使用为蓝牙提供的配对 UI，并使用 "配对" 按钮来启动配对。

 

 
## <a name="related-topics"></a>相关主题
 [NFC 设备驱动程序接口 (DDI) 参考](/windows-hardware/drivers/ddi/index)  
