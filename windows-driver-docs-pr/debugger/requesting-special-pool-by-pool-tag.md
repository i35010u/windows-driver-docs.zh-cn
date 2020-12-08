---
title: 按池标记请求特殊池
description: 按池标记请求特殊池
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0be1eca0a5c68c7549e93c918590ee90ae7d599c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798367"
---
# <a name="requesting-special-pool-by-pool-tag"></a>按池标记请求特殊池

## <span id="ddk_requesting_special_pool_for_allocations_with_a_specified_pool_tag_"></span><span id="DDK_REQUESTING_SPECIAL_POOL_FOR_ALLOCATIONS_WITH_A_SPECIFIED_POOL_TAG_"></span>

你可以为使用指定池标记的所有分配请求特殊池。 一次只能有一个系统上的一个池标记与内核特殊池请求相关联。

在 Windows Vista 和更高版本的 Windows 中，还可以使用命令行来请求按池标记的特殊池。 有关信息，请参阅 [**GFlags 命令**](gflags-commands.md)。

**请求按池标记的特殊池**

1. 选择 " **系统注册表** " 选项卡或 " **内核标志** " 选项卡。

   在 Windows Vista 和更高版本的 Windows 上，此选项在两个选项卡上都可用。 在早期版本的 Windows 上，它仅在 " **系统注册表** " 选项卡上可用。

2. 在 " **内核特殊池标记** " 部分中，单击 " **文本**"，然后为标记键入四字符模式。

   标记可以包含 **？**  (单字符) 和 * *\** _ (多个字符) 通配符。 例如，Fat \_ 或 Av？4。

3. 以下屏幕截图显示了在 "系统注册表" 选项卡上以文本形式输入的标记。

   !["系统注册表" 选项卡上作为文本输入的标记的屏幕截图](images/gflags-specialpool-text.png)

4. 单击“应用” 。

   单击 " **应用**" 时，GFlags 会将所选内容从 **文本** 更改为 **Hex** ，并以十六进制值的形式显示 ASCII 字符， (低字节序) 顺序。 例如，如果键入 **Tag1**，则 GFlags 会将标记显示为 **0x31676154** (1gaT) 。 这就是将其存储在注册表中并由调试器和其他工具显示的方式。

   下图显示了单击 " **应用**" 的效果。

   ![显示单击 "应用" 效果的屏幕截图](images/gflags-specialpool-hex.png)

### <a name="span-idcommentsspanspan-idcommentsspanremarks"></a><span id="comments"></span><span id="COMMENTS"></span>标记

若要有效地使用此功能，请确保您的驱动程序或其他内核模式程序使用唯一的池标记。 如果您怀疑您的驱动程序正在使用所有特殊池，请考虑在您的代码中使用多个池标记。 然后，可以多次测试您的驱动程序，并在每个测试中为一个池标记分配特殊的池。

另外，请选择一个具有大于系统页面大小的十六进制值的池标记。 对于内核模式代码，如果输入的池标记的值小于页面 \_ 大小，则 Gflags 会为大小在相应范围内的所有分配请求特殊池，并请求具有等效池标记的分配的特殊池。 例如，如果选择的大小为 **30**，则会将特殊池用于大小介于17到32字节之间的所有分配，并用于使用池标记0x0030 的分配。
