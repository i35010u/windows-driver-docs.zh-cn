---
title: 选择用户模式或内核模式
description: 选择用户模式或内核模式
ms.assetid: 1e63d01e-8cf2-488a-89e8-d4a3ff5cfe19
keywords:
- 打印机图形 DLL WDK、用户模式与内核模式
- 图形 DLL WDK 打印机、用户模式与内核模式
- 用户模式执行 WDK 打印机图形
- 内核模式执行 WDK 打印机图形
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4d7905c56496ff8960e8df60f278769a6859763
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208431"
---
# <a name="choosing-user-mode-or-kernel-mode"></a>选择用户模式或内核模式





与内核模式执行相比，在用户模式下执行打印机图形 Dll 具有以下优势：

-   无限堆栈空间。

-   对 Win32 Api 的访问。

-   导致系统崩溃的可能性更小。

-   通过用户模式调试器更容易调试。

-   更好的浮点功能，因为不需要使用图形 DDI 浮点函数。

-   能够调用任何不属于所述 Microsoft Windows 2000 和更高版本的打印机驱动程序体系结构的自定义供应商提供的用户模式 Dll

在 Windows Vista 中，无法安装内核模式打印机驱动程序。 如果应用程序尝试执行此操作，则 Windows SDK) 文档中所述的 AddPrinterDriver 和 AddprinterDriverEx 函数 (将失败，并阻止错误代码错误 \_ KM \_ 驱动程序 \_ 。

下表显示了允许的打印机驱动程序执行模式：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>操作系统版本</th>
<th>允许的打印机图形 DLL 执行模式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows NT 4.0</p></td>
<td><p>内核 (kernel)</p></td>
</tr>
<tr class="even">
<td><p>Windows 2000</p></td>
<td><p>用户或内核</p></td>
</tr>
<tr class="odd">
<td><p>Windows XP 和服务器2003</p></td>
<td><p>适用于现有打印机的内核模式;新打印机安装所需的用户模式</p></td>
</tr>
<tr class="even">
<td>Windows Vista</td>
<td><p>user</p></td>
</tr>
</tbody>
</table>

 

### <a name="using-the-graphics-ddi-in-user-mode"></a>在用户模式下使用图形 DDI

用户模式打印机图形 DLL 并不局限于调用 [GDI 支持服务](../display/gdi-support-services.md) 和其他 Eng 的图形 DDI 回调函数。 但是，有一些必须遵循的规则：

-   与内核模式图形 Dll 一样，用户模式图形 Dll 必须调用图形 DDIs 来创建或修改绘图图面。 这些回调函数是 GDI 支持服务，不允许调用这些绘图函数的 Win32 等效项。

    对于用户模式 Dll，对这些绘图回调函数的调用会被用户模式 GDI 客户端截获，后者随后将调用传递到 GDI 的内核模式图形呈现引擎 (GRE) 。

-   用户模式 Dll 不能调用下面的 Eng 前缀图形 DDI 函数列表：

    [**EngCreatePath**](/windows/win32/api/winddi/nf-winddi-engcreatepath)

    [**EngGetType1FontList**](/windows/win32/api/winddi/nf-winddi-enggettype1fontlist)

    [**EngMapModule**](/windows/win32/api/winddi/nf-winddi-engmapmodule)

    [**EngDebugBreak**](/windows/win32/api/winddi/nf-winddi-engdebugbreak)

-   用户模式打印机图形 Dll 可以继续对 [GDI 浮点服务](../display/gdi-floating-point-services.md)使用图形 DDI 函数。

### <a name="converting-an-existing-printer-graphics-dll-to-user-mode"></a>将现有打印机图形 DLL 转换为用户模式

如果你之前开发了在内核模式下执行的打印机图形 DLL，则可以将该 DLL 转换为用户模式执行。 若要进行转换，只需将 [**DrvQueryDriverInfo**](/windows/win32/api/winddi/nf-winddi-drvquerydriverinfo) 函数添加到 DLL，然后按照 [生成打印机图形 DLL](building-a-printer-graphics-dll.md)的规则。

### <a name="creating-a-new-printer-graphics-dll-in-user-mode"></a>在用户模式下创建新的打印机图形 DLL

若要开发在用户模式下执行的新打印机图形 DLL，可以继续使用内核模式 Dll 使用的所有图形 DDI 函数。 但是，您还可以使用以下选项：

-   对于具有完全 Win32 等效项的 Eng 前缀函数，强烈建议调用 Win32 函数。 下表列出了这些 Eng 前缀的函数及其等效的 Win32 函数。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Eng-带前缀的函数</th>
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

-   对于与具有类似功能的 Win32 函数相对应的 Eng 前缀函数，还强烈建议调用 Win32 函数。 下表列出了其中几个 Eng 前缀的函数及其 Win32 对应项。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Eng-带前缀的函数</th>
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
    <td><p>分配 CRITICAL_SECTION 对象，并通过调用 Win32 InitializeCriticalSection 函数对其进行初始化。</p></td>
    </tr>
    <tr class="odd">
    <td><p>EngDeleteSemaphore</p></td>
    <td><p>DeleteCriticalSection</p></td>
    </tr>
    <tr class="even">
    <td><p>EngFindResource</p></td>
    <td><p>System.windows.frameworkelement.findresource</p></td>
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

-   对于创建或修改绘图服务的函数，新驱动程序必须继续调用 [GDI 支持服务](../display/gdi-support-services.md) ，而不是其 Win32 等效项。

-   您可以使用 FLOAT 数据类型，而不是对 [GDI 浮点服务](../display/gdi-floating-point-services.md)使用图形 DDI 函数。

 

