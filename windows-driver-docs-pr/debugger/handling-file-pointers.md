---
title: 处理文件指针
description: 处理文件指针
keywords:
- SymProxy，文件指针
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c13ec36c0613da8bf266def6841dfc161c1f09a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839945"
---
# <a name="handling-file-pointers"></a>处理文件指针


UNC 符号存储区支持将实际文件放在单独的位置，并且客户端代码通过文件指针查找文件的位置。 使用带有 **/p** 选项的 SymStore 在符号存储区中生成这些指针。 仅当文件指针指向客户端直接可访问的 UNC 位置时，其他基于 HTTP 的符号存储区支持此处理。 将 SymProxy 加载到 Web 服务器时，文件指针处理会自动增强。 客户端不再需要能够直接访问目标文件，因为 SymProxy 通过 HTTP 接口为其提供服务。

由于此功能是自动应用的，因此，如果您必须使用代理来为其他文件提供一些文件和常规文件指针实现，则可以使用一个选项来关闭此功能。 为此，请 \_ 在 **HKLM \\ Software \\ Microsoft \\ 符号服务器** 中创建名为 "NoFilePointerHandler" 的注册表 DWORD。 将此值设置为 1 (或0以外的任何值，) 关闭 SymProxy 中的内部文件指针处理程序。

 

 





