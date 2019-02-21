---
title: INF 文件中的常规 Unicode 要求
description: 应保存 INF 文件，并将其编码为 unicode 格式;它们不能 ANSI。
ms.assetid: 100F5DAB-FD25-4B42-8E3B-321E96CD25A2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aaaec5e465cf85eb2fc6e1a352d3bf3588f2d5a6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523204"
---
# <a name="general-unicode-requirement-in-inf-files"></a>INF 文件中的常规 Unicode 要求


应保存 INF 文件，并将其编码为 Unicode (utf-16);它们不能 ANSI 或 utf-8。

**若要检查的 INF 文件中的 Unicode**

1.  使用 Microsoft 记事本打开 INF 文件。
2.  在“文件”菜单上，单击“另存为”。
3.  如果**ANSI**将出现在**编码**字段的对话框框中，更改到编码**Unicode**并保存该文件以新名称。

此图显示了**另存为**具有 ANSI 编码的文件的对话框：

![将另存为包含 ansi 编码对话框](images/saveasdialogansi.jpg)

在此图中显示正确的默认值：

![另存为具有 unicode 编码的对话框](images/saveasdialogunicode.jpg)

 

 





