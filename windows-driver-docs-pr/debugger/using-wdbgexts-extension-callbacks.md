---
title: 使用 WdbgExts 扩展回调
description: 使用 WdbgExts 扩展回调
ms.assetid: b9a2f30a-b09c-43eb-b105-a6b0ffdb1342
keywords:
- WdbgExts 扩展，回调，使用
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: c343ab0f7f84df8f0634de971d736d7e9b8a3b62
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206565"
---
# <a name="using-wdbgexts-extension-callbacks"></a>使用 WdbgExts 扩展回调


## <span id="ddk_using_wdbgexts_extension_callbacks_dbwx"></span><span id="DDK_USING_WDBGEXTS_EXTENSION_CALLBACKS_DBWX"></span>


编写 WdbgExts 扩展 DLL 时，可以导出某些函数：

-   必须导出名为 [*WinDbgExtensionDllInit*](/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_extension_dll_init)的函数。 调试器加载扩展 DLL 时，它首先调用 *WinDbgExtensionDllInit* 并将其传递给它三个参数。

    -   一个指向 **WINDBG \_ 扩展 \_ APIS64** 结构的指针，该结构包含指向由调试器实现并在 Wdbgexts 中声明的函数的指针。 必须将整个结构复制到在 DLL 中创建的全局变量。
    -   主要版本号。 必须将主版本号复制到在 DLL 中创建的全局变量。
    -   次版本号。 必须将次版本号复制到在 DLL 中创建的全局变量。

    例如，可以创建名为 ExtensionApis、SavedMajorVersion 和 SavedMinorVersion 的全局变量，如以下示例中所示。

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

-   必须导出名为 [*ExtensionApiVersion*](/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_extension_api_version)的函数。 调试器调用此函数并要求返回指向包含扩展 DLL 版本号的 **EXT \_ API \_ 版本** 结构的指针。 当执行的命令（如 [**链**](-chain--list-debugger-extensions-.md) 和 [**版本**](version--show-debugger-version-.md) ）显示扩展版本号时，调试器将使用此版本号。

-   可以选择导出名为 [*CheckVersion*](/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_check_version)的函数。 每次使用扩展命令时，调试器都会调用此例程。 如果 DLL 的版本与调试器的版本略有不同，则可以使用此方法输出版本不匹配警告，但不会有足够的时间来防止运行。

 

