---
title: 处理文件指针
description: 处理文件指针
ms.assetid: 9bc03ae0-3e03-492a-b8d7-760eeb18106a
keywords:
- SymProxy，文件指针
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5830add47c784b98fb535c2c25db92e367856ebe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547765"
---
# <a name="handling-file-pointers"></a>处理文件指针


UNC 符号存储区支持放置在单独的位置，查找文件指针的文件的位置的客户端代码提供的实际文件。 在使用与 SymStore 符号存储区中生成这些指针 **/p**选项。 这种空格处理与其他基于 HTTP 的符号存储区的支持仅当文件指针指向可直接访问的 UNC 位置由客户端。 当 SymProxy 加载到 Web 服务器时，文件指针处理自动得到了增强。 客户端不再需要能够直接访问的目标文件，因为 SymProxy 提供它们通过 HTTP 接口。

由于此功能会自动应用，都有一个选项以将其关闭，如果必须使用代理服务器用于处理某些文件和其他人的常规文件指针实现。 若要执行此操作，创建 REG\_DWORD 中称为"NoFilePointerHandler" **HKLM\\软件\\Microsoft\\符号服务器**。 设置此值设置为 1 （或 0 之外的任何内容） 若要启用关闭 SymProxy 中的内部文件指针处理程序。

 

 





