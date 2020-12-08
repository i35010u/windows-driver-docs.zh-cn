---
title: DevCon Dp_enum
description: 列出本地计算机上驱动程序存储区中的第三方 (OEM) 驱动程序包。
keywords:
- DevCon Dp_enum 驱动程序开发工具
topic_type:
- apiref
api_name:
- DevCon Dp_enum
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 486c435025b293620e2b4b8e483bc2dfff4e41a8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798343"
---
# <a name="devcon-dp_enum"></a>DevCon Dp \_ 枚举


列出本地计算机上驱动程序存储区中的第三方 (OEM) 驱动程序包。

```
    devcon dp_enum
```

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

DevCon Dp \_ enum 命令列出了 \* 本地计算机上% windir%/Inf 中的 OEM .inf 文件。 对于每个文件，此命令将显示 INF 文件中的提供程序、类、日期和版本号。

### <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon dp_enum
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

[示例 45：添加和删除驱动程序包](example-45--add-and-remove-driver-packages.md)









