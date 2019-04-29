---
title: 修改流数据
description: 修改流数据
ms.assetid: 8f591bc1-272c-4e53-8e49-3350c6a3a33e
keywords:
- 分类标注 WDK Windows 筛选平台，流数据更改
- 流的数据更改 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0612f461a8b6f780115296af5a52ba759eacd4e8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362318"
---
# <a name="modifying-stream-data"></a>修改流数据


在标注处理流层的数据时其[ *classifyFn* ](https://msdn.microsoft.com/library/windows/hardware/ff544890)标注函数可修改数据流中的数据。 标注*classifyFn*标注函数允许将通过在要删除的流中没有更改，阻止将数据在流中的可接受数据并将新的或更改数据注入到流时适用。

标注可以在流中的数据将替换为其他数据通过阻止要替换的数据，并在相同时，将新数据注入到流。 在此情况下，新数据插入到流中的阻止的数据从流中删除其中的相同点。

对于用于将数据注入到数据流的标注驱动程序，它必须先创建注入句柄。 这可以是为将修改后的数据包数据注入恢复到网络堆栈创建的相同注入句柄。 请参阅[检查数据包和 Stream 数据](inspecting-packet-and-stream-data.md)有关如何创建注入句柄的信息。

有关如何修改数据流式传输的信息，请参阅"Windows 筛选平台 Stream 编辑示例"中[硬件示例](https://go.microsoft.com/fwlink/p/?LinkId=618052)代码库。

 

 





