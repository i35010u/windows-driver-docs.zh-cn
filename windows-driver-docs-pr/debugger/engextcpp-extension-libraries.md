---
title: EngExtCpp 扩展库
description: EngExtCpp 扩展库
ms.assetid: 8c7ce3f8-46c4-408c-aab5-00d654bddfcd
keywords:
- EngExtCpp 扩展，库
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f345fb6d9e66cf21e706c1b5f510618f2befb3f3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837759"
---
# <a name="engextcpp-extension-libraries"></a>EngExtCpp 扩展库


## <span id="ddk_anatomy_of_a_dbgeng_extension_dll_dbx"></span><span id="DDK_ANATOMY_OF_A_DBGENG_EXTENSION_DLL_DBX"></span>


EngExtCpp 扩展库是使用 EngExtCpp 中找到的 EngExtCpp 扩展框架的 DLL。 如果调试器引擎加载此库，则在 Microsoft Windows 上执行用户模式或内核模式调试时，其方法和函数可以提供额外的任务功能或自动化任务。

EngExtCpp 扩展框架建立在[DbgEng 扩展框架](writing-dbgeng-extension-code.md)的基础之上。 它提供相同的调试器引擎 API 用于与调试器引擎交互。 但它还提供了其他功能来简化常见任务。

如果已执行 Windows 调试工具的完全安装，则可以在安装目录的 sdk\\示例\\extcpp 子目录中找到一个名为 "extcpp" 的示例 EngExtCpp 扩展。

### <a name="span-idext_class_and_extextensionspanspan-idext_class_and_extextensionspanext_class-and-extextension"></a><span id="ext_class_and_extextension"></span><span id="EXT_CLASS_AND_EXTEXTENSION"></span>EXT\_类和 ExtExtension

EngExtCpp 扩展库的核心是[**EXT\_类**](https://docs.microsoft.com/previous-versions/ff544508(v=vs.85))的单个实例。 EngExtCpp 扩展库将提供此类的实现，该类包含库导出的格式设置结构的所有扩展命令和方法。

EXT\_类是[**ExtExtension**](https://msdn.microsoft.com/library/windows/hardware/ff543981)的子类。 此类的单个实例是使用[**EXT\_\_GLOBALS**](https://docs.microsoft.com/previous-versions/ff544527(v=vs.85))宏创建的，该宏必须只在扩展库的源文件中出现一次。

加载扩展库时，将由引擎调用类的[**Initialize**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff550945(v=vs.85))方法，并在卸载类之前调用 Initialize[**方法。** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff558961(v=vs.85)) 此外，引擎调用[**OnSessionActive**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff552312(v=vs.85))、 [**OnSessionInactive**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff552318(v=vs.85))、 [**OnSessionAccessible**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff552310(v=vs.85))和[**OnSessionInaccessible**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff552315(v=vs.85))方法，以通知扩展库调试会话的状态。

### <a name="span-idextension_commandsspanspan-idextension_commandsspanextension-commands"></a><span id="extension_commands"></span><span id="EXTENSION_COMMANDS"></span>扩展命令

[**EXT\_类**](https://docs.microsoft.com/previous-versions/ff544508(v=vs.85))可以包含多个用于执行扩展命令的方法。 使用[**ext\_命令\_方法**](https://docs.microsoft.com/windows-hardware/drivers/ddi/engextcpp/nf-engextcpp-ext_command_method)宏在 EXT\_类中声明每个扩展命令。 使用[**EXT\_命令**](https://docs.microsoft.com/windows-hardware/drivers/ddi/engextcpp/nf-engextcpp-ext_command)宏定义命令的实现。

### <a name="span-idknown_structuresspanspan-idknown_structuresspanknown-structures"></a><span id="known_structures"></span><span id="KNOWN_STRUCTURES"></span>已知结构

[**EXT\_类**](https://docs.microsoft.com/previous-versions/ff544508(v=vs.85))可以包含多个使用[*ExtKnownStructMethod*](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))原型的方法。 引擎可使用这些方法来设置特定结构类型的实例的格式以进行输出。

### <a name="span-idprovided_valuesspanspan-idprovided_valuesspanprovided-values"></a><span id="provided_values"></span><span id="PROVIDED_VALUES"></span>提供的值

[**EXT\_类**](https://docs.microsoft.com/previous-versions/ff544508(v=vs.85))可以包含多个使用**ExtProvideValueMethod**原型的方法。 引擎可使用这些方法来评估扩展提供的一些伪寄存器。

 

 





