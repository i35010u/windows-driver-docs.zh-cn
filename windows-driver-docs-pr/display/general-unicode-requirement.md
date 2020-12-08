---
title: INF 文件中的常规 Unicode 要求
description: INF 文件应保存并编码为 Unicode;它们不得为 ANSI。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30b7dc841333b5b18adf6f8c4b7b66b354d3ffc6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803949"
---
# <a name="general-unicode-requirement-in-inf-files"></a>INF 文件中的常规 Unicode 要求


INF 文件应保存并编码为 Unicode (UTF-16) ;它们不能是 ANSI 或 UTF-8。

**检查 INF 文件中的 Unicode**

1.  使用 Microsoft Notepad 打开 INF 文件。
2.  在“文件”菜单中，单击“另存为”。
3.  如果在对话框的 "**编码**" 字段中显示 " **ANSI** "，请将编码更改为 **Unicode** ，并使用新名称保存该文件。

下图显示了具有 ANSI 编码的文件的 " **另存为** " 对话框：

![具有 ansi 编码的 "另存为" 对话框](images/saveasdialogansi.jpg)

此图显示了正确的默认值：

![具有 unicode 编码的 "另存为" 对话框](images/saveasdialogunicode.jpg)

 

 





