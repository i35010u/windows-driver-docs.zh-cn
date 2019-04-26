---
title: Wi-Fi Direct 打印实现
description: 提供有关 Wi-Fi Direct 打印实现设备要求的信息。
ms.assetid: 03266F8F-4C91-49E7-9CAF-2D08AF5E3E18
ms.date: 01/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9acae4bdd2577d02567bd9feb027ae9a18def63c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326035"
---
# <a name="wi-fi-direct-printing-implementation"></a>Wi-Fi Direct 打印实现


## <a name="device-requirements"></a>设备要求


WFD WSD 设备以获取无缝连接体验，如中所述[Wi-Fi Direct 打印概述](wfd-overview.md)，设备必须遵守以下要求：

-   设备必须支持垂直配对并发送相关 DPWS (WSD) 数据中的 WPS 消息 （"实现垂直配对的数据 Blob"下面所述的格式）
-   物理设备中的所有逻辑设备必须在其 PNP-X 的扩展中使用相同的 PNP-X 的容器 ID
    -   有关为网络连接的设备实现 PNP-X 的容器 Id 的详细信息，请参阅[概述的容器 Id](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-container-ids)。
    -   PNP-X 的扩展的常规信息，请参阅[PnP x:Plug and Play for Windows 规范的扩展](https://msdn.microsoft.com/windows/hardware/gg463082)。

由于 WFD 容器 ID 将与匹配的打印机的 UUID，设备元数据中将不需要 PNP-X 的容器 ID。 但是，仍建议设备支持 PNP-X 的元数据中的设备元数据和设备元数据中的 PNP-X 的元数据的一部分播发 PNP-X 的容器 ID。 此容器 ID 应匹配 WFD 容器的 id。

具有相同的容器 ID WFD 层以及 WSD 层可确保以下项：

-   配对 UI，如添加一个设备向导中，可以了解多个逻辑设备共存于单个物理设备和处理方式为用户更具逻辑性配对。 （例如用户无需配对 WFD 和手动在单独的操作中的打印设备。）
-   即使有两个设置的 devnodes （WFD devnodes 一个组），另一 WSD devnodes 在系统上安装的设备和打印机可以显示设备的单个设备的图标。
-   请注意该正确的容器 ID 实现是所必需的 Windows 硬件认证工具包测试正确运行。 不正确的实现将导致测试作为单独的物理设备识别每个逻辑设备。

如果 WFD WSD 设备不符合上述要求，然后在此实现中所述的连接体验不会应用到这些设备中。

设备应实现持久的组和并发连接多个组中的规定[Wi-fi 联盟-Wi-Fi Direct 行业白皮书](https://go.microsoft.com/fwlink/p/?LinkId=784967)。

## <a name="how-to-publish-container-uuid-over-wi-fi-direct-for-printers"></a>如何将发布容器 UUID 通过 Wi-Fi Direct 打印机


Windows 通过 Wi-Fi Direct 使用探测请求/响应每个 Wi-fi 联盟"Wi-Fi-对等 (P2P) 规范 v1.1"发现打印机部分 3.1.2.1.2 （扫描阶段）。 该设备，打印机在这种情况下将回复使用适当的探测请求/响应帧的 PC。

同时探测请求和探测响应帧可以使用自定义导致浏览器扩展。 Microsoft 还定义了自定义 IE 具有多个特性来启用各种扩展。

**如何构造 Microsoft 802.11 自定义 IE**

自定义 IE 包含供应商 ID 和供应商数据。

![wfd 供应商扩展](images/wfd-customie.png)

*WFD 供应商扩展*

Microsoft 使用供应商 ID 0x137 来表示导致浏览器由 Microsoft 拥有。 在每个供应商的供应商扩展的供应商数据块包含任意供应商定义数据的块。 在 Microsoft 供应商扩展包含一个或多个类型-长度-值 (TLV) 结构中块的供应商数据。 在图下方显示 TLV 结构的组织。

![wfd 供应商数据](images/wfd-vendordatatlv.png)

*WFD 供应商数据*

**容器 UUID 的 TLV 定义**

有两个 TLVs 与 Contained id。 没有"请求属性"，Windows 将发送到设备和没有"容器 UUID"TLV 设备使用进行响应。

定义：

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>名称/描述</th>
<th>类型 （2 个字节）</th>
<th>长度 （2 个字节）</th>
<th>值 （由长度定义）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>请求的 Microsoft 属性 （这由发送探测请求中的 PC 在发现期间）</p></td>
<td><p>0x1005</p></td>
<td><p>0x0002</p></td>
<td><p>0x0001 = Microsoft 正在请求包含 UUID</p></td>
</tr>
<tr class="even">
<td><p>容器 UUID （这由发送打印机在探测响应在发现期间）</p></td>
<td><p>0x1006</p></td>
<td><p>0x0010</p></td>
<td><p>若要定义的打印机</p></td>
</tr>
</tbody>
</table>

 

## <a name="implementing-vertical-pairing-data-blob"></a>实现垂直配对的数据 Blob


垂直的配对数据 Blob 允许 PC 连接到打印机之前，了解 WSD 打印服务。 此机制是服务发现的简单替代 Wi-Fi Direct 的服务发现规范已写入之前已实现。

容器 UUID，如垂直配对的数据 Blob 也是 Microsoft IE 的属性。 与不同的容器 ID 属性，这必须发布，任一 M7/M8 WPS 消息中 （在 Wi-Fi Direct 配对） 期间从设备根据其角色。

**如何构造 Microsoft 802.11 自定义 IE**

自定义 IE 包含供应商 ID 和供应商数据。

![wfd 供应商扩展](images/wfd-customie.png)

*WFD 供应商扩展*

Microsoft 使用供应商 ID 0x137 来表示导致浏览器由 Microsoft 拥有。 在每个供应商的供应商扩展的供应商数据块包含任意供应商定义数据的块。 在 Microsoft 供应商扩展包含一个或多个类型-长度-值 (TLV) 结构中块的供应商数据。 TLV 结构的组织在下图中所示：

![wfd 供应商数据](images/wfd-vendordatatlv.png)

*WFD 供应商数据*

**垂直配对的 Blob 的 TLV 定义**

为 Rally 垂直配对定义两个特定 TLV 类型。 下表列出了这些 TLV 类型。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>名称/描述</th>
<th>类型 （2 个字节）</th>
<th>长度 （2 个字节）</th>
<th>值 （由长度定义）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>垂直配对标识符 （进行通信的设备内部拓扑）</p></td>
<td><p>0x1001</p></td>
<td><p>0x0002</p></td>
<td><p>请参阅下面的"垂直配对标识符 TLV"。</p></td>
</tr>
<tr class="even">
<td><p>传输 UUID （设备的 UUID 值传输）</p></td>
<td><p>0x1002</p></td>
<td><p>0x0010</p></td>
<td><p>请参阅上面的"容器 UUID TLV 定义"。</p></td>
</tr>
</tbody>
</table>

 

*Rally 垂直配对 TLVs*
**垂直配对标识符 TLV**

垂直配对标识符 (VPI) TLV 通信设备的内部拓扑，指定 Windows 可以在与设备的服务进行通信。 至少一个 VPI 必需以支持 Rally 垂直配对的扩展，即使在设备中不实现垂直配对。 在此情况下，VPI 会指定不使用任何传输。 VPI TLV 必须作为 Microsoft 供应商扩展 WPS M1 消息中的一部分发送。

附带 VPI TLV 数据是 2 个字节长和两个不同字段组成： 传输字段和一个配置文件请求字段，如下面的图像 （每个字段为 1 个字节长） 中所示：

![wfd vpi tlv 中包含的数据](images/wfd-vpi.png)

*WFD VPI TLV 中包含的数据*

**VPI 传输字段**

传输字段指定 Windows 可用于与设备进行通信的传输。 每 VPI，可以指定只有一个传输。 如果设备支持多个 PNP-X 的传输协议，它可以通过在 Microsoft 供应商扩展中包含多个 VPI TLVs （一个用于每个传输协议） 来进行通信。 下表中列出 VPI 传输字段的有效值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ReplTest1</th>
<th>“传输”</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0x00</p></td>
<td><p>无</p></td>
</tr>
<tr class="even">
<td><p>0x01</p></td>
<td><p>DPWS</p></td>
</tr>
<tr class="odd">
<td><p>0x02</p></td>
<td><p>UPnP</p></td>
</tr>
<tr class="even">
<td><p>0x03</p></td>
<td><p>安全 DPWS</p></td>
</tr>
<tr class="odd">
<td><p>0x04-0xFF</p></td>
<td><p>保留</p></td>
</tr>
</tbody>
</table>

 

*VPI 传输字段值*

**请注意**  Windows 7 提供支持 DPWS (0x01) 或安全 DPWS (0x03)，但不是同时。

 

**请注意**  如果设备未实现 Rally 垂直配对时，它必须指定只有一个 VPI 传输值为 0x00 （无）。 在此情况下，设备不应指定传输 UUID TLV。 这会通知 Windows，它不应期望以与设备配对。 因此，Windows 不会尝试将设备的 Wi-fi 设置配置时，与设备预配对。

 

**VPI 配置文件请求字段**

VPI 一来，设备使用 WPS 协议来预配设备的服务。 在这种情况下，设备服务可以请求，Windows 将其发送了用于配置服务的信息。 此信息称为配置文件。 VPI 的第二个字段指定设备是否正在请求，Windows 将其发送了一个配置文件。 下表中列出的 VPI 配置文件请求的字段的有效值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0x01</p></td>
<td><p>请求的 Wi-fi 配置文件。 这是 Windows 7 目前支持的唯一值。</p></td>
</tr>
<tr class="even">
<td><p>0x00，0x02 – 0xFF</p></td>
<td><p>保留</p></td>
</tr>
</tbody>
</table>

 

*VPI 配置文件请求字段值*

**请注意**  VPI 配置文件请求字段值为 0x00 被视为预留，因为它当前不支持通过 Windows 7。 VPI 配置文件请求字段仅应设置为值 0x01 （请求的 Wi-fi 配置文件），值为 0x00 （无），即使指定的传输。

 

**传输 UUID TLV**

传输 UUID TLV 指定特定的传输 （DPWS 或 UPnP） 具有不同基 UUID 值比 WPS UUID。 传输 UUID TLV 是可选的。 如果未包括传输 UUID TLV，则使用 WPS UUID 窗体中指定的传输的标识。

如果包括传输 UUID TLV，则它必须紧跟标识传输 VPI TLV。 如果包含多个 VPI TLV，则在每个 VPI TLV 后可以包含传输 UUID TLV。

**请注意**  传输 UUID TLV 数据值必须以网络字节顺序。

 

**请注意**  设备指定 VPI 传输值为 0x00 （无），如果不包括传输 UUID TLV。

 

## <a name="wps-example"></a>WPS 示例


对于此示例中，假定打印机设备使用 DPWS 并实现 WS 打印接口。 设备使用下表中的 UUID 值：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>服务</th>
<th>标识</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WPS</p></td>
<td><p>ec742c0d-5915-4bcb-b969-008132afec5e</p></td>
</tr>
<tr class="even">
<td><p>DPWS 打印</p></td>
<td><p>urn:uuid:00010203-0405-0607-0809-0a0b0c0e0e0f</p></td>
</tr>
</tbody>
</table>

 

*WPS 示例 — 服务 UUID 值*

**请注意**  中全部小写，指定 UUID 值并 DPWS 标识字符串使用格式 urn: uuid:uuid\_值。

 

**请注意**  在此示例中的 UUID 值是虚构的和不得在实际设备上使用。

 

当设备发送出其 WPS M7/M8 消息时，它包括在下图中所示的 Microsoft 供应商扩展：

![示例 wfd 供应商扩展详细信息](images/wfd-vendorextensiondetails.png)

*示例 WFD 供应商扩展详细信息*

在此示例中，供应商扩展包含 0x137，其标识为 Microsoft 供应商扩展的供应商 ID 值。 在供应商扩展的供应商数据字段是两个 TLV 结构。

第一个 TLV 具有 0x1001，标识作为 VPI TLV 类型值。 第一个 TLV 中数据的长度为 2 个字节，包含值为 0x0101。 这将指定设备是否支持 DPWS 传输 (0x01) 和请求的配置文件 (0x01)。

第二个 TLV 具有 0x1002，标识作为传输 UUID TLV 类型值。 第二个 TLV 中的数据的长度为 16 个字节，其中包含的 UUID 值 00010203-0405年-0607年-0809年-0a0b0c0e0e0f 的二进制版本。

客户垂直对打印机，Windows 先将设备的 Wi-fi 无线电配置具有适当设置。 然后，它使用指定的传输 UUID 值对 DPWS 设备。

设备连接到 Wi-fi 网络，并宣布其 DPWS 服务后，Windows 将适当的即插即用设备节点创建和安装并加载合适的驱动程序。

 

 




