---
title: 报告流偏移量支持
description: 报告流偏移量支持
keywords:
- 流偏移 WDK DirectX 9.0，报表支持
- 顶点流偏移 WDK DirectX 9.0，报告支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 068dcf7d222b616044abd82f78bfe0ba1655101a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789989"
---
# <a name="reporting-support-for-stream-offsets"></a>报告流偏移量支持


## <span id="ddk_reporting_support_for_stream_offsets_gg"></span><span id="DDK_REPORTING_SUPPORT_FOR_STREAM_OFFSETS_GG"></span>


DirectX 9.0 版本驱动程序必须通过设置 \_ D3DCAPS9 结构的 **DevCaps2** 成员中的 D3DDEVCAPS2 STREAMOFFSET 功能位来指示支持流偏移量。

 

 





