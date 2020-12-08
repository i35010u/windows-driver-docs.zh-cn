---
title: 创建自己的源代码管理系统
description: 创建自己的源代码管理系统
keywords:
- 源服务器，HTTP 站点
- 源服务器，UNC 共享
- Srcsrv.ini，HTTP 站点
- Srcsrv.ini，UNC 共享
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab1856fb687d371dcbff81f52faca7f683549a56
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787815"
---
# <a name="creating-your-own-source-control-system"></a>创建自己的源代码管理系统


本部分可让你了解如何准备检测脚本，以便可以将 Srcsrv.ini 集成到你的生成或版本控制系统中。 实现依赖于随 Srcsrv.ini 附带的语言规范版本。

介绍如何通过符号处理程序代码调用 Srcsrv.dll 的一些细节。 但是，此信息并不是静态的，将来也不会成为。 任何人都不会尝试编写直接调用 Srcsrv.dll 的代码。 此为 Dbghelp.dll 或 Visual Studio 产品保留。 希望将此类功能集成到产品中的第三方供应商应该使用 **SymGetSourceFile** 函数。 Dbghelp.dll 文档中介绍了此函数以及 Dbghelp.dll API 中的其他功能，可以在 Windows 调试工具的 sdk/help 子目录中找到该功能。

本节包括：

[语言规范 1](language-specification-1.md)

[语言规范 2](language-specification-2.md)

 

 





