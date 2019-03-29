---
title: EngExtCpp 扩展库
description: EngExtCpp 扩展库
ms.assetid: 8c7ce3f8-46c4-408c-aab5-00d654bddfcd
keywords:
- EngExtCpp 扩展库
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e278db7c6d5192790ea2ae89d10d52935c8a0d57
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562607"
---
# <a name="engextcpp-extension-libraries"></a>EngExtCpp 扩展库


## <span id="ddk_anatomy_of_a_dbgeng_extension_dll_dbx"></span><span id="DDK_ANATOMY_OF_A_DBGENG_EXTENSION_DLL_DBX"></span>


EngExtCpp 扩展插件库是使用 EngExtCpp.h 中找到的 EngExtCpp 扩展框架的 DLL。 由调试器引擎加载此库时，额外功能或任务的自动化执行用户模式下还是在 Microsoft Windows 上的内核模式调试时可以提供其方法和函数。

EngExtCpp 扩展框架构建的[DbgEng 扩展框架](writing-dbgeng-extension-code.md)。 它提供与调试器引擎进行交互的同一调试器引擎 API。 但它还提供附加的功能来简化常见任务。

如果您执行的 Windows 调试工具的完整安装，可以在 sdk 中找到名为"extcpp"的示例 EngExtCpp 扩展\\示例\\extcpp 的安装目录的子目录。

### <a name="span-idextclassandextextensionspanspan-idextclassandextextensionspanextclass-and-extextension"></a><span id="ext_class_and_extextension"></span><span id="EXT_CLASS_AND_EXTEXTENSION"></span>EXT\_类和 ExtExtension

EngExtCpp 扩展核心库是一份[ **EXT\_类**](https://msdn.microsoft.com/library/windows/hardware/ff544508)类。 EngExtCpp 扩展库将提供此类，该类包含所有扩展命令和格式设置由库导出的结构的方法的实现。

EXT\_类是一个的子类[ **ExtExtension**](https://msdn.microsoft.com/library/windows/hardware/ff543981)。 使用创建此类的一个实例[ **EXT\_DECLARE\_GLOBALS** ](https://msdn.microsoft.com/library/windows/hardware/ff544527) macro，它必须出现在扩展库的源代码文件中的一次。

加载扩展插件库时， [**初始化**](https://msdn.microsoft.com/library/windows/hardware/ff550945)类的方法调用由引擎使用，并且[ **Uninitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff558961)在卸载类之前调用方法。 此外，方法[ **OnSessionActive**](https://msdn.microsoft.com/library/windows/hardware/ff552312)， [ **OnSessionInactive**](https://msdn.microsoft.com/library/windows/hardware/ff552318)， [ **OnSessionAccessible**](https://msdn.microsoft.com/library/windows/hardware/ff552310)，并[ **OnSessionInaccessible** ](https://msdn.microsoft.com/library/windows/hardware/ff552315)由要通知的扩展库中的调试会话的状态的引擎调用。

### <a name="span-idextensioncommandsspanspan-idextensioncommandsspanextension-commands"></a><span id="extension_commands"></span><span id="EXTENSION_COMMANDS"></span>扩展命令

[ **EXT\_类**](https://msdn.microsoft.com/library/windows/hardware/ff544508)类可以包含多种用于执行扩展命令的方法。 每个扩展命令声明中 EXT\_类使用的类[ **EXT\_命令\_方法**](https://msdn.microsoft.com/library/windows/hardware/ff544517)宏。 使用定义的命令实现[ **EXT\_命令**](https://msdn.microsoft.com/library/windows/hardware/ff544514)宏。

### <a name="span-idknownstructuresspanspan-idknownstructuresspanknown-structures"></a><span id="known_structures"></span><span id="KNOWN_STRUCTURES"></span>已知的结构

[ **EXT\_类**](https://msdn.microsoft.com/library/windows/hardware/ff544508)类可以包含多种使用方法[ *ExtKnownStructMethod* ](https://msdn.microsoft.com/library/windows/hardware/ff543989)原型。 由输出格式类型实例的特定结构的引擎，可以使用方法。

### <a name="span-idprovidedvaluesspanspan-idprovidedvaluesspanprovided-values"></a><span id="provided_values"></span><span id="PROVIDED_VALUES"></span>提供的值

[ **EXT\_类**](https://msdn.microsoft.com/library/windows/hardware/ff544508)类可以包含多种使用方法**ExtProvideValueMethod**原型。 方法可以由引擎，用于评估插件提供的一些伪寄存器。

 

 





