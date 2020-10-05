---
title: 使用 CryptCATAdminAddCatalog 安装目录文件
description: 使用 CryptCATAdminAddCatalog 安装目录文件
ms.assetid: 2ab71f74-5a94-4f07-bd08-d3f5f6b6a785
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58e78ff2dda19f6cd22a3e6e7557b2adec3f317e
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91732857"
---
# <a name="installing-a-catalog-file-by-using-cryptcatadminaddcatalog"></a>使用 CryptCATAdminAddCatalog 安装目录文件


安装程序可以使用 [CryptCATAdminAddCatalog](/windows/win32/api/mscat/nf-mscat-cryptcatadminaddcatalog) 和其他 **CryptCATAdmin * Xxx*** 加密功能以编程方式在系统组件和驱动程序数据库中安装 [目录文件](catalog-files.md) 。

安装程序必须按以下方式使用适用于 Windows 7 的 Microsoft Windows 软件开发工具包 (SDK) 和 .NET Framework 4.0：

- 安装程序的源文件必须包括以下标头 (*.h*) 文件：
  - *Mscat*，它定义各种 **CryptCATAdmin * Xxx*** 函数的原型和结构。
  - *Softpub*，它定义 **CryptCATAdmin * Xxx*** 函数使用的各种数据结构和 guid。

- 安装程序必须链接到 *wintrust.dll*。

若要使用这些 **CryptCATAdmin * Xxx*** 密码功能，安装程序将执行以下操作：

1.  调用 [CryptCATAdminAcquireContext](/windows/win32/api/mscat/nf-mscat-cryptcatadminacquirecontext) 以获取目录管理员上下文的句柄。 应用程序通过将 *pgSubsystem* 输入参数设置为指向 GUID DRIVER_ACTION_VERIFY 的指针来标识子系统。 此 GUID 是在 *Softpub*中定义的。

2.  调用 [CryptCATAdminAddCatalog](/windows/win32/api/mscat/nf-mscat-cryptcatadminaddcatalog) 将 [目录文件](catalog-files.md) 添加到系统组件和驱动程序数据库。 安装程序提供了在步骤1中获得的目录管理员上下文的句柄、指向目录文件的完全限定路径的指针，以及指向该函数用于在数据库中安装目录文件副本的目录文件名称的指针。 函数为已添加到数据库的目录文件返回目录信息上下文的句柄。

3.  调用 [CryptCATAdminReleaseCatalogContext](/windows/win32/api/mscat/nf-mscat-cryptcatadminreleasecatalogcontext) 将句柄释放到目录信息上下文中的目录文件。 安装程序向在步骤1中获得的目录管理员上下文提供句柄，并向步骤2中返回的目录信息上下文提供句柄。

4.  调用 [CryptCATAdminReleaseContext](/windows/win32/api/mscat/nf-mscat-cryptcatadminreleasecontext) 以释放目录管理员上下文的句柄。 应用程序向在步骤1中获得的目录管理员上下文提供句柄。