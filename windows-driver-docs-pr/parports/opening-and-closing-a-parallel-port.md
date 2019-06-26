---
title: 打开和关闭并行端口
description: 打开和关闭并行端口
ms.assetid: 2183ffd9-8265-4848-b5d1-703643e0d0e6
keywords:
- WDK，打开的并行端口
- 并行端口 WDK，关闭
- 并行端口 WDK，共享
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40b9245151e32fa40d4ec69aa99b8b5d26c63889
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358499"
---
# <a name="opening-and-closing-a-parallel-port"></a>打开和关闭并行端口





客户端可以共享的并行端口。 客户端必须打开并行端口上的文件，然后客户端可以使用其他输入/输出请求或使用[并行端口回调例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。 客户端必须尝试后客户端已关闭其文件的端口上与并行端口进行通信。

请注意，在插环境中，设备可以删除或添加任何打开的文件时。 一般情况下，每次添加并行端口，插分配不同的位置和资源。

 

 




