---
title: 格式操作
description: 格式操作
ms.assetid: 242e5b5a-4184-487a-aeda-19149caa941b
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，纹理格式列表
- 纹理格式列出 WDK DirectX 8。0
- DPIXELFORMAT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f63542eed5d65a827e3bc05e04c12a7cf0adbb9
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067432"
---
# <a name="format-operations"></a>格式操作


## <span id="ddk_format_operations_gg"></span><span id="DDK_FORMAT_OPERATIONS_GG"></span>


在报告受支持的图面格式时，DirectX 8.0 驱动程序还必须指示可对该格式的表面执行哪些操作。 可以通过[**DDPIXELFORMAT**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)结构的**dwOperations**字段报告像素格式支持的操作。 驱动程序应将此字段设置为该格式的所有支持操作的逻辑组合。

 

