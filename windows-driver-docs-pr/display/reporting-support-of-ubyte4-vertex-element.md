---
title: 报告 UBYTE4 顶点元素支持
description: 报告 UBYTE4 顶点元素支持
keywords:
- UBYTE4 顶点元素 WDK DirectX 9。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44d0208b75d4b395a98586e074bfcf571cbfff88
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837802"
---
# <a name="reporting-support-of-ubyte4-vertex-element"></a>报告 UBYTE4 顶点元素支持


## <span id="ddk_reporting_support_of_ubyte4_vertex_element_gg"></span><span id="DDK_REPORTING_SUPPORT_OF_UBYTE4_VERTEX_ELEMENT_GG"></span>


DirectX 9.0 版本驱动程序必须通过 \_ 在 D3DCAPS9 结构的 **DeclTypes** 成员中设置 D3DDTCAPS UBYTE4 位来报告对 UBYTE4 顶点元素类型的支持。 若要指示 UBYTE4 顶点元素类型的 nonsupport，驱动程序不会设置 D3DDTCAPS \_ UBYTE4 位。 相反，DirectX 8.1 和更早版本的驱动程序将 D3DVTXPCAPS \_ NO \_ VSDT \_ UBYTE4 位设置为 UBYTE4 顶点元素类型的 nonsupport。

 

 





