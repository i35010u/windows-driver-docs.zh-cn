---
title: WDI TLV 版本控制
description: 若要维护向后兼容性，WDI 和微型端口使用 TLV 流作为版本控制边界。
ms.assetid: 308B4C7A-4AC1-4FEB-9775-65ED088F7C48
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07e04e1d5a55eeaeaae4786ef3aac101ea1133d3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67357282"
---
# <a name="wdi-tlv-versioning"></a>WDI TLV 版本控制


若要维护向后兼容性，WDI 和微型端口使用 TLV 流作为版本控制边界。 TLV 字节流的生成者必须始终生成向后兼容 TLV，不包括任何新添加的字段。 这可以通过添加**PeerVersion**到*上下文*参数。 此字段应由调用方的初始化*WdiVersion*接收在初始化过程。

下面是类型定义*上下文*参数传递到每个分析和生成 API。

```C++
typedef struct _TLV_CONTEXT
{
    ULONG_PTR   AllocationContext;
    ULONG       PeerVersion;
} TLV_CONTEXT, *PTLV_CONTEXT;
typedef const TLV_CONTEXT * PCTLV_CONTEXT;
```

**AllocationContext**由分析和生成 Api 以未修改形式，并继续向提供微型端口运算符传递`new`回调。 有关详细信息，请参阅[WDI TLV 生成器/分析器内存接口](wdi-tlv-generator-parser-memory-interface.md)。

基于 WDI 的单一二进制驱动程序运行时对 WDI 较早版本，如果使用中的微型端口生成器**PeerVersion**以生成较旧的字节流。 相反，分析器会使用基于较旧的字节流**PeerVersion**并将其转换到新的数据结构。

如果微型端口驱动程序不使用 TLV 分析器生成器库，而是将写入自己的 TLV 分析器和生成器，并且希望是具有单一的二进制文件运行仅较旧操作系统版本 （以及因此旧版本的 WDI），他们必须也包含此功能。 其分析程序必须接受生成的较旧 WDI TLV 语法和其生成器必须只能生成 TLVs 根据旧语法。

XML 具有其扩充，以支持此版本控制与允许在 containerRefs 上的两个属性： *versionAdded*并*versionRemoved*。 这是什么驱动器的解析器和生成器来调整根据对等方版本的字节流。

**请注意**  分析器和生成器假定它们始终链接与 WDI\_版本\_最新。 微型端口应始终传递 WDI\_版本\_的最新[ **NDIS\_微型端口\_驱动程序\_WDI\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_ndis_miniport_driver_wdi_characteristics)::**WdiVersion**调用时[ **NdisMRegisterWdiMiniportDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nf-dot11wdi-ndismregisterwdiminiportdriver)而不是使用特定版本，如 WDI\_版本\_1\_0，因为它们将会过期并会导致出现问题 TLV 分析器生成器，因为另一端可能会发送是意外的字节流。

 

 

 





