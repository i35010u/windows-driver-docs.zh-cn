---
title: BCDEdit/bootsequence
description: Bootsequence 命令将启动管理器设置为要使用的一次性启动顺序。
ms.assetid: 74eb527c-78f3-41d0-bac6-f6fc200096a5
ms.date: 09/23/2020
keywords:
- BCDEdit/bootsequence 驱动程序开发工具
topic_type:
- apiref
api_name:
- BCDEdit /bootsequence
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 92d52abeaa43c017d973385d83e1a276c8953ff0
ms.sourcegitcommit: f2fbb6e54e085e9329288cee49860fe380be9c4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/06/2020
ms.locfileid: "91778993"
---
<a name="bcdedit-bootsequence"></a>BCDEdit/bootsequence
============

**/Bootsequence**命令将启动管理器设置为要使用的一次性启动顺序。

``` syntax
bcdedit /bootsequence <id> [...] [ /addfirst | /addlast | /remove ]
```

## <a name="parameters"></a>参数

**<id> [...]**

指定组成启动序列的数据存储标识符的列表。 必须至少指定一个标识符，并且必须用空格分隔标识符。 有关标识符的详细信息，请运行 "bcdedit/？ ID "。

**/addfirst**

将指定的条目标识符添加到启动序列的顶部。  如果指定此开关，则只能指定一个标识符。  如果标识符已经存在于列表中，则会将其移动到列表的顶部。

**/addlast**

将指定的条目标识符添加到启动序列的末尾。  如果指定此开关，则只能指定一个标识符。  如果标识符已经存在于列表中，则将其移动到列表的末尾。

/remove

从启动序列中移除指定的项标识符。  如果指定此开关，则只能指定一个条目标识符。  如果标识符不在列表中，则该操作不起作用。 如果删除最后一个条目，则会从启动管理器条目中删除启动序列值。

## <a name="examples"></a>示例

以下命令在启动管理器的 "一次性启动序列" 中设置两个 OS 项和基于 NTLDR 的 OS 加载程序：

`bcdedit /bootsequence {802d5e32-0784-11da-bd33-000476eba25f} {cbd971bf-b7b8-4885-951a-fa03044f5d71} {ntldr}`

以下命令将指定的 OS 条目添加到启动管理器的一次性启动序列的末尾：

`bcdedit /bootsequence {802d5e32-0784-11da-bd33-000476eba25f} /addlast`