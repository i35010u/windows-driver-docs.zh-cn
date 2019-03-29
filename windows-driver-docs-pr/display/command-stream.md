---
title: 命令流
description: 命令流
ms.assetid: 125e2072-42d6-4d4b-aec9-94b40a9d493c
keywords:
- Direct3D WDK Windows 2000 显示，操作代码
- 操作代码 WDK Direct3D
- 命令流 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8296b3045fdde44687e8469ee2466cddb5c6784
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564647"
---
# <a name="command-stream"></a>命令流


## <span id="ddk_command_stream_gg"></span><span id="DDK_COMMAND_STREAM_GG"></span>


在驱动程序级别的调用的形式说明出现[ **D3dDrawPrimitives2**](https://msdn.microsoft.com/library/windows/hardware/ff544704)。 输入的结构[ **D3DHAL\_DRAWPRIMITIVES2DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff545957)包含到命令缓冲区的指针。 这是一系列[ **D3DHAL\_DP2COMMAND** ](https://msdn.microsoft.com/library/windows/hardware/ff545454)结构。 这些结构的每个包含**bCommand**指定什么类型的数据遵循它在缓冲区中的成员。 此规范采用的形式[ **D3DHAL\_DP2OPERATION** ](https://msdn.microsoft.com/library/windows/hardware/ff545678)枚举类型，例如 D3DDP2OP\_INDEXEDTRIANGLESTRIP 或在设置纹理状态的情况下D3DDP2OP\_TEXTURESTAGESTATE。

换而言之，D3DHAL\_DP2OPERATION 操作代码指定何种类型的结构遵循其命令缓冲区中。 通过以下任一方法指定的结构，以按照数**wPrimitiveCount**或**wStateCount**，又是 D3DHAL 的成员将联合成员\_DP2COMMAND 结构。 **WPrimitiveCount**跟踪的成员数图形基元来呈现，而**wStateCount**跟踪的成员的状态更改处理的数量。

一个驱动程序如何处理操作代码示例，请参阅[处理纹理阶段](processing-texture-stages.md)。

 

 





