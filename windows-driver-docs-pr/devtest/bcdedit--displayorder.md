---
title: BCDEdit/displayorder
description: Displayorder 命令将设置启动管理器使用的显示顺序。
ms.assetid: 6e2fcde1-f2f8-434d-80d5-d74f32831bfe
ms.date: 09/23/2020
keywords:
- BCDEdit/displayorder 驱动程序开发工具
topic_type:
- apiref
api_name:
- BCDEdit /displayorder
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fbe747ce32b9e7232b28d6f2df2871d66196a6b4
ms.sourcegitcommit: f2fbb6e54e085e9329288cee49860fe380be9c4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/06/2020
ms.locfileid: "91778974"
---
<a name="bcdedit-displayorder"></a>BCDEdit/displayorder
============

**/Displayorder**命令将设置启动管理器使用的显示顺序。

``` syntax
bcdedit /displayorder <id> [...] [ /addfirst | /addlast | /remove ]
```

> [!NOTE]
> 设置 BCDEdit 选项之前，可能需要禁用或暂停计算机上的 BitLocker 和安全启动。

## <a name="parameters"></a>参数

**\<id\> [...]**  指定组成显示顺序的标识符列表。  至少必须指定一个标识符，并且必须用空格分隔。  有关标识符的详细信息，请运行 "bcdedit/？ ID "。

**/addfirst**   将指定的条目标识符添加到显示顺序的顶部。  如果指定此开关，则只能指定一个条目标识符。  如果指定的标识符已在列表中，则会将其移动到列表的顶部。

**/addlastAdds** 指定的条目标识符到显示顺序的结尾。  如果指定此开关，则只能指定一个条目标识符。  如果指定的标识符已在列表中，则将其移动到列表的末尾。

/remove

从显示顺序中删除指定的条目标识符。  如果指定此开关，则只能指定一个条目标识符。  如果标识符不在列表中，则该操作不起作用。 如果删除最后一个条目，则将从启动管理器条目中删除显示顺序值。

## <a name="examples"></a>示例

以下命令在启动管理器显示顺序中设置两个 OS 项和基于 NTLDR 的 OS 加载程序：

`bcdedit /displayorder {802d5e32-0784-11da-bd33-000476eba25f} {cbd971bf-b7b8-4885-951a-fa03044f5d71} {ntldr}`

以下命令将指定的 OS 条目添加到启动管理器显示顺序的末尾：

`bcdedit /displayorder {802d5e32-0784-11da-bd33-000476eba25f} /addlast`
