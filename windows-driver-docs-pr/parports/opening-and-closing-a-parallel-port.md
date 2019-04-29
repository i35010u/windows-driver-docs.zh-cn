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
ms.openlocfilehash: 94e66a666784484a185eb8253754d335578a2363
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373486"
---
# <a name="opening-and-closing-a-parallel-port"></a>打开和关闭并行端口





客户端可以共享的并行端口。 客户端必须打开并行端口上的文件，然后客户端可以使用其他输入/输出请求或使用[并行端口回调例程](https://msdn.microsoft.com/library/windows/hardware/ff544307)。 客户端必须尝试后客户端已关闭其文件的端口上与并行端口进行通信。

请注意，在插环境中，设备可以删除或添加任何打开的文件时。 一般情况下，每次添加并行端口，插分配不同的位置和资源。

 

 




