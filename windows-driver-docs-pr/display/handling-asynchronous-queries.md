---
title: 处理异步查询
description: 处理异步查询
ms.assetid: b5e289db-eb9f-46e6-b221-4aa6661a9ce1
keywords:
- 异步查询操作 WDK DirectX 9。0
- 查询操作 WDK DirectX 9.0，异步
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ded9cb09e581d8b634d4a8ad08e4539eb4f135c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838912"
---
# <a name="handling-asynchronous-queries"></a>处理异步查询


## <span id="ddk_handling_asynchronous_queries_gg"></span><span id="DDK_HANDLING_ASYNCHRONOUS_QUERIES_GG"></span>


驱动程序处理在其[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)函数的[命令流](command-stream.md)中接收的异步查询操作，如以下序列中所述：

1.  驱动程序在接收到 D3DDP2OP\_SERVICECONTEXT.CREATEQUERY 操作代码以及命令流中的[**D3DHAL\_DP2CREATEQUERY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2createquery)结构后，为查询创建资源。

2.  驱动程序在接收到 D3DDP2OP\_ISSUEQUERY 操作代码以及命令流中的[**D3DHAL\_DP2ISSUEQUERY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2issuequery)结构后开始处理查询。

3.  如果以前使用 D3DDP2OP\_ISSUEQUERY 操作完成提交的查询，则驱动程序将设置[**D3DHAL\_DRAWPRIMITIVES2DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_drawprimitives2data)结构的**dwErrorOffset**成员中响应缓冲区的大小，并设置D3DHAL 的 ddrval 成员\_DRAWPRIMITIVES2DATA 到 D3D\_"确定" 成功完成。 驱动程序用传出流中的响应缓冲区覆盖传入[命令流](command-stream.md)中的命令缓冲区。 驱动程序将[**D3DHAL\_DP2RESPONSE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2response)结构的**bCommand**成员设置为 D3DDP2OP\_RESPONSEQUERY，以指示响应缓冲区中有以前发出的查询的响应。 响应缓冲区中的每个[**D3DHAL\_DP2RESPONSEQUERY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2responsequery)后跟以下与查询相关的数据：

    -   D3DQUERYTYPE\_事件的布尔值。 在为事件响应 D3DDP2OP\_RESPONSEQUERY 之前，驱动程序必须确保图形处理单元（GPU）处理完与事件相关的所有[**D3DHAL\_DP2OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ne-d3dhal-_d3dhal_dp2operation)操作。 也就是说，驱动程序只在事件的问题\_结束状态之后才会响应。 在驱动程序将事件设置为 "已终止" 状态（设置为 " **TRUE**"）之前，可能需要使用 GPU 执行刷新，以确保像素完成了光栅化、blts 已完成、资源不再被使用等。 响应时，驱动程序必须始终将事件的布尔值设置为**TRUE** 。
    -   D3DQUERYTYPE\_封闭的 DWORD。 驱动程序将此 DWORD 设置为在查询开始和结束之间的所有基元的 z 测试传递的像素数。 如果深度缓冲区为多级采样，则驱动程序将确定样本数的像素数。 但是，如果显示设备能够按采样 z 测试准确性，则通常应将转换为像素数。 然后，应用程序可以检查0的封闭结果，以有效地表示 "完全封闭像素"。 将多级采样数量转换为像素数量的驱动程序应检测呈现目标多级
    -   D3DQUERYTYPE\_VCACHE 的[**D3DDEVINFO\_VCACHE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d9types/ns-d3d9types-_d3ddevinfo_vcache)结构。

    如果提供的命令缓冲区太小，驱动程序无法写入所有响应，则驱动程序还会将 D3DDP2OP\_RESPONSECONTINUE 发送到传出流中。

4.  如果运行时确定驱动程序的[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)函数 SUCCEEDED （D3DHAL\_DRAWPRIMITIVES2DATA 的**ddrval**成员设置为 D3D\_正常），则运行时检查 dwErrorOffset 的**D3DHAL**成员\_DRAWPRIMITIVES2DATA 来确定驱动程序是否可以使用响应。 如果没有可用的响应，则此**dwErrorOffset**成员为零;否则， **dwErrorOffset**是响应缓冲区的大小（以字节为单位）。 因此，在*D3dDrawPrimitives2*成功时（**DDRVAL**设置为 D3D\_"确定"），驱动程序必须确保当响应可用时，该驱动程序必须将**dwErrorOffset**设置为非零值。

5.  运行时分析返回的响应缓冲区，并更新其内部数据结构。

6.  如果驱动程序向 D3DDP2OP 发送了\_RESPONSECONTINUE，则运行时将在传入[命令流](command-stream.md)中提交一个空的命令缓冲区，以便驱动程序可以继续写入更多响应。 驱动程序必须确保它可以处理空的命令缓冲区。

 

 





