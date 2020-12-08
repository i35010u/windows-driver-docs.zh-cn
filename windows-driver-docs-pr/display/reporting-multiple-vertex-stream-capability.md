---
title: 报告多个顶点流功能
description: 报告多个顶点流功能
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，多个顶点流
- 多个顶点流 WDK DirectX 8。0
- 顶点多流 WDK DirectX 8。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e7a52f19a77a8c038619d15efd96c97819d333d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815447"
---
# <a name="reporting-multiple-vertex-stream-capability"></a>报告多个顶点流功能


## <span id="ddk_reporting_multiple_vertex_stream_capability_gg"></span><span id="DDK_REPORTING_MULTIPLE_VERTEX_STREAM_CAPABILITY_GG"></span>


驱动程序通过设置 D3DCAPS8 结构的 **MaxStreams** 字段的值，来报告支持多个顶点流的能力。 支持多个顶点流的驱动程序应指定一个大于1的值。 不支持多个顶点流的 DX8 级别驱动程序应将 **MaxStreams** 设置为1。 对于此字段，不应将 DX8 级别驱动程序的值指定为零。 驱动程序还应将 " **MaxStreamStride** " 字段设置为顶点流中顶点元素之间的最大支持跨距 (以字节为单位) 。

 

 





