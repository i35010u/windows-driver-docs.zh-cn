---
title: SetupAPI 使用指南
description: SetupAPI 使用指南
keywords:
- Setupapi.log 函数 WDK，指导原则
- 设备安装功能 WDK Setupapi.log
- 常规设置函数 WDK Setupapi.log
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4c7e33e217ae8b65b3a26b8d795f0b23e3b6b20
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791453"
---
# <a name="guidelines-for-using-setupapi"></a>SetupAPI 使用指南





以下准则介绍了如何使用 [常规安装程序功能](/previous-versions/ff544985(v=vs.85)) (**安装**_xxx_) 和 [设备安装功能](/previous-versions/ff541299(v=vs.85)) (由 setupapi.log 提供的 **SetupDi**_xxx_) ：

-   永远不会假定安装文件的内容是错误的，或者你提供的安装文件未被恶意修改。 因此，请始终验证从 Setupapi.log 函数接收到的所有信息。 验证字符串的长度是否有效，缓冲区的大小是否有效，以及索引值是否在有效范围内。

-   在 Microsoft Windows XP 和更高版本的系统上编写安装应用程序进行安装时，可以调用 Windows SDK 文档) 中所述的 **SetupVerifyInfFile** (，这将验证是否未修改经过数字签名的 INF 文件。

-   始终测试每个 Setupapi.log 函数的返回值。 如果函数失败，你的代码应调用 [GetLastError](/windows/win32/api/errhandlingapi/nf-errhandlingapi-getlasterror) 以获取用于标识失败的错误代码。 返回的错误代码可在 *winerror.h* 或 *setupapi.log* 中定义。 **在使用 FORMAT_MESSAGE_FROM_SYSTEM** 创建文本显示之前，请始终使用 *winerror.h*) 中定义的 HRESULT_FROM_SETUPAPI 宏 (将返回值转换为 HRESULT 值。 如果 Setupapi.log 函数成功返回，则代码不得调用 [GetLastError](/windows/win32/api/errhandlingapi/nf-errhandlingapi-getlasterror)。 Windows SDK 文档中介绍了 ([GetLastError](/windows/win32/api/errhandlingapi/nf-errhandlingapi-getlasterror) 和 **FormatMessage** 函数以及系统错误代码。 ) 

-   如果 Setupapi.log 函数返回句柄，你的代码必须检查的返回值是否为 INVALID_HANDLE_VALUE。 此类函数不返回 **NULL**。

-   请注意 **SetupDi**_xxx_ 和 **设置**_xxx_ 函数之间的以下差异，它们允许调用方查询所需的缓冲区大小：

    -   如果 **SetupDi**_Xxx_ 函数的调用方执行此类查询，则 [GetLastError](/windows/win32/api/errhandlingapi/nf-errhandlingapi-getlasterror) 始终返回 ERROR_INSUFFICIENT_BUFFER。

    -   如果 **设置**_Xxx_ 函数的调用方执行此类查询，则在未指定缓冲区长度的情况下， [GetLastError](/windows/win32/api/errhandlingapi/nf-errhandlingapi-getlasterror) 返回 NO_ERROR; 如果指定的缓冲区太小，则为 ERROR_INSUFFICIENT_BUFFER。

