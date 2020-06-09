---
title: 调试 Windows Vista
description: 若要使用 WinDbg 调试 Windows Vista，请获取适用于 windows 7 的 windows 7 调试工具（包含在 Windows 7 中）。
ms.assetid: 1E4FC9D9-7F84-4F67-8FBC-4283C69AB0AC
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08c750e38a44e9623c8e34927e238aeb30bec36c
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534778"
---
# <a name="debugging-windows-vista"></a>调试 Windows Vista


若要使用 WinDbg 调试 Windows Vista，请获取适用于 windows 7[和 .NET Framework 4.0 的 Microsoft Windows 软件开发工具包（SDK）](https://www.microsoft.com/download/details.aspx?id=8279)中包含的 Windows 7 调试工具（适用于 windows）。

如果你只想下载适用于 Windows 的调试工具，请安装 SDK，然后在安装过程中，选择 "**适用于 Windows 的调试工具**" 框并清除所有其他框。

**注意**   安装 SDK 之前，可能必须卸载 Microsoft Visual C++ 2010 可再发行组件。 有关详细信息，请参阅[Microsoft 支持部门网站](https://support.microsoft.com/help/2717426/windows-sdk-fails-to-install-with-return-code-5100)。

 

## <a name="span-iddebugging_tools__windbg__kd__cdb__ntsd__for_windows_windows_vistaspandebugging-tools-windbg-kd-cdb-ntsd-for-windows-vista"></a><span id="DEBUGGING_TOOLS__WINDBG__KD__CDB__NTSD__FOR_WINDOWS_WINDOWS_VISTA"></span>适用于 Windows Vista 的调试工具（WinDbg、KD、CDB、NTSD）


适用于 Windows 的 Windows 7 调试工具可以在基于 x86 或基于 x64 的处理器上运行，并且它们可以调试在基于 x86 或基于 x64 的处理器上运行的代码。 有时候，调试程序和要调试的代码运行在同一计算机上，但另外一些时候，调试程序和要调试的代码则运行在不同的计算机上。 不管哪一种情况，运行调试程序的计算机称为“主计算机”**，被调试的计算机称为“目标计算机”**。 如果目标计算机运行的是以下操作系统之一，请使用 windows 7 调试工具。

|               |                     |
|---------------|---------------------|
| Windows Vista | Windows Server 2008 |
 

如果目标计算机运行的是更新版本的 Windows，请获取当前的[Windows 调试工具](index.md)。


 

 





