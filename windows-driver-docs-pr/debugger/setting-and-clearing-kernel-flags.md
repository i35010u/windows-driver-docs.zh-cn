---
title: 设置和清除内核标志
description: 设置和清除内核标志
ms.assetid: 6bca8007-2d9f-4b93-b5fb-300c262604c8
keywords:
- GFlags、 内核标志
- GFlags、 运行时间设置
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6fe55fef0fd81b02ca7b5a976e3bbc2e81d5a160
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523557"
---
# <a name="setting-and-clearing-kernel-flags"></a>设置和清除内核标志


## <span id="ddk_setting_and_clearing_kernel_mode_flags_dtools"></span><span id="DDK_SETTING_AND_CLEARING_KERNEL_MODE_FLAGS_DTOOLS"></span>


内核标志设置，也称为"运行设置"会影响整个系统。 它们会立即生效时避免重新启动，但如果你关闭或重新启动系统，它们会丢失。

内核设置优先于注册表设置在运行时，但在关闭或重新启动系统时，内核标志设置都将丢失，再次是有效的注册表设置。

**若要设置和清除内核标志**

1.  单击**内核标志**选项卡。

    下面的屏幕截图所示**内核标志**Windows Vista 中的选项卡。

    ![windows vista 中内核标志选项卡的屏幕截图 ](images/gflags-kernel.png)

2.  设置或清除标志，通过选中或清除关联的标志的复选框。

3.  已选择或清除所有所需的标志，请单击**应用**。

 

 





