---
title: 按池标记请求特殊池
description: 按池标记请求特殊池
ms.assetid: 201eb8a5-b38b-4625-853d-448488214e52
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc71c56b19d726ab0d558f8fad0b413bd039e95a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382121"
---
# <a name="requesting-special-pool-by-pool-tag"></a>按池标记请求特殊池


## <span id="ddk_requesting_special_pool_for_allocations_with_a_specified_pool_tag_"></span><span id="DDK_REQUESTING_SPECIAL_POOL_FOR_ALLOCATIONS_WITH_A_SPECIFIED_POOL_TAG_"></span>


你可以请求特殊池使用指定的池标记的所有分配。 在系统上的只有一个池标记可以一次是与内核特殊池请求相关联。

在 Windows Vista 和更高版本的 Windows 中，还可以使用命令行来请求特殊标记，池的池。 有关信息，请参阅[ **GFlags 命令**](gflags-commands.md)。

**若要请求特殊标记，池的池**

1. 选择**系统注册表**选项卡或**内核标志**选项卡。

   在 Windows Vista 和更高版本的 Windows 上，此选项才可用两个选项卡。 在早期版本的 Windows，它是仅适用于**系统注册表**选项卡。

2. 在中**内核特殊池标记**部分中，单击**文本**，然后键入标记的四个字符模式。

   标记可以包含 **？** （单个字符） 和**\\*** （多个字符） 通配符字符。 例如，Fat\*或 Av？ 4。

3. 下面的屏幕截图显示以文本形式输入系统注册表选项卡上的标记。

   ![以文本形式输入系统注册表选项卡上的标记的屏幕截图](images/gflags-specialpool-text.png)

4. 单击 **“应用”**。

   当您单击**应用**，GFlags 更改从所选**文本**到**十六进制**并将 ASCII 字符显示为十六进制值反向 （较低字节序） 顺序。 例如，如果键入**标记 1**，显示为标记 GFlags **0x31676154** (1gaT)。 这是它是存储在注册表中并显示调试器和其他工具的方法。

   下图显示单击的效果**应用**。

   ![屏幕截图的显示单击的效果应用](images/gflags-specialpool-hex.png)

### <a name="span-idcommentsspanspan-idcommentsspanremarks"></a><span id="comments"></span><span id="COMMENTS"></span>备注

若要有效地使用此功能，请确保您的驱动程序或其他内核模式程序使用的唯一池标记。 如果您怀疑您的驱动程序使用所有特殊的池，请考虑在代码中使用多个池标记。 你随后可以测试您的驱动程序多次，将特殊的池分配给每个测试中的一个池标记。

此外，选择具有大于系统页面大小的十六进制值的池标记。 有关内核模式代码，如果输入池标记的值小于页面\_大小，Gflags 请求其大小在相应范围内，并请求特殊池分配，则使用等效的池标记的所有分配的特殊池。 例如，如果您选择的大小**30**，对于大小，为 17 到 32 个字节之间的所有分配和分配，则使用池标记 0x0030，将使用特殊的池。

 

 





