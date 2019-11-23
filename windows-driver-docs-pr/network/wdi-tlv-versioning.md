---
title: WDI TLV 版本控制
description: 为了保持向后兼容性，WDI 和微型端口都使用 TLV 流作为版本控制边界。
ms.assetid: 308B4C7A-4AC1-4FEB-9775-65ED088F7C48
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2099ffc02bc2159232145f8b4c33f8b511054cb8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841716"
---
# <a name="wdi-tlv-versioning"></a>WDI TLV 版本控制


为了保持向后兼容性，WDI 和微型端口都使用 TLV 流作为版本控制边界。 TLV 字节流的生成者必须始终生成向后兼容的 TLV，而不包含任何新添加的字段。 这是通过将**PeerVersion**添加到*上下文*参数来完成的。 此字段应由调用方初始化为在初始化期间收到的*WdiVersion* 。

下面是*上下文*参数的类型定义，该参数将传入每个分析和生成 API。

```C++
typedef struct _TLV_CONTEXT
{
    ULONG_PTR   AllocationContext;
    ULONG       PeerVersion;
} TLV_CONTEXT, *PTLV_CONTEXT;
typedef const TLV_CONTEXT * PCTLV_CONTEXT;
```

**AllocationContext**由分析和生成 api 修改，并继续传递给微型端口提供的运算符 `new` 回调。 有关详细信息，请参阅[WDI TLV 生成器/分析器内存接口](wdi-tlv-generator-parser-memory-interface.md)。

如果对较旧版本的 WDI 运行基于 WDI 的单二进制驱动程序，则微型端口中的生成器将使用**PeerVersion**生成较旧的字节流。 相反，分析器会根据**PeerVersion**使用较旧的字节流，并将其转换为新的数据结构。

如果微型端口驱动程序不使用 TLV 分析器生成器库，而是写入其自己的 TLV 分析器和生成器，而希望使用单个二进制文件（因此也就是旧版本的 WDI），则它们也必须包括此功能。 它们的分析器必须接受由较旧的 WDI 生成的 TLV 语法，并且其生成器只能根据旧语法生成 TLVs。

已对 XML 进行了补充，以支持 containerRefs 上允许使用两个属性的此版本控制： *versionAdded*和*versionRemoved*。 这会使分析器和生成器根据对等端版本调整字节流。

**请注意**  分析器和生成器会假设它们始终与 WDI\_版本\_最新的链接。 在调用[**NdisMRegisterWdiMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nf-dot11wdi-ndismregisterwdiminiportdriver)而不是使用特定版本（如 WDI\_版本\_1\_0 **）时，** 小型端口应始终将[**NDIS\_\_微**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_miniport_driver_wdi_characteristics)端口的 WDI\_版本传递\_最新版本，而不是使用特定版本，例如\_版本\_1 0，因为其他端可能会发送意外的字节流。

 

 

 





