---
title: Wi-fi direct 配对实现
description: 本部分提供了设计指导原则和外围设备参与点击和设置和点击和重新连接要求用例。
ms.assetid: 1B729E9F-DF9F-4263-9F0B-5EDCF817D2C3
keywords:
- NFC
- 附近通信
- 近程
- 邻近附近
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17a4387f395ec44fcc2d63e6bc8d76a9b874e596
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524702"
---
# <a name="wi-fi-direct-pairing-implementation"></a>Wi-fi direct 配对实现


本部分提供了设计指导原则和外围设备参与点击和设置和点击和重新连接要求用例。

**请注意**  配对实现本主题中所述的评分配对到仅限打印机设备的当前支持在 Windows 8.1 中。

 

**请注意**  Windows 10 还通过 Wi-fi 联盟的 Wi-fi P2P 运营商配置记录的 Wi-Fi Direct 静态连接移交到支持 NFC。 有关详细信息，请参阅[Wi-fi 联盟](http://www.wi-fi.org)。

 

## <a name="peripheral-wi-fi-direct-device-pairing"></a>外围设备的 Wi-Fi Direct 设备配对


分流期间 NFP 接收来自连接设备配对的信息。 NFP 将配对信息传递给 Windows。 Wi-Fi Direct 设备遵循的 Wi-fi 联盟带外 (OOB) 配对过程和 NFC 论坛建议。 Windows 依赖于一种专有配对消息定义如下。

Windows 会提示用户同意，然后如果给定了它，则 Windows 将尝试连接到每个地址，按顺序排列，直到成功为止。 没有与 pc NFP 提供程序与连接方设备之间无需进一步交互。

使用 NFC 作为示例，通过将配对信息存储在静态或被动 NFC 标记 （也可能使用活动 NFC 标记在静态仿真模式下） 中实现单向安装。 Windows 对此订阅配对信息。 在 PC 上的 nfc 的 NFP 提供程序从标记接收连接信息，并将此传递到作为订阅者的 Windows。 收到的连接信息，Windows 执行实际安装中外设备使用设备类的特定技术。

## <a name="interoperability-requirements"></a>互操作性要求


若要确保 NFP 提供程序之间的互操作性，应在特定于提供程序的消息格式封装配对信息。

如本文档中其他地方所述，有针对邻近技术以外的其他支持 NFC 的 NFP 提供程序的特定要求。

Windows 要求支持 NFC 的 NFP 提供商支持特定定义 NFC 论坛 – 机制传达 Wi-Fi Direct OOB 配对单向配对的信息。 NDEF 消息包含 TNF 字段值 0x01 的第一条记录和等于"Hs"的类型字段和其他电话公司记录指向 Wi-Fi Direct 运营商配置记录。 在此方法中，将使用仅 NDEF 记录的有效负载。

## <a name="unidirectional-pairing-using-nfc-for-wi-fi-direct"></a>单向配对使用 NFC Wi-Fi Direct


本部分提供有关 NFC、 Wi-Fi Direct 和 Windows 如何协同工作以支持 Wi-Fi Direct 设备，例如打印机为单向无线配对的更多详细信息。

### <a name="nfp-provider-references"></a>NFP 提供程序的引用

Wi-Fi Direct 配对通过 NFC 论坛标准化连接移交选择消息类型。 下图概述了如何将连接移交选择消息应用 Wi-Fi Direct 设备配对，特别是 NDEF 记录 3 和 4。 移交选择消息描述一个或多个"ac"备用运营商"记录。 这些记录按顺序遵循移交选择记录，每个具有明确定义的类型。 最后，消息将包含 Microsoft 定义的设备配对记录它为 Windows 提供了有关如何处理配对操作的信息。

![连接移交选择消息](images/handover.png)

### <a name="wi-fi-direct-device-pairing-message"></a>Wi-Fi Direct 设备配对消息

在按照这些示例用例，NFC 类型 2 标记用作演示示例。 如果需要使用不同的 NFC 标记类型，必须根据该标记定义正确封装 NDEF 消息。

| 字段                 | 值                                            | 描述                                                               |
|-----------------------|--------------------------------------------------|---------------------------------------------------------------------------|
| TNF                   | 0x02                                             | 遵循类型字段的格式。 媒体类型 RFC 2046 中定义。 |
| 在任务栏的搜索框中键入                  | 'application/vnd.ms-windows.wfd.oob'             | 我们为此方案中定义新类型字符串。                              |
| OOB 数据的大小      | WORD                                             | 最多 64 KB 的 OOB 数据支持。                                        |
| Wi-Fi Direct OOB 数据 | &lt;指示由上一个字段大小的 blob&gt; | Wi-Fi Direct OOB 数据定义如下。                                   |

 

### <a name="wi-fi-direct-oob-format"></a>Wi-Fi Direct OOB 格式

下表介绍 WiFi 直接 OOB 数据的格式。 OOB 单向数据可能会传输任何单向 P2P OOB 设备。

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
<th align="left">注意</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>OOB 标头</p>
<p>请参阅 OOB 标头属性设置表格格式。</p></td>
<td align="left">不适用</td>
<td align="left">必需</td>
<td align="left">OOB 标头属性应会出现在 P2P OOB 数据 blob 并 OOB 类型值设置为"OOB 单向预配 Data"。</td>
</tr>
<tr class="even">
<td align="left"><p>OOB 设备信息</p>
<p>请参阅 OOB 设备信息属性格式表。</p></td>
<td align="left">1</td>
<td align="left">必需</td>
<td align="left">此属性必须存在。 它提供有关此 P2P 设备的信息。</td>
</tr>
<tr class="odd">
<td align="left"><p>OOB 预配信息</p>
<p></p></td>
<td align="left">2</td>
<td align="left">必需</td>
<td align="left">此属性必须存在。 它提供此 P2P 设备应使用的预配信息。</td>
</tr>
<tr class="even">
<td align="left"><p>OOB 配置超时</p>
<p></p></td>
<td align="left">5</td>
<td align="left">必需</td>
<td align="left">此属性必须存在。 它提供了有关此 P2P 设备将等待多长的响应通过 Wi-Fi Direct 的信息。</td>
</tr>
</tbody>
</table>

 

### <a name="oob-header-attribute-format"></a>OOB 标头属性格式

| 字段名称        | 大小 （八进制） | 值    | 描述                                                                                                    |
|-------------------|---------------|----------|----------------------------------------------------------------------------------------------------------------|
| 总数据长度 | 2             | 变量 | 整个 OOB 数据 Blob （包括标头） 的长度。                                                             |
| 长度            | 2             | 变量 | OOB 标头中的以下字段的长度。                                                                  |
| 版本           | 1             | 0x10     | 标识此 P2P OOB 记录的版本值。                                                          |
| OOB 类型          | 1             | 变量 | 标识的 OOB 事务类型的值。 中定义的特定值*OOB 事务类型*表。 |
| OUI               | 0 或 3        | 变量 | 特定于供应商 OUI。 这是一个可选值。 必须仅在供应商特定 OOB 类型时存在。         |
| OUI 类型          | 0 或 1        | 变量 | 特定于供应商的类型。 这是一个可选值。 必须仅在供应商特定 OOB 类型时存在。        |

 

### <a name="oob-transaction-types"></a>OOB 事务类型

| OOB 类型 （十六进制） | 描述                          |
|----------------|--------------------------------------|
| 0x00           | OOB 单向预配数据 |
| 0x01           | OOB 设置侦听器数据       |
| 0x02           | OOB 预配连接器数据      |
| 0x03           | OOB Reinvoke 数据                    |
| 0x04-0xDC      | 保留                             |
| 0xDD           | 特定于供应商                      |
| 0xDE-0xFF      | 保留                             |

 

### <a name="oob-device-info-attribute-format"></a>OOB 设备信息属性格式

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
<th align="left">大小 （八进制）</th>
<th align="left">值</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">属性 ID</td>
<td align="left">1</td>
<td align="left">1</td>
<td align="left">标识 P2P OOB 属性的类型。 中定义的特定值<em>P2P OOB 属性</em>表。</td>
</tr>
<tr class="even">
<td align="left">长度</td>
<td align="left">2</td>
<td align="left">变量</td>
<td align="left">该属性中的以下字段的长度。</td>
</tr>
<tr class="odd">
<td align="left">P2P 设备地址</td>
<td align="left">6</td>
<td align="left">P2P 规范中定义。</td>
<td align="left">用于唯一引用 P2P 设备的标识符。</td>
</tr>
<tr class="even">
<td align="left">配置方法</td>
<td align="left">2</td>
<td align="left">P2P 规范中定义。</td>
<td align="left"><p>此设备支持的 WSC 方法。</p>
<div class="alert">
<strong>请注意</strong>  应 big endian 字节顺序配置方法字段中。
</div>
<div>
 
</div></td>
</tr>
<tr class="odd">
<td align="left">主要设备类型</td>
<td align="left">8</td>
<td align="left">P2P 规范中定义。</td>
<td align="left"><p>P2P 设备的主要设备类型。 包含 （不包括属性 ID 和长度字段） 的 WSC 主设备类型属性的数据部分。</p>
<div class="alert">
<strong>请注意</strong>  应 big endian 字节顺序在主要设备类型字段中。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td align="left">设备功能的位图</td>
<td align="left">1</td>
<td align="left">P2P 规范中定义。</td>
<td align="left">一组参数，该值指示 P2P 设备的功能。</td>
</tr>
<tr class="odd">
<td align="left">设备名称</td>
<td align="left">变量</td>
<td align="left">P2P 规范中定义。</td>
<td align="left"><p>P2P 设备的友好名称。 包含整个 WSC 设备名称属性 TLV 格式。</p>
<div class="alert">
<strong>请注意</strong>  应 big endian 字节顺序在设备名称字段中。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

### <a name="p2p-oob-attributes"></a>P2P OOB 属性

| OOB 类型 （十六进制） | 描述               |
|----------------|---------------------------|
| 0x00           | OOB 状态                |
| 0x01           | OOB 设备信息           |
| 0x02           | OOB 预配信息     |
| 0x03           | OOB 组 ID              |
| 0x04           | OOB 侦听通道        |
| 0x05           | OOB 配置超时 |
| 0x06-0xDC      | 保留                  |
| 0xDD           | 供应商特定属性 |
| 0xDE-0xFF      | 保留                  |

 

### <a name="oob-provisioning-info-attribute-format"></a>OOB 预配信息属性格式

| 字段名称                   | 大小 （八进制） | 值                   | 描述                                                                                                                                                             |
|------------------------------|---------------|-------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 属性 ID                 | 1             | 1                       | 标识 P2P OOB 属性的类型。 中定义的特定值*P2P OOB 属性*表。                                                                 |
| 长度                       | 2             | 变量                | 该属性中的以下字段的长度。                                                                                                                        |
| 预配设置位图 | 1             | 变量                | 预配设置选项，定义一组*预配设置*表。                                                                                   |
| 所选的配置方法       | 2             | P2P 规范中定义。 | 预配此 P2P 设备选择了 WSC 方法。                                                                                                   |
| Pin 长度                   | 1             | 0 - 8                   | 以下固定数据字段中的字节数。 此字段设置为 0 指示没有其他的 PIN 数据。                                                                  |
| Pin 数据                     | 变量      | n                       | 此字段是可选字段。 此字段才存在固定长度字段不是 0，并包含表示要用于预配一个 PIN 八位字节的数组。 |

 

### <a name="provisioning-settings"></a>预配设置

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">位 (s)</th>
<th align="left">信息</th>
<th align="left">注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">0</td>
<td align="left">创建新的组</td>
<td align="left">如果此设置的信息适用于与目标 P2P 设备形成新的组，创建新组位设置为 1。 否则，此设置的信息是加入现有组。</td>
</tr>
<tr class="even">
<td align="left">1</td>
<td align="left">强制实施组键入的设置</td>
<td align="left">如果必须强制实施所需的组类型位的强制实施组类型设置位设置为 1、 组; 否则为所需类型的位是只需首选项。</td>
</tr>
<tr class="odd">
<td align="left">2</td>
<td align="left">所需的组类型</td>
<td align="left">如果所需的组类型是暂时的并且应设置为 1，如果所需的组类型是持久性的所需组类型位应设置为 0。</td>
</tr>
<tr class="even">
<td align="left">3 - 7</td>
<td align="left">保留</td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

### <a name="oob-configuration-timeout-attribute-format"></a>OOB 配置超时属性格式

| 字段名称                     | 大小 （八进制） | 值   | 描述                                                                                                                                                        |
|--------------------------------|---------------|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 属性 ID                   | 1             | 5       | 标识 P2P OOB 属性的类型。 中定义的特定值*P2P OOB 属性*表。                                                            |
| 长度                         | 2             | 1       | 该属性中的以下字段的长度。                                                                                                                   |
| 侦听器配置超时 | 1             | 0 - 255 | 此 P2P 设备将花费等待 Wi-Fi Direct 通信后 OOB 数据传输、 100 毫秒为单位的时间量。 （最大 25.5 秒为单位）。 |

 

### <a name="windows-device-pairing-record"></a>Windows 设备配对记录

Windows 设备配对记录遵循 NDEF 规范。 它提供到 Windows 有关如何处理连接移交选择消息的其他信息。 必须根据 NDEF 规范指定 TNF 和类型字段。 下面的其他字段 NDEF 记录的有效负载字段中，将按顺序列出。

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
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">TNF</td>
<td align="left">0x02</td>
<td align="left">3 位</td>
<td align="left">遵循类型字段的格式。 媒体类型 RFC 2046 中定义。</td>
</tr>
<tr class="even">
<td align="left">在任务栏的搜索框中键入</td>
<td align="left">&#39;application/vnd.ms-windows.devicepairing&#39;</td>
<td align="left">0x28 字节</td>
<td align="left">我们为此方案中定义新类型字符串。</td>
</tr>
<tr class="odd">
<td align="left">主要版本</td>
<td align="left">0x1</td>
<td align="left">2 个字节</td>
<td align="left">所需的主版本为 0x1。</td>
</tr>
<tr class="even">
<td align="left">MinorVersion</td>
<td align="left">0x0</td>
<td align="left">2 个字节</td>
<td align="left">次要版本需为 0x0。</td>
</tr>
<tr class="odd">
<td align="left">Flags</td>
<td align="left">0x0 或 0x01</td>
<td align="left">4 个字节</td>
<td align="left"><p>设为 0x0 尝试所有传输。</p>
<p>设置为 0x1，按顺序尝试安装并在第一个成功后停止。 由另一个电话公司记录的序列表示传输有关的首选项。</p>
<div class="alert">
<strong>请注意</strong>  值通过 0x0064 0x0002 已被保留。
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
<td align="left">Utf-8 编码的字符串最多 255 个字节。</td>
<td align="left">设备友好名称的长度</td>
<td align="left">设备友好名称，它将显示在同意 UI 客户端上。</td>
</tr>
</tbody>
</table>

 

### <a href="" id="wi-fi-direct--just-works--ceremony--static-connection-handover-tag-format"></a>Wi-Fi Direct"Just Works"繁琐程度，静态连接移交标记格式

例如，下面是 NFC 被动标记的典型实现。 这对应于具有 Wi-Fi Direct 的运营商记录、 网络共享打印机和 ms 设备配对记录的静态连接移交事例。

此第一个表说明了 Wi-Fi Direct 配对标记的部分的格式。

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
<p>MB=1b, ME=0b, CF=0b, SR=1b, IL=0b, TNF=001b</p></td>
</tr>
<tr class="even">
<td align="left">1</td>
<td align="left">0x02</td>
<td align="left">1</td>
<td align="left">记录类型长度：2 个字节</td>
</tr>
<tr class="odd">
<td align="left">2</td>
<td align="left">0x0A</td>
<td align="left">1</td>
<td align="left">记录类型长度：10 个八位字节</td>
</tr>
<tr class="even">
<td align="left">3</td>
<td align="left">0x48 0x73</td>
<td align="left">2</td>
<td align="left">记录类型：“Hs”</td>
</tr>
<tr class="odd">
<td align="left">5</td>
<td align="left">0x12</td>
<td align="left">1</td>
<td align="left">版本号：主要 = 1，次要 = 2</td>
</tr>
<tr class="even">
<td align="left">6</td>
<td align="left">0xD1</td>
<td align="left">1</td>
<td align="left"><p>NDEF 记录标头：</p>
<p>MB=1b, ME=1b, CF=0b, SR=1b, IL=0b, TNF=001b</p></td>
</tr>
<tr class="odd">
<td align="left">7</td>
<td align="left">0x02</td>
<td align="left">1</td>
<td align="left">记录类型长度：2 个字节</td>
</tr>
<tr class="even">
<td align="left">8</td>
<td align="left">0x04</td>
<td align="left">1</td>
<td align="left">有效负载长度：4 个字节</td>
</tr>
<tr class="odd">
<td align="left">9</td>
<td align="left">0x61 0x63</td>
<td align="left">2</td>
<td align="left">记录类型:"ac"</td>
</tr>
<tr class="even">
<td align="left">11</td>
<td align="left">0x01</td>
<td align="left">1</td>
<td align="left">运营商的标志：CPS=1, &quot;active&quot;</td>
</tr>
<tr class="odd">
<td align="left">12</td>
<td align="left">0x01</td>
<td align="left">1</td>
<td align="left">运营商的数据引用长度：1 个字节</td>
</tr>
<tr class="even">
<td align="left">13</td>
<td align="left">0x30</td>
<td align="left">1</td>
<td align="left">运营商的数据引用：“0”</td>
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
<p>MB=0b, ME=0b, CF=0b, SR=1b, IL=1b, TNF=010b</p></td>
</tr>
<tr class="odd">
<td align="left">16</td>
<td align="left">0x22</td>
<td align="left">1</td>
<td align="left">记录类型名称的长度：34 个八位字节</td>
</tr>
<tr class="even">
<td align="left">17</td>
<td align="left">0x3E</td>
<td align="left">1</td>
<td align="left">有效负载长度：62 八位字节</td>
</tr>
<tr class="odd">
<td align="left">18</td>
<td align="left">0x01</td>
<td align="left">1</td>
<td align="left">Id 长度：1 个字节</td>
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
<td align="left">记录类型名称： &#39;application/vnd.ms-windows.wfd.oob&#39;</td>
</tr>
<tr class="odd">
<td align="left">53</td>
<td align="left">0x30</td>
<td align="left">1</td>
<td align="left">id:“0”</td>
</tr>
<tr class="even">
<td align="left">54</td>
<td align="left">0x3E 0x00</td>
<td align="left">2</td>
<td align="left"><p>Wi-Fi Direct OOB 数据长度：62 八位字节。 长度读取为无符号短整数和是包容性的</p>
<p>整个 blob。 包括 2 个长度八位字节。 此值必须存储在 little-endian 格式。</p></td>
</tr>
<tr class="odd">
<td align="left">56</td>
<td align="left">0x02，0x00</td>
<td align="left">2</td>
<td align="left">标头长度：2 个字节</td>
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
<td align="left">OOB 类型：0x00 （单向）</td>
</tr>
<tr class="even">
<td align="left">60</td>
<td align="left">0x01</td>
<td align="left">1</td>
<td align="left">属性：0x01 （设备信息属性）</td>
</tr>
<tr class="odd">
<td align="left">61</td>
<td align="left">0x22 0x00</td>
<td align="left">2</td>
<td align="left">设备信息长度：34 个八位字节</td>
</tr>
<tr class="even">
<td align="left">63</td>
<td align="left"><p>0x01 0x23 0x34 0xab</p>
<p>0xcd 0xef</p></td>
<td align="left">6</td>
<td align="left">Wi-Fi Direct P2P 设备 MAC 地址：“01:23:34<span class="emoji" shortCode="ab">🆎</span>cd:ef”</td>
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
<td align="left">设备名称的长度：13 个八位字节</td>
</tr>
<tr class="even">
<td align="left">84</td>
<td align="left"><p>0x43 0x6f 0x6e 0x74</p>
<p>0x6f 0x73 0x6f 0x20</p>
<p>0x4d 0x6f 0x75 0x73</p>
<p>0x65</p></td>
<td align="left">13</td>
<td align="left"><p>在 utf-8 中的设备友好名称。 请注意，有没有 NULL 终止字符和该 utf-8</p>
<p>可能是每个字符的一个或两个字节。 此示例读取"Contoso Mouse"</p></td>
</tr>
<tr class="odd">
<td align="left">97</td>
<td align="left">0x02</td>
<td align="left">1</td>
<td align="left">属性： 预配信息</td>
</tr>
<tr class="even">
<td align="left">98</td>
<td align="left">0x0c 0x00</td>
<td align="left">2</td>
<td align="left">预配信息长度：12 个八位字节</td>
</tr>
<tr class="odd">
<td align="left">100</td>
<td align="left">0x07</td>
<td align="left">1</td>
<td align="left">设置位图： 新组中，强制执行持久性</td>
</tr>
<tr class="even">
<td align="left">101</td>
<td align="left">0x01 0x00</td>
<td align="left">2</td>
<td align="left">配置方法： 将固定项</td>
</tr>
<tr class="odd">
<td align="left">103</td>
<td align="left">0x08</td>
<td align="left">1</td>
<td align="left">Pin 长度：8 个字节</td>
</tr>
<tr class="even">
<td align="left">104</td>
<td align="left"><p>0x01 0x02 0x03 0x04</p>
<p>0x05 0x06 0x07 0x08</p></td>
<td align="left">8</td>
<td align="left">Pin:“12345678”</td>
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
<td align="left">10 秒，以 100 毫秒为单位</td>
</tr>
</tbody>
</table>

 

此第二个表说明了该标记的网络打印机配对部分的格式。

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
<p>MB=0b,ME=0b, CF=0b, SR=1b, IL=0b,TNF=010b</p></td>
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
<td align="left">有效负载长度字段</td>
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
<td align="left">记录类型名称:"application/vnd.ms-windows.nwprinting.oob"</td>
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
<td align="left">打印机名称:"\printServer\printerName&quot;</td>
</tr>
</tbody>
</table>

 

此第三个表说明了该标记的 MS 设备配对部分的格式。

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
<p>MB=0b, ME=1b, CF=0b, SR=1b, IL=0b,TNF=010b</p></td>
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
<td align="left">有效负载长度字段</td>
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
<td align="left">记录类型名称:"application/vnd.ms-windows.devicepairing"</td>
</tr>
<tr class="odd">
<td align="left">228</td>
<td align="left">0x00 0x01 0x00 0x00</td>
<td align="left">4</td>
<td align="left">版本：主要 = 1，次要 = 0</td>
</tr>
<tr class="even">
<td align="left">232</td>
<td align="left">0x00</td>
<td align="left">1</td>
<td align="left">Flags：设置为 0，请尝试所有传输</td>
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
<td align="left">向用户显示的设备友好名称："Contoso 打印机"</td>
</tr>
</tbody>
</table>

 

## <a name="wi-fi-direct-connectivity-requirements"></a>Wi-Fi Direct 连接要求


设备和客户端必须具有的 Wi-fi 无线电开启。 如果没有，配对将会失败。

## <a name="handling-edge-cases"></a>处理边缘情况


如果用户以前已配对的设备，但手动然后从设备列表中删除设备，再次点击会尝试安装或配对。

如果用户输入时闭合的范围，但然后突然离开传输的带外 (OOB) 信息之前，设备可能会变得可连接但 PC 不会查找设备。 在这种情况下，将从电脑的用户界面不同意，并且用户将需要再次点击。 如果设备已发现，再次点击时，它应保留可发现，并应重置的超时期限。

对于 Wi-Fi Direct 设备，如果 Wi-fi 无线电关闭然后安装将不会成功。

如果在用户点击几乎同一时间在两个设备，则将尝试仅配对的第一个接收到 OOB 信息。

任何尝试点击设备上运行的操作系统的系统不支持 Tap 到安装程序或重新连接到点击可能会导致设备进入可连接模式但配对将不会发生。 用户将需要使用提供的蓝牙配对 UI 并使用配对按钮才能发起配对。

 

 
## <a name="related-topics"></a>相关主题
 [NFC 设备驱动程序接口 (DDI) 参考](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
 
