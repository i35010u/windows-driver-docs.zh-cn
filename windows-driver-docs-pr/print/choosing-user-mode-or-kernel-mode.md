---
title: 选择用户模式或内核模式
description: 选择用户模式或内核模式
ms.assetid: 1e63d01e-8cf2-488a-89e8-d4a3ff5cfe19
keywords:
- 打印机图形 DLL WDK，用户模式和内核模式对比
- 图形 DLL WDK 打印机，用户模式和内核模式对比
- 用户模式下执行 WDK 打印机图形
- 内核模式执行 WDK 打印机图形
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44b01cc556652bbb66876366047d447470b9ab91
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364923"
---
# <a name="choosing-user-mode-or-kernel-mode"></a>选择用户模式或内核模式





用户模式下执行的打印机图形 Dll 提供了对内核模式下执行以下优点：

-   不受限制的堆栈空间。

-   对 Win32 Api 的访问。

-   更低的可能导致系统崩溃。

-   方便调试，用于用户模式下调试程序。

-   更好地浮点功能，因为不需要使用 DDI 浮点函数的图形。

-   调用不是所述的 Microsoft Windows 2000 和更高版本的打印机驱动程序体系结构的一部分的任何自定义的供应商提供的用户模式 Dll 的能力

在 Windows Vista 中，不能安装内核模式打印机驱动程序。 如果应用程序尝试执行此操作，（Windows SDK 文档中所述） 的 AddPrinterDriver 和 AddprinterDriverEx 函数将失败，错误代码错误\_KM\_驱动程序\_已阻止。

下表显示允许的打印机驱动程序的执行模式：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>操作系统版本</th>
<th>允许使用的打印机图形 DLL 的执行模式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows NT 4.0</p></td>
<td><p>内核</p></td>
</tr>
<tr class="even">
<td><p>Windows 2000</p></td>
<td><p>用户或内核</p></td>
</tr>
<tr class="odd">
<td><p>Windows XP 和 Server 2003</p></td>
<td><p>内核模式可用于现有打印机;为新的打印机安装所需的用户模式</p></td>
</tr>
<tr class="even">
<td>Windows Vista</td>
<td><p>用户</p></td>
</tr>
</tbody>
</table>

 

### <a name="using-the-graphics-ddi-in-user-mode"></a>在用户模式下使用 DDI 的图形

