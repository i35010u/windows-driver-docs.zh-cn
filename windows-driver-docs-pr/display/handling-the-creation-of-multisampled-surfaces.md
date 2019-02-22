---
title: 处理多级采样曲面的创建
description: 处理多级采样曲面的创建
ms.assetid: 78557c9d-b741-4eb9-b8e2-56387cad80c4
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，多重采样呈现创建
- multisample 呈现 WDK DirectX 8.0，创建
- 呈现 multisamples WDK DirectX 8.0 中，创建
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3205ee3101c9249ffd0061c8d924b06169d4a201
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541881"
---
# <a name="handling-the-creation-of-multisampled-surfaces"></a>处理多级采样曲面的创建


## <span id="ddk_handling_the_creation_of_multisampled_surfaces_gg"></span><span id="DDK_HANDLING_THE_CREATION_OF_MULTISAMPLED_SURFACES_GG"></span>


创建一个多级采样的面后，可以中找到的样本数**ddsCapsEx.dwCaps3**的[ **DD\_图面\_详细**](https://msdn.microsoft.com/library/windows/hardware/ff551737)结构。 此字段将包含的一个枚举类型 D3DMULTISAMPLE 值\_类型。 它不是像一组标志**wFlipMSTypes**或**wBltMSTypes**。 如果一个面不是多级采样， **dwCaps3**具有值 D3DMULTISAMPLE\_NONE (0)。

在确定是否可以或不满足的多重采样表面的创建请求时，驱动程序应不考虑在内的当前值的 D3DRS\_MULTISAMPLEANTIALIAS 呈现状态。 不允许驱动程序失败的请求设置 D3DRS\_MULTISAMPLEANTIALIAS **FALSE**。 因此，应在上下文强制执行多重采样呈现的能力会影响创建时任何限制即使 D3DRS\_MULTISAMPLEANTIALIAS 是**FALSE**在该时间。

 

 





