---
title: AV/C 子单元插头连接和格式管理
description: AV/C 子单元插头连接和格式管理
keywords:
- 插头连接 WDK AV/C
- 子次级支持 WDK AV/C
- AV/C WDK，插头连接
- 对等子单位驱动程序堆栈 WDK AV/C
- KS pin 连接 WDK AV/C
- 固定连接 WDK AV/C
- 格式化 WDK AV/C
- pin 格式 WDK AV/C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff78759f92420adbf549d729ac2dca3c05a14154
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817047"
---
# <a name="avc-subunit-plug-connection-and-format-management"></a>AV/C 子单元插头连接和格式管理





AV/C 对等互连驱动程序堆栈为 IEEE 1394 和 AV/C 子单位插入连接和格式管理提供函数。 内核流式传输 (KS) pin 格式协商和 pin 连接机制会转换为通过 *Avc.sys* 的插入连接。 此体系结构的一些关键方面包括：

-   IEEE 1394 和 AV/C 子单位的插头连接在 DirectShow 筛选器-图形中表示为 KS pin 连接。

-   IEEE 1394 串行总线插入 (输入和输出插头) 仅当没有内部子源插头连接功能时，才会直接表示为 KS pin。 出现这种情况时，每个 IEEE 1394 串行总线插头有一个 pin。

-   中型全局唯一标识符 (GUID) 表示 IEEE 1394 串行总线连接。 有关中型 Guid 的详细信息，请参阅 [媒体和类别](mediums-and-categories.md)。

-   用于永久内部 AV/C 单元和子单位连接的中等 Guid 是从设备唯一标识符和插入地址合成的。

-   有新的 KSDATARANGE 和 KSDATAFORMAT 扩展可用于 AV/C 连接。

媒体和格式一起有助于确定 KS pin 连接是由 IEEE 1394 串行总线上的计算机还是从内部设备到设备的内部数据。

 

 




