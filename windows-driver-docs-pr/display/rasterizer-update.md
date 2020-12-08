---
title: 光栅器更新
description: 光栅器更新
keywords:
- rasterizers WDK Direct3D
- 生产 rasterizers WDK Direct3D
- 引用 rasterizers WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89eeec8b12e230f9ae2c40b677ac174f33d69139
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810087"
---
# <a name="rasterizer-update"></a>光栅器更新


## <span id="ddk_rasterizer_update_gg"></span><span id="DDK_RASTERIZER_UPDATE_GG"></span>


已将引用光栅化程序提取到单独的 DLL 中，以便能够以异步方式将其他 WHQL 测试添加到 (按季度的典型) 。 已对其进行更新，以支持在核心中或作为要求保证实现一致性的扩展添加到 API 的任何光栅程序级别操作。

生产光栅化程序可能不会更新以支持这些技术，因为在软件中运行时，顶点级别的环境映射可能比像素级别更快。

对于标识的关键事例，此光栅化程序可能会升级。

 

 





