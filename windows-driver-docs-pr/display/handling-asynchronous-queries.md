---
title: 处理异步查询
description: 处理异步查询
ms.assetid: b5e289db-eb9f-46e6-b221-4aa6661a9ce1
keywords:
- 异步查询操作 WDK DirectX 9.0
- 查询操作 WDK DirectX 9.0，异步
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f84e494a4da2d7c12719272835ac340d312e464
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520678"
---
# <a name="handling-asynchronous-queries"></a>处理异步查询


## <span id="ddk_handling_asynchronous_queries_gg"></span><span id="DDK_HANDLING_ASYNCHRONOUS_QUERIES_GG"></span>


驱动程序将处理异步查询操作中接收[命令流](command-stream.md)的其[ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704)函数按以下顺序中所述:

1.  驱动程序创建的查询的资源后收到 D3DDP2OP\_CREATEQUERY 操作代码，连同[ **D3DHAL\_DP2CREATEQUERY** ](https://msdn.microsoft.com/library/windows/hardware/ff545469)命令中的结构流。

2.  该驱动程序启动的查询处理后收到 D3DDP2OP\_ISSUEQUERY 操作代码，连同[ **D3DHAL\_DP2ISSUEQUERY** ](https://msdn.microsoft.com/library/windows/hardware/ff545638)命令流中的结构。

3.  如果先前所提交查询使用 D3DDP2OP\_ISSUEQUERY 操作已完成，该驱动程序设置中的响应缓冲区的大小**dwErrorOffset**的成员[ **D3DHAL\_DRAWPRIMITIVES2DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff545957)结构和集**ddrval** D3DHAL 成员\_DRAWPRIMITIVES2DATA 到 D3D\_是否已经成功完成的确定。 该驱动程序将覆盖在传入的命令缓冲区[命令流](command-stream.md)与传出流中的响应缓冲区。 驱动程序集[ **D3DHAL\_DP2RESPONSE** ](https://msdn.microsoft.com/library/windows/hardware/ff545710)结构的**bCommand**成员添加到 D3DDP2OP\_RESPONSEQUERY 以指示该响应以前颁发的查询中提供了响应缓冲区。 每个[ **D3DHAL\_DP2RESPONSEQUERY** ](https://msdn.microsoft.com/library/windows/hardware/ff545714)在响应中缓冲区后跟与查询相关的以下数据：

    -   对于 D3DQUERYTYPE 为 BOOL\_事件。 再响应与 D3DDP2OP\_RESPONSEQUERY 事件，该驱动程序必须确保在图形处理单元 (GPU) 是已完成所有处理[ **D3DHAL\_DP2OPERATION** ](https://msdn.microsoft.com/library/windows/hardware/ff545678)与事件相关的操作。 也就是说，该驱动程序只响应事件的问题后\_结束状态时发生。 该驱动程序将事件设置为终止状态之前 (设置为 **，则返回 TRUE**)，可能需要 GPU 来执行刷新以确保像素都是已完成的光栅化、 blts 都已完成，资源不再使用，等等。 该驱动程序必须始终将该事件的 BOOL 值设置为 **，则返回 TRUE**响应时。
    -   DWORD D3DQUERYTYPE\_的阻挡物。 该驱动程序将此 DWORD 设置为其 z 检验针对所有基元之间传递的开始和结束的查询的像素数。 如果多级采样深度缓冲区，该驱动程序将确定从样本数的像素数。 但是，如果显示设备支持的每个 multisample z 测试准确性，转换成的像素为单位的数字应通常会向上舍入。 然后，应用程序可以检查封闭结果对 0，来有效地表示"完全封闭的像素。" 转换为像素数量的多级采样的数量的驱动程序应检测呈现器目标多级取样更改并继续适当地计算查询结果。
    -   [**D3DDEVINFO\_VCACHE** ](https://msdn.microsoft.com/library/windows/hardware/ff544702) D3DQUERYTYPE 结构\_VCACHE。

    如果提供的命令缓冲区太小，驱动程序编写所有响应，该驱动程序还会发送 D3DDP2OP\_RESPONSECONTINUE 传出流中的。

4.  如果运行时确定的驱动程序[ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704)函数成功 (**ddrval** D3DHAL 成员\_DRAWPRIMITIVES2DATA 设置为 D3D\_确定)，则运行时检查**dwErrorOffset** D3DHAL 成员\_DRAWPRIMITIVES2DATA 以确定响应是否可从该驱动程序。 这**dwErrorOffset**成员为零，如果没有响应可用; 否则为**dwErrorOffset**是以字节为单位的响应缓冲区的大小。 因此，在成功*D3dDrawPrimitives2* (**ddrval**设置为 D3D\_确定)，该驱动程序必须确保其唯一集**dwErrorOffset**为非零值提供响应。

5.  在运行时分析返回的响应缓冲区，并更新其内部数据结构。

6.  如果该驱动程序发送 D3DDP2OP\_RESPONSECONTINUE，运行时将提交中传入的空命令缓冲区[命令流](command-stream.md)，以便该驱动程序可以继续编写更多的答复。 该驱动程序必须确保它可以处理空命令缓冲区。

 

 





