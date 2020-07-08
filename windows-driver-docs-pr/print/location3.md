---
title: 位置（装订）
description: 此属性包含与在输出页上进行装订的位置相关的所有值项。
ms.assetid: cbe6ec7f-36dd-484e-8db6-42e91e69577c
ms.date: 07/07/2020
ms.localizationpriority: medium
ms.openlocfilehash: a8a714ed9489c7919f7e181040da2d7a334ff450
ms.sourcegitcommit: ff2f72fe98f6ba559c1c01b17d25c773df7337c1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/07/2020
ms.locfileid: "86060848"
---
# <a name="location-staple"></a>位置（装订）

架构路径： \\ Printer .. 装订。位置

节点类型：属性

说明：此属性包含与在输出页上进行装订的位置相关的所有值项。

Location 属性包含两个子值： **CurrentValue**和**受支持**。

## <a name="currentvalue"></a>CurrentValue

架构路径： \\ Printer .. 装订。位置： CurrentValue

节点类型：值

数据类型：双向 \_ 字符串

说明：应用装订的当前（默认）位置。

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
