---
title: 审批 Sdv-map.h 文件
description: 审批 Sdv-map.h 文件
keywords:
- Sdv-map h-p 静态驱动程序验证程序，批准
- 批准 Sdv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86c2dbb688894f26660b4d71e41f376fc0e6278e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803971"
---
# <a name="approving-the-sdv-maph-file"></a>审批 Sdv-map.h 文件


Sdv 文件包含一行文本，通知 SDV 已批准该文件，可能是在检查文件并更正任何错误之后。 创建后，Sdv 文件将包含短语： "已批准 = false"。

### <a name="span-idto_approve_an_sdv_map_h_filespanspan-idto_approve_an_sdv_map_h_filespanto-approve-an-sdv-maph-file"></a><span id="to_approve_an_sdv_map_h_file"></span><span id="TO_APPROVE_AN_SDV_MAP_H_FILE"></span>批准 Sdv-map .h 文件

1.  在文本编辑器（例如记事本）中打开 Sdv 文件。 SDV 在驱动程序的源目录中创建 Sdv 文件。  (它是验证的本地目录。 ) 

2.  将 **//Approved = false** 更改为 **//Approved = true**。

### <a name="span-idwhen_you_should_approve_a_sdv_map_h_filespanspan-idwhen_you_should_approve_a_sdv_map_h_filespanwhen-you-should-approve-a-sdv-maph-file"></a><span id="when_you_should_approve_a_sdv_map_h_file"></span><span id="WHEN_YOU_SHOULD_APPROVE_A_SDV_MAP_H_FILE"></span>当你应该批准 Sdv 文件时

SDV 时，Sdv 正确且完整：

-   找到它使用的所有入口点。

-   已将入口点与正确的函数角色类型相关联。

### <a name="span-idwhen_you_should_correct_a_sdv_map_h_filespanspan-idwhen_you_should_correct_a_sdv_map_h_filespanwhen-you-should-correct-a-sdv-maph-file"></a><span id="when_you_should_correct_a_sdv_map_h_file"></span><span id="WHEN_YOU_SHOULD_CORRECT_A_SDV_MAP_H_FILE"></span>应更正 Sdv-map .h 文件

SDV 时，Sdv 文件不正确或不完整：

-   未检测到驱动程序中的任何入口点，通常是因为它找不到函数角色类型声明 (请参阅) [使用函数角色类型声明](using-function-role-type-declarations.md) 。

-   具有与函数角色类型相关联的重复回调函数。

-   具有的回调函数大于函数角色类型支持的最大值。

-   已检测到文件在被批准后，Sdv 文件中存在错误的或不存在的函数名称。

驱动程序无需具有 SDV 可以分析的每个入口点。 如果特定规则验证需要驱动程序入口点，而该驱动程序没有驱动程序，SDV 将取消对该规则的验证，并返回结果 " **不适用**"。 此结果不视为失败的结果。

除非 SDV 在驱动程序中找不到任何入口点，否则它将继续进行分析。 如果分析中使用的头文件不完整或不正确，则验证结果不可靠。

如果 SDV 检测到在文件被批准后，Sdv 文件中存在错误的或不存在的函数名称，则 SDV 将退出并发出一条警告消息，如以下示例所示：

```
Warning 'driver' It appears that your sdv-map.h file has an incorrect entry at this line "#define fun_IRP_MJ_PNP DispatchPnpNotExist". Please regenerate your sdv-map.h file.
```

若要修复此错误，请删除导致错误的 Sdv 文件中的行，或者重新生成该文件。

### <a name="span-idto_regenerate_the_sdv_map_h_filespanspan-idto_regenerate_the_sdv_map_h_filespanto-regenerate-the-sdv-maph-file"></a><span id="to_regenerate_the_sdv_map_h_file"></span><span id="TO_REGENERATE_THE_SDV_MAP_H_FILE"></span>重新生成 Sdv 文件

1.  打开 Sdv 文件，并将 **//Approved = true** 更改为 **//Approved = false**。

2.  使用 **staticdv/scan** 命令重新生成映射文件，或使用 **staticdv/rule** 或 **staticdv/config** 命令运行 SDV 分析。

 

 





