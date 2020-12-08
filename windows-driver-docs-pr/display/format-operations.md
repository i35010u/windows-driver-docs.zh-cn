---
title: 格式操作
description: 格式操作
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，纹理格式列表
- 纹理格式列出 WDK DirectX 8。0
- DPIXELFORMAT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71e250f79dd8f20dfae8887acdb1a7eb60e593d1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799691"
---
# <a name="format-operations"></a>格式操作


## <span id="ddk_format_operations_gg"></span><span id="DDK_FORMAT_OPERATIONS_GG"></span>


在报告受支持的图面格式时，DirectX 8.0 驱动程序还必须指示可对该格式的表面执行哪些操作。 可以通过 [**DDPIXELFORMAT**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)结构的 **dwOperations** 字段报告像素格式支持的操作。 驱动程序应将此字段设置为该格式的所有支持操作的逻辑组合。

 

