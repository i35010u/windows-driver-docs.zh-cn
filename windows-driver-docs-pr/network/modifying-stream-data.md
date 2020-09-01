---
title: 修改流数据
description: 修改流数据
ms.assetid: 8f591bc1-272c-4e53-8e49-3350c6a3a33e
keywords:
- 分类标注 WDK Windows 筛选平台，流数据更改
- 流数据更改 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 326fe51f5094ca7efd55dc1c84d44c6d80acaad1
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211033"
---
# <a name="modifying-stream-data"></a>修改流数据


当标注在流层处理数据时，它的 [*classifyFn*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0) callout 函数可以修改数据流中的数据。 标注的 *classifyFn* callout 函数允许流中可接受的数据通过未经修改的、阻止要删除的流中的数据，并在适当时将新数据或更改的数据注入到流中。

标注可以通过阻止要替换的数据将流中的数据替换为其他数据，同时将新数据注入到流中。 在这种情况下，新数据会被注入到流中的同一点，阻止的数据将从流中删除。

若要使标注驱动程序将数据注入数据流，必须先创建注入句柄。 这可能是创建的注入句柄，用于将修改后的数据包数据注入网络堆栈。 有关如何创建注入句柄的信息，请参阅 [检查数据包和流数据](inspecting-packet-and-stream-data.md) 。

有关如何修改流数据的信息，请参阅 [硬件示例](https://go.microsoft.com/fwlink/p/?LinkId=618052) 代码库中的 "Windows 筛选平台流编辑示例"。

 

