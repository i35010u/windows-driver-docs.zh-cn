---
title: 验证渲染器目标的有效性
description: 验证渲染器目标的有效性
keywords:
- 呈现目标 WDK DirectX 9.0，验证有效性
- 验证呈现器目标 WDK DirectX 9。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9847ff824d2af689f8d915f8f5ae46609fdf6103
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799589"
---
# <a name="verifying-validity-of-render-target"></a>验证渲染器目标的有效性


## <span id="ddk_verifying_validity_of_render_target_gg"></span><span id="DDK_VERIFYING_VALIDITY_OF_RENDER_TARGET_GG"></span>


在使用呈现目标之前，DirectX 9.0 版本驱动程序必须验证其内部呈现目标是否有效，因为 DirectX 9.0 运行时允许应用程序将呈现目标设置为 **NULL**。 与此相反，DirectX 8.1 和更早版本的运行时保证呈现目标对于 Direct3D 上下文始终有效。

 

 





