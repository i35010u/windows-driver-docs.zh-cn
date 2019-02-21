---
title: 命令和顶点缓冲区
description: 命令和顶点缓冲区
ms.assetid: e23013d2-d545-42e5-9787-e4a90921153b
keywords:
- 命令缓冲区 WDK Direct3D
- 顶点缓冲区 WDK Direct3D
- WDK Direct3D 缓冲区
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7560faa0a27216251438b8697d885b1b3ddcd365
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526486"
---
# <a name="command-and-vertex-buffers"></a>命令和顶点缓冲区


## <span id="ddk_command_and_vertex_buffers_gg"></span><span id="DDK_COMMAND_AND_VERTEX_BUFFERS_GG"></span>


[ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704) DDI 使用两种类型的缓冲区： 命令缓冲区和顶点缓冲区。 命令缓冲区包含跟结构类似于执行缓冲区中数据的说明。 命令缓冲区可能包含索引和非索引基元，有时，内联顶点数据。 命令缓冲区可以是任一 API 级别执行缓冲区或 Direct3D 内部命令缓冲区。 主要输入结构的说明，请参阅[ **D3DHAL\_DRAWPRIMITIVES2DATA**](https://msdn.microsoft.com/library/windows/hardware/ff545957)。

与内部命令缓冲区，该驱动程序分配的内存，可能 multibuffering。 内部命令缓冲区是只写。 指令格式所示[ **D3DHAL\_DP2COMMAND**](https://msdn.microsoft.com/library/windows/hardware/ff545454)。

如果 D3DHALDP2\_设置 USERMEMVERTICES 标志，顶点缓冲区指定的用户内存指针。 否则，顶点缓冲区是可以是 API 级别执行缓冲区、 内部隐式顶点缓冲区或 API 级别顶点缓冲区 DirectDrawSurface。

顶点缓冲区 API 可以创建、 销毁、 锁定和解锁顶点缓冲区，可以使用**IDirect3DVertexBuffer7::ProcessVertices**到过程顶点从源到目标缓冲区的方法。 **IDirect3DDevice7::DrawPrimitiveVB**并**IDirect3DDevice7::DrawIndexedPrimitiveVB**方法都是主要的 API 级别调用。 此外可以优化顶点缓冲区，但不能锁定优化的顶点缓冲区。 这三种方法的说明，请参阅 Direct3D SDK 文档。

 

 





