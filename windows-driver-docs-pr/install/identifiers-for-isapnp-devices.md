---
title: ISAPNP 设备的标识符
description: ISAPNP 设备的标识符
keywords:
- 设备标识字符串 WDK，ISAPNP 设备
- 标识字符串 WDK 设备，ISAPNP 设备
- 标识符 WDK 设备，ISAPNP 设备
- ISAPNP 设备标识符 WDK 设备安装
- 硬件 Id WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f8f6d0d3108163036d89c8d905169978079efd1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829923"
---
# <a name="identifiers-for-isapnp-devices"></a>ISAPNP 设备的标识符





每个 ISAPNP 卡都支持可读的资源数据结构，该结构描述了支持的资源和卡所请求的资源。 此结构支持 (或 "逻辑设备" ) ISA 卡的多个函数的概念。 一组单独的 "标记" 或 "描述符" 与卡片的每个函数相关联。 ISAPNP 枚举器使用此标记信息构造两个硬件标识符，格式为：

ISAPNP \\ m (3) d (4) 

\*m (3) n (4) 

其中， *m (3) d (4)* 一起构成设备的 EISA 样式的标识符，三个字母用于标识制造商，4个十六进制数字用于标识特定设备。

以下硬件 Id 对可能由多功能卡上的特定功能生成：

ISAPNP \\ CSC6835_DEV0000

\*CSC0000

这两个硬件 Id 中的第一种是设备 ID。 如果相关设备是多功能卡的一个功能，则设备 ID 采用以下格式：

ISAPNP \\ m (3) d (4) _DEVn (4) 

其中， *n (4)* 是 (具有函数前导零) 的十进制索引。

这两个硬件标识符中的第二个也是兼容的 ID。 ISAPNP 枚举器生成一个或多个兼容 Id，其中第一个 Id 始终是第二个硬件 ID。 ISAPNP 兼容 ID 中为 "" 的前三个字符（ *m (3)*） \* 通常是 "PNP"。 例如，串行端口的兼容 ID 可能是：

PNP0501

 

 





