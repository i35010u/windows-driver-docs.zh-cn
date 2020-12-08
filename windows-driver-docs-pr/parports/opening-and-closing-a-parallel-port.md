---
title: 打开和关闭并行端口
description: 打开和关闭并行端口
keywords:
- 并行端口 WDK，打开
- 并行端口 WDK，关闭
- 并行端口 WDK，共享
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f543b6dc6e2b30307e1e8afcf2fc8be5ae1f27b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812599"
---
# <a name="opening-and-closing-a-parallel-port"></a>打开和关闭并行端口





客户端可以共享并行端口。 客户端必须先在并行端口上打开文件，然后客户端才能使用其他 i/o 请求或使用 [并行端口回调例程](/windows-hardware/drivers/ddi/index)。 客户端在端口上关闭其文件后，不能尝试与并行端口进行通信。

请注意，在即插即用环境中，每当设备上没有打开的文件时，可以删除或添加设备。 通常，每次添加并行端口时，即插即用会分配不同的位置和资源。

 

