---
title: 设置和清除内核标志
description: 设置和清除内核标志
keywords:
- GFlags，内核标志
- GFlags，运行时设置
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1533711541ab4dc6aa49e6baa4dd4e4647398a60
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840429"
---
# <a name="setting-and-clearing-kernel-flags"></a>设置和清除内核标志


## <span id="ddk_setting_and_clearing_kernel_mode_flags_dtools"></span><span id="DDK_SETTING_AND_CLEARING_KERNEL_MODE_FLAGS_DTOOLS"></span>


内核标志设置（也称为 "运行时设置"）会影响整个系统。 它们会立即生效，无需重新启动，但当你关闭或重新启动系统时，它们会丢失。

内核设置在运行时优先于注册表设置，但当你关闭或重新启动系统时，内核标志设置会丢失，并且注册表设置将再次生效。

**设置和清除内核标志**

1.  单击 " **内核标志** " 选项卡。

    以下屏幕截图显示 Windows Vista 中的 " **内核标志** " 选项卡。

    ![windows vista 中的 "内核标志" 选项卡的屏幕截图 ](images/gflags-kernel.png)

2.  通过选中或清除与标志关联的复选框来设置或清除标志。

3.  如果选择或清除了所需的所有标志，请单击 " **应用**"。

 

 





