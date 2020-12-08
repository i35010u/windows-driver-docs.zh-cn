---
title: 编写 WdbgExts 扩展
description: 编写 WdbgExts 扩展
keywords:
- WdbgExts 扩展，编写
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f77727507fdb7e7937d1388ee21adcbe30cf967
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802743"
---
# <a name="writing-wdbgexts-extensions"></a>编写 WdbgExts 扩展


## <span id="ddk_writing_wdbgexts_extensions_dbwx"></span><span id="DDK_WRITING_WDBGEXTS_EXTENSIONS_DBWX"></span>


WdbgExts 扩展是原始类型的调试器扩展。 它们的功能不如 DbgEng 扩展，但在 Microsoft Windows 上执行用户模式或内核模式调试时，它们仍然提供各种功能。

如果已执行 Windows 调试工具的完全安装，则可以在 \\ 安装目录的 sdk 示例 simplext 子目录中找到一个名为 "simplext" 的示例 WdbgExts 扩展 \\ 。

本节包括：

[WdbgExts 扩展设计指南](wdbgexts-extension-design-guide.md)

[WdbgExts 扩展引用](/windows-hardware/drivers/ddi/wdbgexts/)

 

