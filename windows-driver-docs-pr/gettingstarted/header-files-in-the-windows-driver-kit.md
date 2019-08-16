---
title: Windows 驱动程序工具包中的头文件
description: Windows 驱动程序工具包中的头文件
ms.assetid: 7d02148d-502d-4b49-9c56-9fff498dd2af
keywords:
- 驱动程序设计决策 WDK, 头文件更改
- 设计驱动程序 WDK, 头文件更改
- 头文件 WDK
- 头文件 WDK, 更改
- .h 文件
- 用户模式头文件 WDK
- 内核模式头文件 WDK
- 文件 WDK 头文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d517eb0cf67d274bbffd80403f7927400793a76
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371966"
---
# <a name="header-files-in-the-windows-driver-kit"></a>Windows 驱动程序工具包中的头文件


[Windows 驱动程序工具包 (WDK)](https://docs.microsoft.com/windows-hardware/drivers/) 包含构建内核模式和用户模式驱动程序所需的所有头文件（.h 文件）。 头文件位于 WDK 安装文件夹的 Include 文件夹中。 示例：C:\\Program Files (x86)\\Windows Kits\\10\\Include。

头文件包含版本信息，因此不论驱动程序在哪个版本的 Windows 上运行，你都可以使用一组相同的头文件。

## <a name="span-idconstants_that_represent_windows_versionsspanspan-idconstants_that_represent_windows_versionsspanspan-idconstants_that_represent_windows_versionsspanconstants-that-represent-windows-versions"></a><span id="Constants_that_represent_Windows_versions"></span><span id="constants_that_represent_windows_versions"></span><span id="CONSTANTS_THAT_REPRESENT_WINDOWS_VERSIONS"></span>表示 Windows 版本的常量


WDK 中的头文件包含的条件语句指定编程元素仅在某些版本的 Windows 操作系统中才可用。 进行版本管理的元素包括函数、枚举、结构以及结构成员。

若要指定编程元素在每个操作系统版本中都可用，头文件包含的预处理器条件会将 NTDDI\_VERSION 的值与 Sdkddkver.h 中定义的一组预定义常量值相比较。

以下是表示 Microsoft Windows 操作系统版本的预定义常量值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Constant</th>
<th align="left">操作系统版本</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>NTDDI_WIN10</p></td>
<td align="left"><p>Windows 10</p></td>
</tr>
<tr class="even">
<td align="left"><p>NTDDI_WINBLUE</p></td>
<td align="left"><p>Windows 8.1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NTDDI_WIN8</p></td>
<td align="left"><p>Windows 8</p></td>
</tr>
<tr class="even">
<td align="left"><p>NTDDI_WIN7</p></td>
<td align="left"><p>Windows 7</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NTDDI_WS08SP4</p></td>
<td align="left"><p>Windows Server 2008 SP4</p></td>
</tr>
<tr class="even">
<td align="left"><p>NTDDI_WS08SP3</p></td>
<td align="left"><p>Windows Server 2008 SP3</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NTDDI_WS08SP2</p></td>
<td align="left"><p>Windows Server 2008 SP2</p></td>
</tr>
<tr class="even">
<td align="left"><p>NTDDI_WS08</p></td>
<td align="left"><p>Windows Server 2008</p></td>
</tr>
</tbody>
</table>

 

你可以在 WDK 头文件中看到特定于版本的 DDI 元素的多个示例。 此条件声明出现在 Wdm.h 中，该文件为可能由内核模式驱动程序包含的头文件。

```cpp
#if (NTDDI_VERSION >= NTDDI_WIN7)
_Must_inspect_result_
NTKERNELAPI
NTSTATUS
KeSetTargetProcessorDpcEx (
    _Inout_ PKDPC Dpc,
    _In_ PPROCESSOR_NUMBER ProcNumber
    );
#endif
```

在该示例中，你可以看到仅在 Windows 7 和更高版本的 Windows 中才提供 [**KeSetTargetProcessorDpcEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesettargetprocessordpcex) 函数。

此条件声明出现在 Winspool.h 中，该文件为可能由用户模式驱动程序包含的头文件。

```ManagedCPlusPlus
#if (NTDDI_VERSION >= NTDDI_WIN7)
...
BOOL
WINAPI
GetPrintExecutionData(
    _Out_ PRINT_EXECUTION_DATA *pData
    );

#endif // (NTDDI_VERSION >= NTDDI_WIN7)
```

在该示例中，你可以看到仅在 Windows 7 和更高版本的 Windows 中才提供 [**GetPrintExecutionData**](https://docs.microsoft.com/windows/desktop/printdocs/getprintexecutiondata) 函数。

## <a name="span-idheader_files_for_the_kernel_mode_driver_frameworkspanspan-idheader_files_for_the_kernel_mode_driver_frameworkspanspan-idheader_files_for_the_kernel_mode_driver_frameworkspanheader-files-for-the-kernel-mode-driver-framework"></a><span id="Header_files_for_the_Kernel_Mode_Driver_Framework"></span><span id="header_files_for_the_kernel_mode_driver_framework"></span><span id="HEADER_FILES_FOR_THE_KERNEL_MODE_DRIVER_FRAMEWORK"></span>用于内核模式驱动程序框架的头文件


WDK 支持多种版本的 Windows，并且它还支持多种版本的内核模式驱动程序框架 (KMDF) 和用户模式驱动程序框架 (UMDF)。 WDK 头文件中的版本信息与 Windows 版本有关，但与 KMDF 或 UMDF 版本无关。 用于不同版本的 KMDF 和 UMDF 的头文件放置在不同的目录中。

 

 





