---
title: 使用 WdbgExts 扩展回调
description: 使用 WdbgExts 扩展回调
ms.assetid: b9a2f30a-b09c-43eb-b105-a6b0ffdb1342
keywords:
- WdbgExts 扩展，使用的回调
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d58272bc50854d1b0e9f2fa11012cfbdbd68027
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390536"
---
# <a name="using-wdbgexts-extension-callbacks"></a>使用 WdbgExts 扩展回调


## <span id="ddk_using_wdbgexts_extension_callbacks_dbwx"></span><span id="DDK_USING_WDBGEXTS_EXTENSION_CALLBACKS_DBWX"></span>


在编写 WdbgExts 扩展 DLL 时，可以导出某些函数：

-   必须将导出一个名为函数[ *WinDbgExtensionDllInit*](https://msdn.microsoft.com/library/windows/hardware/ff561303)。 当调试器加载扩展 DLL 时，首先调用*WinDbgExtensionDllInit*并将其传递三个参数。

    -   一个指向**WINDBG\_扩展\_APIS64**结构，其中包含指向由调试器实现和 Wdbgexts.h 中声明的函数的指针。 必须将整个结构复制到在您的 DLL 中创建的全局变量。
    -   主版本号。 在您的 DLL 中创建的全局变量，必须将复制的主版本号。
    -   次版本号。 在您的 DLL 中创建的全局变量，必须将复制的次版本号。

    例如，可以创建名为 ExtensionApis、 SavedMajorVersion 和 SavedMinorVersion 如下面的示例中所示的全局变量。

    ```cpp
    WINDBG_EXTENSION_APIS64 ExtensionApis;
    USHORT SavedMajorVersion;
    USHORT SavedMinorVersion;

    VOID WinDbgExtensionDllInit(PWINDBG_EXTENSION_APIS64 lpExtensionApis,
        USHORT MajorVersion, USHORT MinorVersion)
    {
       ExtensionApis = *lpExtensionApis;
       SavedMajorVersion = MajorVersion;
       SavedMinorVersion = MinorVersion;
        ...
    }
    ```

-   必须将导出一个名为函数[ *ExtensionApiVersion*](https://msdn.microsoft.com/library/windows/hardware/ff543968)。 调试器将调用此函数，并要求返回一个指向**EXT\_API\_版本**结构，其中包含扩展 DLL 的版本号。 执行类似的命令时，调试器将使用此版本号[ **.chain** ](-chain--list-debugger-extensions-.md)并[**版本**](version--show-debugger-version-.md)显示扩展版本数。

-   （可选） 可以将导出一个名为函数[ *CheckVersion*](https://msdn.microsoft.com/library/windows/hardware/ff539096)。 每次使用扩展插件命令时，调试器将调用此例程。 可以使用此版本不匹配警告您的 DLL 是略有不同版本的调试器，但不同足够可阻止运行时打印。

 

 





