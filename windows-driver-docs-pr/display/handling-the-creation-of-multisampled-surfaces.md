---
title: 处理多重采样图面的创建
description: 处理多重采样图面的创建
ms.assetid: 78557c9d-b741-4eb9-b8e2-56387cad80c4
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，多级显示，创建
- 以多级显示方式呈现 WDK DirectX 8.0，创建
- 呈现 multisamples WDK DirectX 8.0，创建
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a7ec6fe3775948d88f09ad45688b4e767d505ec
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063086"
---
# <a name="handling-the-creation-of-multisampled-surfaces"></a>处理多重采样图面的创建


## <span id="ddk_handling_the_creation_of_multisampled_surfaces_gg"></span><span id="DDK_HANDLING_THE_CREATION_OF_MULTISAMPLED_SURFACES_GG"></span>


在创建多级采样表面时，可以在[**DD \_ 表面 \_ **](/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_more)的**ddsCapsEx. dwCaps3**中找到示例数。 此字段保存枚举类型 D3DMULTISAMPLE 类型的值之一 \_ 。 它不是像 **wFlipMSTypes** 或 **wBltMSTypes**这样的域。 如果图面不是多级采样，则 **dwCaps3** 的值 D3DMULTISAMPLE \_ 无 (0) 。

确定是否可以满足对多级显示图面的创建请求时，驱动程序不应考虑 D3DRS \_ MULTISAMPLEANTIALIAS 呈现状态的当前值。 不允许驱动程序对设置 D3DRS \_ MULTISAMPLEANTIALIAS **FALSE**的请求失败。 因此，即使 \_ 此时 D3DRS MULTISAMPLEANTIALIAS 为 **FALSE** ，也应在上下文创建时间强制执行任何影响执行多级显示呈现功能的限制。

 

