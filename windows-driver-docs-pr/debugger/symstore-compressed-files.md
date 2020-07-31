---
title: SymStore 压缩文件
description: SymStore 压缩文件
ms.assetid: 4ec6a7f5-ceee-46d5-9a5e-36ab9fe9db52
keywords:
- SymStore，压缩文件
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6244d1b7a0fefcc4d0e0db4e42028504e540f4f5
ms.sourcegitcommit: 1d531bf9d02653fdf9ad728126d68b8acb86182e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/29/2020
ms.locfileid: "87402264"
---
# <a name="symstore-compressed-files"></a>SymStore 压缩文件

可以通过两种不同的方式将 SymStore 用于压缩的文件：

1. 使用带有 **/p**选项的 SymStore 存储指向符号文件的指针。 SymStore 完成后，压缩指针所指向的文件。

2. 使用带有 **/x**选项的 SymStore 创建索引文件。 SymStore 完成后，压缩索引文件中列出的文件。 然后，使用 SymStore 和 **/y**选项（如果需要，还可以使用 **/p**选项）将文件或指针存储到符号存储区中的文件。 （SymStore 不需要对文件进行解压缩即可执行此操作。）

符号服务器将负责在正确的时间解压缩文件。

如果使用 SymSrv 作为符号服务器，则应使用[Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?displaylang=en&id=17657)提供的 compress.exe 工具进行任何压缩。 压缩的文件应将一个下划线作为其文件扩展名中的最后一个字符（例如，module1 \_ 或 module2 \_ ）。 有关详细信息，请参阅[SymSrv](symsrv.md)。
