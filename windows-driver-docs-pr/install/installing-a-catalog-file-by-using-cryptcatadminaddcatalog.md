---
title: 使用 CryptCATAdminAddCatalog 安装目录文件
description: 使用 CryptCATAdminAddCatalog 安装目录文件
ms.assetid: 2ab71f74-5a94-4f07-bd08-d3f5f6b6a785
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 446055e4774094b72d8c2f7fce96c5c324f444d9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325285"
---
# <a name="installing-a-catalog-file-by-using-cryptcatadminaddcatalog"></a>使用 CryptCATAdminAddCatalog 安装目录文件


安装程序可以使用[CryptCATAdminAddCatalog](https://go.microsoft.com/fwlink/p/?linkid=104926)和其他**CryptCATAdmin * Xxx*** 加密函数以编程方式安装[编录文件](catalog-files.md)在系统组件和驱动程序数据库。

安装程序必须适用于 Windows 7 和.NET Framework 4.0 中使用 Microsoft Windows 软件开发工具包 (SDK)，如下所示：

- 安装程序的源文件必须包含以下标头 (*.h*) 文件：
  - *Mscat.h*，用于定义原型和结构有关的各种**CryptCATAdmin * Xxx*** 函数。
  - *Softpub.h*，用于定义的各种数据结构和使用的 Guid **CryptCATAdmin * Xxx*** 函数。

- 安装程序必须链接到*Wintrust.lib*。

若要使用这些**CryptCATAdmin * Xxx*** 加密功能，安装程序执行以下操作：

1.  调用[CryptCATAdminAcquireContext](https://go.microsoft.com/fwlink/p/?linkid=105783)获取目录管理员上下文的句柄。 应用程序通过设置标识子系统*pgSubsystem*为指向 GUID DRIVER_ACTION_VERIFY 的输入的参数。 在中定义此 GUID *Softpub.h*。

2.  调用[CryptCATAdminAddCatalog](https://go.microsoft.com/fwlink/p/?linkid=136382)以添加[编录文件](catalog-files.md)到系统组件和驱动程序数据库。 安装程序提供在步骤 1、 目录文件的完全限定路径指向的指针和指向该函数使用要安装的目录 fi 副本的编录文件的名称中获得的目录管理员上下文的句柄在数据库中的 le。 该函数返回的句柄添加到数据库的编录文件的目录信息上下文。

3.  调用[CryptCATAdminReleaseCatalogContext](https://go.microsoft.com/fwlink/p/?linkid=105784)释放到编录文件的目录信息上下文的句柄。 安装程序提供在步骤 1 中获得的目录管理员上下文的句柄和在步骤 2 中返回目录信息上下文的句柄。

4.  调用[CryptCATAdminReleaseContext](https://go.microsoft.com/fwlink/p/?linkid=105785)发布目录管理员上下文的句柄。 应用程序提供在步骤 1 中获得的目录管理员上下文的句柄。









