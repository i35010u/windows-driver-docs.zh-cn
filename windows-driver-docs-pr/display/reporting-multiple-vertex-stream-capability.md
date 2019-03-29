---
title: 报告多个顶点流功能
description: 报告多个顶点流功能
ms.assetid: 61441576-0e5d-4c6d-9e36-dcd8c59c8db0
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，多个顶点流
- 多个顶点流式传输 WDK DirectX 8.0
- 顶点多个流 WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d229a5b39a2e40b82d048c0f2b60c27349e3317
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566581"
---
# <a name="reporting-multiple-vertex-stream-capability"></a>报告多个顶点流功能


## <span id="ddk_reporting_multiple_vertex_stream_capability_gg"></span><span id="DDK_REPORTING_MULTIPLE_VERTEX_STREAM_CAPABILITY_GG"></span>


驱动程序报告的值设置支持多个顶点流的能力**MaxStreams** D3DCAPS8 结构的字段。 支持多个顶点流的驱动程序应指定大于 1 的值。 不支持多个顶点流 DX8 级别驱动程序应设置**MaxStreams**到其中一个。 没有 DX8 级的驱动程序应指定此字段的零值。 该驱动程序还应设置**MaxStreamStride**字段 （以字节为单位） 顶点流中的顶点元素之间的最大支持跨距。

 

 





