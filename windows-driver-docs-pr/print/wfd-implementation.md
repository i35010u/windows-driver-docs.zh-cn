---
title: Wi-Fi 直接打印实现
description: 提供 Wi-Fi 直接打印实现的设备要求的相关信息。
ms.date: 06/15/2020
ms.localizationpriority: medium
ms.openlocfilehash: 69b55fb84ca5dc8b7d3d84f18a357c12ac511975
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831217"
---
# <a name="wi-fi-direct-printing-implementation"></a>Wi-Fi 直接打印实现

## <a name="device-requirements"></a>设备要求

要使 WFD WSD 设备获取 [Wi-fi Direct 打印概述](wfd-overview.md)中所述的无缝连接体验，设备必须遵守以下要求：

- 设备必须支持垂直配对，并发送相关 DPWS (WSD 消息中的 WSD) 数据 (下面的 "实现垂直配对数据 Blob" 中所述格式) 

- 物理设备中的所有逻辑设备必须使用其 Pnp-x 扩展中的相同 Pnp-x 容器 ID

  - 有关为网络连接设备实施 Pnp-x 容器 Id 的详细信息，请参阅 [容器 Id 概述](../install/overview-of-container-ids.md)。

  - 有关 Pnp-x 扩展的常规信息，请参阅 [pnp-x： Windows 即插即用扩展规范](/previous-versions/gg463082(v=msdn.10))。

由于 WFD 容器 ID 将匹配打印机的 UUID，因此设备元数据中不需要 Pnp-x 容器 ID。 但是，仍建议设备在设备元数据中支持 Pnp-id 元数据，并在设备元数据中将 Pnp-x 容器 ID 作为 Pnp-x 元数据的一部分播发。 此容器 ID 应与 WFD 容器 ID 匹配。

在 WFD 层和 WSD 层具有相同的容器 ID 可确保以下各项：

- 配对 UI （如添加设备向导）可以了解多个逻辑设备在单个物理设备上共存，并以更具逻辑性的方式为用户处理配对。  (例如，用户不必在单独的操作中手动配对 WFD 和打印设备。 ) 

- 设备 & 打印机可以显示设备的单个设备图标，即使系统上安装了两组 devnodes (一组 WFD devnodes 和一组 WSD devnodes) 。

- 请注意，要使 Windows 硬件认证工具包测试正确运行，需要正确的容器 ID 实现。 不正确的实现将导致测试将每个逻辑设备识别为单独的物理设备。

如果 WFD WSD 设备不符合上述要求，则此实现中描述的连接体验将不会应用到这些设备。

