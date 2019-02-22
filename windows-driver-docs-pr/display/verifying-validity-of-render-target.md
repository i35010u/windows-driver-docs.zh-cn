---
title: 验证呈现器目标的有效性
description: 验证呈现器目标的有效性
ms.assetid: 316ecd58-996a-4277-b2dc-4424c96d8a56
keywords:
- 呈现器目标 WDK DirectX 9.0 中，验证有效性
- 验证呈现器目标 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af45a846922aa41edd4bfa375f5ca74359c37cb4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522506"
---
# <a name="verifying-validity-of-render-target"></a>验证呈现器目标的有效性


## <span id="ddk_verifying_validity_of_render_target_gg"></span><span id="DDK_VERIFYING_VALIDITY_OF_RENDER_TARGET_GG"></span>


版本驱动程序必须验证其内部的呈现器目标之前使用呈现器目标，因为 DirectX 9.0 运行时允许应用程序设置是否有效 DirectX 9.0 呈现器目标的**NULL**。 与此相反，DirectX 8.1 和更早呈现器目标的运行时保证始终是 Direct3D 上下文有效。

 

 





