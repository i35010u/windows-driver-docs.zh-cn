---
title: " (装订) 位置"
description: 此属性包含与在输出页上进行装订的位置相关的所有值项。
ms.date: 07/07/2020
ms.localizationpriority: medium
ms.openlocfilehash: efc31775c3a9310dc055f8d68125a131c8ee3308
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807915"
---
# <a name="location-staple"></a> (装订) 位置

架构路径： \\ Printer .. 装订。位置

节点类型：属性

说明：此属性包含与在输出页上进行装订的位置相关的所有值项。

Location 属性包含两个子值： **CurrentValue** 和 **受支持**。

## <a name="currentvalue"></a>CurrentValue

架构路径： \\ Printer .. 装订。位置： CurrentValue

节点类型：值

数据类型：双向 \_ 字符串

说明：当前 (默认情况下应用装订的) 位置。

允许以下值：

StapleTopLeft

StapleBottomLeft

StapleTopRight

StapleBottomRight

StapleDualLeft

StapleDualRight

StapleDualTop

StapleDualBottom

SaddleStitch

其他

未知

## <a name="supported"></a>支持

架构路径： \\ Printer .. 装订：支持

节点类型：值

数据类型：双向 \_ 字符串

说明：以逗号分隔的列表，其中列出了装订位置支持的所有值。
