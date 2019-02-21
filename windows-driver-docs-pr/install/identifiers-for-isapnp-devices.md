---
title: 适用于 ISAPNP 设备标识符
description: 适用于 ISAPNP 设备标识符
ms.assetid: 67337bd6-3b5f-41a7-b50d-bf3587f243e8
keywords:
- 设备标识字符串 WDK、 ISAPNP 设备
- ISAPNP 设备-设备标识字符串 WDK
- 标识符 WDK 设备，ISAPNP 设备
- ISAPNP 设备标识符 WDK 设备安装
- 硬件 Id WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 341d5ef9ae7a5337e0b241f8ede14847e3ec0174
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543877"
---
# <a name="identifiers-for-isapnp-devices"></a>适用于 ISAPNP 设备标识符





每个 ISAPNP 卡支持可读的资源数据结构，描述支持的资源和所请求的卡。 此结构支持多个函数 （或"逻辑设备"） 的概念适用于 ISA 卡片。 一组单独的"tags"或"描述符"与相关联的卡的每个函数。 使用此标记信息，ISAPNP 枚举器构造两个硬件标识符，格式为：

ISAPNP\\m(3)d(4)

\*m(3)n(4)

其中*m(3)d(4)* 两者共同构成设备--三个字母来标识特定的设备进行标识的制造商和 4 个十六进制数字的 EISA 样式标识符。

以下两个硬件 Id 可能生成的多功能卡上的特定函数：

ISAPNP\\CSC6835_DEV0000

\*CSC0000

这两个硬件 Id 的第一个是设备 id。 如果该设备是多功能卡的一个函数，则设备 ID 采用如下格式：

ISAPNP\\m(3)d(4)_DEVn(4)

其中*n(4)* 是十进制索引 （使用前导零） 的函数。

两个硬件标识符的第二个也是一个兼容的 id。 ISAPNP 枚举器将生成一个或多个兼容 Id 其中第一个始终是第二个硬件 id。 前三个字符， *m(3)*，后面"\*"在 ISAPNP 兼容 ID 都是经常"PNP。" 例如，串行端口的兼容 ID 可能是这样：

PNP0501

 

 





