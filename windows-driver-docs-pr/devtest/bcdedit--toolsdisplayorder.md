---
title: BCDEdit/toolsdisplayorder
description: BCDEdit/toolsdisplayorder 命令设置启动管理器在显示 "工具" 菜单时使用的显示顺序。
ms.assetid: a849ce02-c392-4982-9b93-7a1d70a77b9d
ms.date: 09/23/2020
keywords:
- BCDEdit/toolsdisplayorder 驱动程序开发工具
topic_type:
- apiref
api_name:
- BCDEdit /toolsdisplayorder
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d6c7720306d32217cba3e4f41f5707bc5129ddb4
ms.sourcegitcommit: f2fbb6e54e085e9329288cee49860fe380be9c4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/06/2020
ms.locfileid: "91778967"
---
<a name="bcdedit-toolsdisplayorder"></a>BCDEdit/toolsdisplayorder
============

**BCDEdit/toolsdisplayorder**命令设置启动管理器在显示 "工具" 菜单时使用的显示顺序。

```syntax
bcdedit /toolsdisplayorder <id> [...] [ /addfirst | /addlast | /remove ]
```

> [!NOTE]
> 设置 BCDEdit 选项之前，可能需要禁用或暂停计算机上的 BitLocker 和安全启动。

## <a name="parameters"></a>参数

**<id> [...]**

指定组成工具显示顺序的标识符列表。  至少必须指定一个标识符，并且必须用空格分隔。  有关标识符的详细信息，请运行 "bcdedit/？ ID "。

**/addfirst**

将指定的条目标识符添加到工具显示顺序的顶部。  如果指定此开关，则只能指定一个条目标识符。  如果指定的标识符已在列表中，则将其移动到列表的顶部。

**/addlast**

向工具显示顺序的末尾添加指定的项标识符。  如果指定此开关，则只能指定一个条目标识符。  如果指定的标识符已在列表中，则将其移动到列表的末尾。

/remove

从工具显示顺序中删除指定的条目标识符。  如果指定此开关，则只能指定一个条目标识符。  如果该标识符不在列表中，则该操作将不起作用。  如果删除最后一个条目，则会从启动管理器条目中删除工具显示顺序值。

## <a name="examples"></a>示例

以下命令在启动管理器的工具显示顺序中设置两个工具项和内存诊断：

`bcdedit /toolsdisplayorder {802d5e32-0784-11da-bd33-000476eba25f} {cbd971bf-b7b8-4885-951a-fa03044f5d71} {memdiag}`

以下命令将指定的工具项添加到启动管理器的工具显示顺序的末尾：

`bcdedit /toolsdisplayorder {802d5e32-0784-11da-bd33-000476eba25f} /addlast`
