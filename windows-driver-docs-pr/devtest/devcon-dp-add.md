---
title: DevCon Dp_add
description: 将第三方 (OEM) 驱动程序包添加到本地计算机上的驱动程序存储。
ms.assetid: 929bb59b-f227-47c5-9351-270ffbe4d745
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
ms.openlocfilehash: 46ec3c6cd36251e9f8de30964909f074e333558b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540865"
---
# <a name="devcon-dpadd"></a>DevCon Dp\_添加


将第三方 (OEM) 驱动程序包添加到本地计算机上的驱动程序存储。

```
    devcon dp_add inf
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______inf______"></span><span id="_______INF______"></span> *inf*   
完全限定的路径和驱动程序包的 INF 文件的名称。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

DevCon dp\_添加命令将指定的 INF 文件复制到 %windir%/Inf 目录，并将其重命名 OEM\*。 inf。 此文件的名称是唯一的计算机上并不能指定。

如果 %windir%/Inf （这是由不按匹配的文件名进行比较的二进制文件） 中已存在此 INF 文件和 INF 的目录 (.cat) 文件等同于目录中的目录文件，不再次 INF 文件复制到 %windir%/Inf目录。

此命令调用**SetupCopyOEMInf**函数没有*CopyStyle*标志。 **SetupCopyOEMInf** Microsoft Windows SDK 文档中所述。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon dp_add C:\WinDDK\5322\src\general\toaste
r\inf\i386\toaster.inf
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

[示例 45:添加和删除驱动程序包](example-45--add-and-remove-driver-packages.md)









