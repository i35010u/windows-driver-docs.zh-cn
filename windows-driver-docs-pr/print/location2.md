---
title: '打孔 (位置) '
description: 此属性包含与在输出页中打孔的位置相关的所有值项。
ms.date: 07/07/2020
ms.localizationpriority: medium
ms.openlocfilehash: deb3311bc0685a5e5c8add4fc0c9d66acca80ec7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807919"
---
# <a name="location-hole-punch"></a>打孔 (位置) 

架构路径： \\ HolePunch

节点类型：属性

说明：此属性包含与在输出页中打孔的位置相关的所有值项。

Location 属性包含两个子值： **CurrentValue** 和 **受支持**。

## <a name="currentvalue"></a>CurrentValue

架构路径： \\ HolePunch： CurrentValue

节点类型：值

数据类型：双向 \_ INT

说明：当前 (默认) 用于打孔的位置。

允许以下值：

顶部

下

Left

Right

## <a name="supported"></a>支持

架构路径： \\ HolePunch：支持

节点类型：值

数据类型：双向 \_ 字符串

说明：打孔位置支持的所有值的逗号分隔列表。