设备应按照 [Wi-fi 联合-Wi-Fi Direct 工业白皮书](https://www.wi-fi.org)中指定的方式来实施永久性组和并发 Connection-Multiple 组。

## <a name="how-to-publish-container-uuid-over-wi-fi-direct-for-printers"></a>如何通过 Wi-Fi 直接在打印机上发布容器 UUID

Windows 使用探测请求/响应按 Wi-Fi 联盟 "Wi-fi 对等 (P2P) 规范 v1.1" 3.1.2.1.2 (Scan 阶段) 来直接发现 Wi-Fi 打印机。 在这种情况下，设备打印机将使用适当的探测请求/响应帧回复 PC。

可使用自定义扩展 & 探测响应帧的探测请求。 Microsoft 定义了具有多个属性的自定义 IE 来启用各种扩展。

### <a name="how-to-construct-a-microsoft-80211-custom-ie-for-container-uuid"></a>如何构造用于容器 UUID 的 Microsoft 802.11 自定义 IE

自定义 IE 包含供应商 ID & 供应商数据，如以下 WFD 供应商扩展图所示。

![wfd 供应商扩展](images/wfd-customie.png)

Microsoft 使用供应商 ID 0x137 来表示 Microsoft 拥有的。 每个供应商供应商扩展中的供应商数据块包含供应商定义的任意数据块。 Microsoft 供应商扩展中的供应商数据块由一个或多个类型长度值 (TLV) 结构组成。 以下 *WFD 供应商数据* 图中显示了 TLV 结构的组织。

![wfd 供应商数据](images/wfd-vendordatatlv.png)

### <a name="tlv-definition-for-container-uuid"></a>容器 UUID 的 TLV 定义

有两个与包含的 ID 相关的 TLVs。 Windows 发送到设备的 "属性请求" & 存在设备所响应的 "容器 UUID" TLV。

定义：

| 名称/说明 | 键入 (2 个字节)  | 长度 (2 个字节)  | 值 (按长度定义)  |
|--|--|--|--|
| 请求 Microsoft 属性 (此项在发现过程中由计算机在探测请求中发送)  | 0x1005 | 0x0002 | 0x0001 = Microsoft 正在请求包含 UUID |
| 容器 UUID (此在发现过程中由打印机在探测响应中发送)  | 0x1006 | 0x0010 | 要由打印机定义 |

## <a name="implementing-vertical-pairing-data-blob"></a>实现垂直配对数据 Blob

在连接到打印机之前，垂直配对数据 Blob 允许 PC 了解 WSD 打印服务。 此机制是服务发现的简单替代，因为它是在写入 Wi-Fi Direct 的服务发现规范之前实现的。

与容器 UUID 一样，垂直配对数据 Blob 也是 Microsoft IE 的一个属性。 与容器 ID 属性不同的是，这必须在 M7/M8-2ms WPS 消息 (中发布，Wi-Fi 直接配对) ，具体取决于设备的角色。

### <a name="how-to-construct-a-microsoft-80211-custom-ie-for-vertical-pairing"></a>如何构造用于垂直配对的 Microsoft 802.11 自定义 IE

自定义 IE 包含供应商 ID & 供应商数据，如以下 WFD 供应商扩展图所示。

![wfd 供应商扩展](images/wfd-customie.png)

Microsoft 使用供应商 ID 0x137 来表示 Microsoft 拥有的。 每个供应商供应商扩展中的供应商数据块包含供应商定义的任意数据块。 Microsoft 供应商扩展中的供应商数据块由一个或多个类型长度值 (TLV) 结构组成。 以下 WFD 供应商数据图中显示了 TLV 结构的组织：

![wfd 供应商数据](images/wfd-vendordatatlv.png)

### <a name="tlv-definition-for-vertical-pairing-blob"></a>垂直配对 Blob 的 TLV 定义

为 Rally 垂直配对定义了两个特定的 TLV 类型。 下表列出了这些 TLV 类型。

| 名称/说明 | 键入 (2 个字节)  | 长度 (2 个字节)  | 值 (按长度定义)  |
|--|--|--|--|
| 垂直配对标识符 (传达设备的内部拓扑)  | 0x1001 | 0x0002 | 请参阅下面的 "垂直配对标识符 TLV"。 |
| 传输 UUID (设备的传输 UUID 值)  | 0x1002 | 0x0010 | 请参阅上面的 "容器 UUID 的 TLV 定义"。 |

### <a name="vertical-pairing-identifier-tlv"></a>垂直配对标识符 TLV

垂直配对标识符 (VPI) TLV 会传达设备的内部拓扑，该拓扑指定 Windows 如何与设备的服务进行通信。 至少需要一个 VPI 才能支持 Rally 垂直配对扩展，即使设备中未实现垂直配对也是如此。 在这种情况下，VPI 将指定不使用传输。 必须将 VPI TLV 作为 Microsoft 供应商扩展的一部分发送到 WPS M1 消息中。

VPI TLV 附带的数据长度为2个字节，包含两个不同的字段： "传输" 字段和 "配置文件请求" 字段，如下图所示，每个字段 (每个字段都为1个字节长) 。

![使用 vpi tlv 进行 wfd 数据](images/wfd-vpi.png)

### <a name="vpi-transport-field"></a>VPI 传输字段

传输字段指定 Windows 可用来与设备通信的传输。 每个 VPI 只能指定一个传输。 如果设备支持多个 Pnp-x 传输，则可以通过为 Microsoft 供应商扩展中的每个传输) 包含多个 VPI TLVs (。 下表列出了 VPI 传输字段的有效值。

| “值” | Transport |
|--|--|
| 0x00 | 无 |
| 0x01 | DPWS |
| 0x02 | UPnP |
| 0x03 | 保护 DPWS |
| 0x04-0xFF | 预留 |

> [!NOTE]
> Windows 7 支持 DPWS (0x01) 或 Secure DPWS (0x03) ，但不能同时支持两者。

如果设备未实现 Rally 垂直配对，则它必须仅指定一个传输值为0x00 的 VPI ("无") 。 在这种情况下，设备不应指定传输 UUID TLV。 这会通知 Windows 它不应与设备配对。 因此，Windows 在配置设备的 Wi-Fi 设置时，不会尝试与设备预配对。

### <a name="vpi-profile-request-field"></a>VPI 配置文件请求字段

VPI 允许设备使用 WPS 协议预配设备的服务。 在这种情况下，设备服务可以请求 Windows 发送用于配置服务的信息。 此信息称为配置文件。 VPI 的第二个字段指定设备是否正在请求 Windows 向其发送配置文件。 下表列出了 VPI 配置文件请求字段的有效值。

| “值” | 描述 |
|--|--|
| 0x01 | 请求 Wi-Fi 配置文件。 这是 Windows 7 当前支持的唯一值。 |
| 0x00，0x02 –0xFF | 预留 |

VPI 配置文件请求字段值0x00 被视为保留值，因为 Windows 7 当前不支持此值。 应仅将 "VPI 配置文件请求" 字段设置为 () 的值 0x01 Wi-fi 配置文件，即使为该传输指定的值为 0x00 (none) 。

### <a name="transport-uuid-tlv"></a>传输 UUID TLV

传输 UUID TLV 指定特定传输 (DPWS 或 UPnP) 的基本 UUID 值与 WPS UUID 不同。 传输 UUID TLV 是可选的。 如果未包含传输 UUID TLV，则使用 WPS UUID 形成指定传输的标识。

如果包含传输 UUID TLV，则它必须紧跟在标识传输的 VPI TLV 之后。 如果包括多个 VPI TLV，则每个 VPI TLV 之后都可以包含一个传输 UUID TLV。

传输 UUID TLV 数据值必须采用网络字节顺序。

如果设备指定的 VPI 传输值为 0x00 (none) ，请不要包含传输 UUID TLV。

## <a name="wps-example"></a>WPS 示例

对于本示例，假定打印机设备使用 DPWS 并实现 WS 打印接口。 设备使用下表中的 UUID 值：

| 服务 | 标识 |
|--|--|
| WPS | ec742c0d-5915-4bcb-b969-008132afec5e |
| DPWS 打印 | urn： uuid：00010203-0405-0607-0809-0a0b0c0e0e0f |

### <a name="wps-exampleservice-uuid-values"></a>WPS 示例-服务 UUID 值

UUID 值以全部小写指定，DPWS 标识字符串使用格式 urn： uuid： uuid \_ 值。

> [!NOTE]
> 此示例中的 UUID 值是虚构的，不能在实际设备中使用。

当设备发送其 WPS M7/M8-2ms 消息时，它会包含 Microsoft 供应商扩展，此扩展将在以下示例中显示：

![wfd 供应商扩展详细信息示例](images/wfd-vendorextensiondetails.png)

在此示例中，供应商扩展包含0x137 的供应商 ID 值，该值将其标识为 Microsoft 供应商扩展。 供应商扩展的供应商数据字段中包含两个 TLV 结构。

第一个 TLV 的类型值为0x1001，它将 TLV 标识为 VPI。 第一个 TLV 中的数据长度为2个字节，其中包含值0x0101。 此方法指定设备支持 DPWS 传输 (0x01) ，并请求配置文件 (0x01) 。

第二个 TLV 的类型值为0x1002，它将 TLV 标识为传输 UUID。 第二个 TLV 中的数据长度为16字节，其中包含00010203-0405-0607-0809-0a0b0c0e0e0f 的二进制版本。

当客户垂直配对打印机时，Windows 首先使用适当的设置来配置设备的 Wi-Fi 收音机。 然后，它使用指定的传输 UUID 值配对设备的 DPWS 设备。

在设备连接到 Wi-Fi 网络并公布其 DPWS 服务后，Windows 将创建适当的 PnP 设备节点并安装和加载相应的驱动程序。
