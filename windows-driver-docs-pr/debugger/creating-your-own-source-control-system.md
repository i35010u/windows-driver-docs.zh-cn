---
title: 创建源代码管理系统
description: 创建源代码管理系统
ms.assetid: 86492545-fc94-40ee-b22d-26fa2b0fbcc8
keywords:
- 源服务器、 HTTP 站点
- 源服务器、 UNC 共享
- SrcSrv，HTTP 站点
- SrcSrv，UNC 共享
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09c645663bc3fb568d10aa11932974d95817b144
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554939"
---
# <a name="creating-your-own-source-control-system"></a>创建源代码管理系统


本部分中，可了解如何准备检测脚本，以便 SrcSrv 可以集成到生成或版本控制系统。 实现是依赖于随 SrcSrv 的语言规范版本。

讨论了很多方式由符号处理程序代码调用 Srcsrv.dll 的具体情况。 但是，此信息不是静态的并且不会这样在将来。 没有人应尝试编写直接调用 Srcsrv.dll 的代码。 这被保留给 DbgHelp 或 Visual Studio 产品。 应使用第三方供应商想要将此类功能集成到他们的产品**SymGetSourceFile**函数。 此函数，以及其他 DbgHelp API 中所述的 DbgHelp 文档，可以找到有关 Windows 调试工具安装目录的 sdk/帮助子目录中。

本部分包括：

[语言规范 1](language-specification-1.md)

[语言规范 2](language-specification-2.md)

 

 





