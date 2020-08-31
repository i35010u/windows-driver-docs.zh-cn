---
title: 处理异步查询
description: 处理异步查询
ms.assetid: b5e289db-eb9f-46e6-b221-4aa6661a9ce1
keywords:
- 异步查询操作 WDK DirectX 9。0
- 查询操作 WDK DirectX 9.0，异步
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 157313c865542fd9d61d6a68d6b13198384cebe2
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064148"
---
# <a name="handling-asynchronous-queries"></a>处理异步查询


## <span id="ddk_handling_asynchronous_queries_gg"></span><span id="DDK_HANDLING_ASYNCHRONOUS_QUERIES_GG"></span>


驱动程序处理在其[**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)函数的[命令流](command-stream.md)中接收的异步查询操作，如以下序列中所述：

1.  驱动程序在收到 D3DDP2OP \_ servicecontext.createquery operation 代码以及命令流中的 [**D3DHAL \_ DP2CREATEQUERY**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2createquery) 结构后，为查询创建资源。

2.  该驱动程序在接收到 D3DDP2OP ISSUEQUERY 操作代码后开始处理查询，并 \_ 在命令流中将其与 [**D3DHAL \_ DP2ISSUEQUERY**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2issuequery) 结构一起处理。

3.  如果以前使用 D3DDP2OP ISSUEQUERY 操作完成了提交的查询 \_ ，则驱动程序将在[**D3DHAL \_ DRAWPRIMITIVES2DATA**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_drawprimitives2data)结构的**dwErrorOffset**成员中设置响应缓冲区的大小，并将 ddrval D3DHAL 的**DRAWPRIMITIVES2DATA**成员设置 \_ 为 D3D \_ OK，以便成功完成。 驱动程序用传出流中的响应缓冲区覆盖传入 [命令流](command-stream.md) 中的命令缓冲区。 驱动程序将 [**D3DHAL \_ DP2RESPONSE**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2response) 结构的 **BCOMMAND** 成员设置为 D3DDP2OP \_ RESPONSEQUERY，以指示响应缓冲区中有以前发出的查询的响应。 响应缓冲区中的每个 [**D3DHAL \_ DP2RESPONSEQUERY**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2responsequery) 后跟以下与查询相关的数据：

    -   对于 D3DQUERYTYPE 事件，则为 BOOL \_ 。 在 \_ 为事件响应 D3DDP2OP RESPONSEQUERY 之前，驱动程序必须确保图形处理单元 (GPU) 完成了与该事件相关的所有 [**D3DHAL \_ DP2OPERATION**](/windows-hardware/drivers/ddi/d3dhal/ne-d3dhal-_d3dhal_dp2operation) 操作的处理。 也就是说，仅在事件的问题结束状态发生之后，驱动程序才 \_ 会响应。 在驱动程序将事件设置为 "已终止" 状态 (设置为 **TRUE**) 之前，可能需要使用 GPU 来执行刷新，以确保像素完成光栅化、blts 已完成，不再使用资源等。 响应时，驱动程序必须始终将事件的布尔值设置为 **TRUE** 。
    -   D3DQUERYTYPE 封闭的 DWORD \_ 。 驱动程序将此 DWORD 设置为在查询开始和结束之间的所有基元的 z 测试传递的像素数。 如果深度缓冲区为多级采样，则驱动程序将确定样本数的像素数。 但是，如果显示设备能够按采样 z 测试准确性，则通常应将转换为像素数。 然后，应用程序可以检查0的封闭结果，以有效地表示 "完全封闭像素"。 将多级采样数量转换为像素数量的驱动程序应检测呈现目标多级
    -   [**D3DDEVINFO \_**](/windows-hardware/drivers/ddi/d3d9types/ns-d3d9types-_d3ddevinfo_vcache)D3DQUERYTYPE VCACHE 的 VCACHE 结构 \_ 。

    如果提供的命令缓冲区太小，驱动程序无法写入所有响应，则驱动程序还会 \_ 在传出流中发送 D3DDP2OP RESPONSECONTINUE。

4.  如果运行时确定驱动程序的 [**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) 函数 succeeded (**ddrval** 成员 D3DHAL \_ DRAWPRIMITIVES2DATA 设置为 D3D \_ OK) ，则运行时将检查 dwErrorOffset D3DHAL 的 **DRAWPRIMITIVES2DATA** 成员， \_ 以确定驱动程序是否可以使用响应。 如果没有可用的响应，则此 **dwErrorOffset** 成员为零;否则， **dwErrorOffset** 是响应缓冲区的大小（以字节为单位）。 因此，当 *D3dDrawPrimitives2* 的成功 (**DDRVAL** 设置为 D3D \_ OK) 时，驱动程序必须确保当响应可用时，该驱动程序必须将 **dwErrorOffset** 设置为非零值。

5.  运行时分析返回的响应缓冲区，并更新其内部数据结构。

6.  如果驱动程序发送 D3DDP2OP \_ RESPONSECONTINUE，则运行时在传入 [命令流](command-stream.md) 中提交一个空的命令缓冲区，以便驱动程序可以继续写入更多响应。 驱动程序必须确保它可以处理空的命令缓冲区。

 

