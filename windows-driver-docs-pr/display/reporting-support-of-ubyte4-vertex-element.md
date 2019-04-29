---
title: 报告 UBYTE4 顶点元素支持
description: 报告 UBYTE4 顶点元素支持
ms.assetid: d5091ceb-71de-4310-95d9-c52361772ebc
keywords:
- UBYTE4 顶点元素 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 637f36ad7a45e1b427d3a10b2c3c06ead731ff79
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383234"
---
# <a name="reporting-support-of-ubyte4-vertex-element"></a>报告 UBYTE4 顶点元素支持


## <span id="ddk_reporting_support_of_ubyte4_vertex_element_gg"></span><span id="DDK_REPORTING_SUPPORT_OF_UBYTE4_VERTEX_ELEMENT_GG"></span>


DirectX 9.0 版本驱动程序必须报告 UBYTE4 顶点元素类型的支持通过设置 D3DDTCAPS\_UBYTE4 位**DeclTypes** D3DCAPS9 结构中的成员。 若要指示 nonsupport UBYTE4 顶点元素类型，该驱动程序不会设置 D3DDTCAPS\_UBYTE4 位。 与此相反，DirectX 8.1 和早期的驱动程序设置 D3DVTXPCAPS\_否\_VSDT\_UBYTE4 位指示 nonsupport UBYTE4 顶点元素类型。

 

 





