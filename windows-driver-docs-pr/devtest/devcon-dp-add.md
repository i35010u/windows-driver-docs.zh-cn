---
title: DevCon Dp_add
description: 将第三方 (OEM) 驱动程序包添加到本地计算机上的驱动程序存储区中。
keywords:
- DevCon Dp_add 驱动程序开发工具
topic_type:
- apiref
api_name:
- DevCon Dp_add
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ed7688f33e1621d12b8021860d5611353873308
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838143"
---
# <a name="devcon-dp_add"></a>DevCon Dp \_ add


将第三方 (OEM) 驱动程序包添加到本地计算机上的驱动程序存储区中。

```
    devcon dp_add inf
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______inf______"></span><span id="_______INF______"></span>*inf*   
驱动程序包的 INF 文件的完全限定路径和名称。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

DevCon dp \_ add 命令将指定的 INF 文件复制到% windir%/Inf 目录，并将其重命名为 "OEM \* .inf"。 此文件名在计算机上是唯一的，因此不能指定。

如果此 INF 文件已存在于% windir% (/Inf 中，则通过比较二进制文件（而不是通过匹配文件名称) 和 INF 的目录 () 文件）来确定，inf 文件不会重新复制到% windir%/Inf 目录。

此命令调用不带 *CopyStyle* 标志的 **SetupCopyOEMInf** 函数。 Microsoft Windows SDK 文档中介绍了 **SetupCopyOEMInf** 。

### <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon dp_add C:\WinDDK\5322\src\general\toaste
r\inf\i386\toaster.inf
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

[示例 45：添加和删除驱动程序包](example-45--add-and-remove-driver-packages.md)









