---
title: 复制 INF 文件
description: 复制 INF 文件
ms.assetid: 3ef92943-6462-4fe7-bd9b-8235083e8e16
keywords:
- INF 文件 WDK 设备安装复制
- 复制 INF 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51c64e22b166a4da7de7cd6dc969da2862725be3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542158"
---
# <a name="copying-inf-files"></a>复制 INF 文件





此外，有时需要在设备安装过程中复制 INF 文件，以便 Windows 可以找到它们而不会重复显示用户提示。 例如，多功能设备的基本 INF 文件可能会复制设备的各个函数的 INF 文件，以便 Windows 可以找到这些 INF 文件，而不提示用户安装设备的函数之一的每个时间。

若要复制 INF 文件，一个 INF 文件，可以使用[ **INF CopyINF 指令**](inf-copyinf-directive.md)。

执行操作，将：

-   如果存在，以及该 INF 文件，请安装相应的编录文件。

-   为 INF 文件指定唯一名称，以便它不会覆盖任何其他 INF 文件，并不会覆盖由其他 INF 文件。

-   保留从其设备文件要复制的源介质的路径。

-   请确保与 Windows 的未来版本的兼容性。

安装软件必须永远不会将 INF 文件复制到系统的直接 *%SystemRoot%/inf*目录。 通过使用未在本部分中介绍的技术复制 INF 文件将使驱动程序的数字签名无效。

 

 