用户模式打印机图形 DLL 并不局限于调用[GDI 支持服务](https://docs.microsoft.com/windows-hardware/drivers/display/gdi-support-services)和其他 Eng 前缀图形 DDI 回调函数。 但是，有一些必须遵循的规则：

-   如内核模式图形 Dll、 用户模式下的图形 Dll 必须调用图形 DDIs 创建或修改绘图图面。 这些回调函数是 GDI 支持服务，并且不允许调用这些绘图函数的 Win32 等效项。

    对于用户模式 Dll，对这些绘图的回调函数的调用都会被截获由用户模式下 GDI 客户端，然后将传递对 GDI 的内核模式图形呈现引擎 (GRE) 的调用。

-   不能由用户模式 Dll 调用以下 Eng 前缀图形 DDI 函数的列表：

    [**EngCreatePath**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatepath)

    [**EngGetType1FontList**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-enggettype1fontlist)

    [**EngMapModule**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engmapmodule)

    [**EngDebugBreak**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdebugbreak)

-   为函数的 Dll 可以继续使用 DDI 的图形的用户模式打印机图形[GDI 浮点服务](https://docs.microsoft.com/windows-hardware/drivers/display/gdi-floating-point-services)。

### <a name="converting-an-existing-printer-graphics-dll-to-user-mode"></a>将现有的打印机图形 DLL 转换为用户模式

如果您以前开发了打印机图形在内核模式下执行的 DLL，您可以将该 DLL 转换为用户模式下执行。 若要转换，只需添加[ **DrvQueryDriverInfo** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvquerydriverinfo)函数的 dll，然后按照规则[构建打印机图形 DLL](building-a-printer-graphics-dll.md)。

### <a name="creating-a-new-printer-graphics-dll-in-user-mode"></a>在用户模式下创建新的打印机图形 DLL

若要开发新的打印机图形在用户模式下执行的 DLL，您可以继续使用使用的内核模式的 Dll 的所有图形 DDI 函数。 但是，你还具有以下选项：

-   对于 Eng 前缀的函数具有确切 Win32 等效项，强烈建议您调用 Win32 函数。 下表列出了这些 Eng 前缀的函数，以及它们的 Win32 等效项。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Eng 前缀函数</th>
    <th>Win32 等效项</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>EngAllocMem</p></td>
    <td><p>HeapAlloc</p></td>
    </tr>
    <tr class="even">
    <td><p>EngAllocUserMem</p></td>
    <td><p>HeapAlloc</p></td>
    </tr>
    <tr class="odd">
    <td><p>EngEnumForms</p></td>
    <td><p>EnumForms</p></td>
    </tr>
    <tr class="even">
    <td><p>EngFreeMem</p></td>
    <td><p>HeapFree</p></td>
    </tr>
    <tr class="odd">
    <td><p>EngFreeUserMem</p></td>
    <td><p>HeapFree</p></td>
    </tr>
    <tr class="even">
    <td><p>EngFindImageProcAddress</p></td>
    <td><p>GetProcAddress</p></td>
    </tr>
    <tr class="odd">
    <td><p>EngGetForm</p></td>
    <td><p>GetForm</p></td>
    </tr>
    <tr class="even">
    <td><p>EngGetLastError</p></td>
    <td><p>GetLastError</p></td>
    </tr>
    <tr class="odd">
    <td><p>EngGetPrinter</p></td>
    <td><p>GetPrinter</p></td>
    </tr>
    <tr class="even">
    <td><p>EngGetPrinterData</p></td>
    <td><p>GetPrinterData</p></td>
    </tr>
    <tr class="odd">
    <td><p>EngGetPrinterDriver</p></td>
    <td><p>GetPrinterDriver</p></td>
    </tr>
    <tr class="even">
    <td><p>EngLoadImage</p></td>
    <td><p>LoadLibrary</p></td>
    </tr>
    <tr class="odd">
    <td><p>EngMulDiv</p></td>
    <td><p>MulDiv</p></td>
    </tr>
    <tr class="even">
    <td><p>EngSetLastError</p></td>
    <td><p>SetLastError</p></td>
    </tr>
    <tr class="odd">
    <td><p>EngSetPrinterData</p></td>
    <td><p>SetPrinterData</p></td>
    </tr>
    <tr class="even">
    <td><p>EngUnloadImage</p></td>
    <td><p>FreeLibrary</p></td>
    </tr>
    <tr class="odd">
    <td><p>EngWritePrinter</p></td>
    <td><p>WritePrinter</p></td>
    </tr>
    </tbody>
    </table>

     

<!-- -->

-   对于 Eng 前缀的函数使用类似的功能对应于 Win32 函数，也强烈建议您调用 Win32 函数。 下表列出了几种这些 Eng 前缀的函数，以及它们的 Win32 对应项。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Eng 前缀函数</th>
    <th>Win32 等效项</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>EngAcquireSemaphore</p></td>
    <td><p>EnterCriticalSection</p></td>
    </tr>
    <tr class="even">
    <td><p>EngCreateSemaphore</p></td>
    <td><p>分配 CRITICAL_SECTION 对象，并将其使用对 Win32 InitializeCriticalSection 函数的调用初始化。</p></td>
    </tr>
    <tr class="odd">
    <td><p>EngDeleteSemaphore</p></td>
    <td><p>DeleteCriticalSection</p></td>
    </tr>
    <tr class="even">
    <td><p>EngFindResource</p></td>
    <td><p>FindResource</p></td>
    </tr>
    <tr class="odd">
    <td><p>EngFreeModule</p></td>
    <td><p>FreeLibrary</p></td>
    </tr>
    <tr class="even">
    <td><p>EngLoadModule</p></td>
    <td><p>LoadLibrary</p></td>
    </tr>
    <tr class="odd">
    <td><p>EngMultiByteToWideChar</p></td>
    <td><p>MultiByteToWideChar</p></td>
    </tr>
    <tr class="even">
    <td><p>EngQueryLocalTime</p></td>
    <td><p>GetLocalTime</p></td>
    </tr>
    <tr class="odd">
    <td><p>EngReleaseSemaphore</p></td>
    <td><p>ReleaseSemaphore</p></td>
    </tr>
    <tr class="even">
    <td><p>EngWideCharToMultiByte</p></td>
    <td><p>WideCharToMultiByte</p></td>
    </tr>
    </tbody>
    </table>

     

<!-- -->

-   对于函数，创建或修改绘制的服务，新的驱动程序必须继续调用[GDI 支持服务](https://docs.microsoft.com/windows-hardware/drivers/display/gdi-support-services)不及其 Win32 等效项。

-   为 DDI 函数而不是使用图形[GDI 浮点服务](https://docs.microsoft.com/windows-hardware/drivers/display/gdi-floating-point-services)，可以使用 FLOAT 数据类型。

 

 




