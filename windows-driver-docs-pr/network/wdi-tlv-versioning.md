---
title: WDI TLV 版本控制
description: 为了保持向后兼容性，WDI 和微型端口都使用 TLV 流作为版本控制边界。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a09be62539c4e22e25e99fb44180ca5c97d17be8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834121"
---
# <a name="wdi-tlv-versioning"></a>WDI TLV 版本控制


为了保持向后兼容性，WDI 和微型端口都使用 TLV 流作为版本控制边界。 TLV 字节流的生成者必须始终生成向后兼容的 TLV，而不包含任何新添加的字段。 这是通过将 **PeerVersion** 添加到 *上下文* 参数来完成的。 此字段应由调用方初始化为在初始化期间收到的 *WdiVersion* 。

下面是 *上下文* 参数的类型定义，该参数将传入每个分析和生成 API。

```C++
typedef struct _TLV_CONTEXT
{
    ULONG_PTR   AllocationContext;
    ULONG       PeerVersion;
} TLV_CONTEXT, *PTLV_CONTEXT;
typedef const TLV_CONTEXT * PCTLV_CONTEXT;
```

**AllocationContext** 由分析和生成 api 修改，并继续传递给微型端口提供的运算符 `new` 回调。 有关详细信息，请参阅 [WDI TLV 生成器/分析器内存接口](wdi-tlv-generator-parser-memory-interface.md)。

如果对较旧版本的 WDI 运行基于 WDI 的单二进制驱动程序，则微型端口中的生成器将使用 **PeerVersion** 生成较旧的字节流。 相反，分析器会根据 **PeerVersion** 使用较旧的字节流，并将其转换为新的数据结构。

如果微型端口驱动程序不使用 TLV 分析器生成器库，而是写入其自己的 TLV 分析器和生成器，并且需要使用单个二进制运行 (较旧的操作系统版本，因此，这些旧版本的 WDI) 也必须包括此功能。 它们的分析器必须接受由较旧的 WDI 生成的 TLV 语法，并且其生成器只能根据旧语法生成 TLVs。

已对 XML 进行了补充，以支持 containerRefs 上允许使用两个属性的此版本控制： *versionAdded* 和 *versionRemoved*。 这会使分析器和生成器根据对等端版本调整字节流。

**注意**  分析器和生成器会假设它们始终与 WDI \_ 版本 \_ 最新链接。 在 \_ \_ 调用 [**NdisMRegisterWdiMiniportDriver**](/windows-hardware/drivers/ddi/dot11wdi/nf-dot11wdi-ndismregisterwdiminiportdriver)而不是使用特定版本（如 WDI 版本 1 0）时，微型端口应始终为 [**NDIS \_ 微型端口 \_ 驱动程序 \_ WDI \_ 特性**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_miniport_driver_wdi_characteristics)：：**WdiVersion** 传递 WDI 版本， \_ \_ \_ 因为它们将会过期并导致 TLV 分析器生成器出现问题，因为其他端可能会发送意外的字节流。

 

 

