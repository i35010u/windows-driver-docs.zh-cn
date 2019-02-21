---
title: 解压缩源代码文件
description: 解压缩源代码文件
ms.assetid: b7c859a9-5264-401c-ad96-ad044bcc140e
keywords:
- 解压缩源代码文件
- 提取源文件的源服务器
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: acd9accb0cec0ee66680071bbdd607f14ad9ee29
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525283"
---
# <a name="extracting-source-files"></a>解压缩源代码文件


若要从你想要提供源的所有模块中提取所有源代码文件，使用该命令：

```console
srctool.exe -x
```

此工具必须在执行上都已进行版本控制系统版本控制访问权限的计算机上创建源索引的.pdb 文件。 这会将所有源文件都放入常见的目录树中。 将此树的内容复制到网站的根目录。 您可以经常要在任何新产品或你想要添加的模块上执行此操作。 没有有关相互覆盖，因为目录的树状结构中保存不同文件分离且唯一可访问的文件无需担心。

### <a name="span-idwalkspanspan-idwalkspanwalk"></a><span id="walk"></span><span id="WALK"></span>遍历

审核 (Walk.cmd) 脚本包含在为 Windows 调试工具。 此脚本浏览目录树以递归方式搜索，并与指定的文件掩码匹配的任何文件上执行任何指定的命令。 此语法为：

```console
walk.cmd FileMask Command
```

其中*FileMask*指定一个文件掩码，具有或不附带的开始目录，并*命令*指定要执行的命令。

下面是示例 c： 驱动器中的所有.pdb 文件上运行 srctool.exe 文件提取命令\\符号和及其子目录：

```console
walk.cmd c:\symbols\*.pdb srctool.exe -x
```

 

 





