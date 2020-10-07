---
title: BCDEdit/timeout
description: '**BCDEdit/timeout**命令在启动管理器选择默认条目之前设置等待时间（以秒为单位）。'
ms.assetid: d8f238ae-fb0f-4c62-b149-0e066bfa4d5f
ms.date: 09/23/2020
keywords:
- BCDEdit/timeout 驱动程序开发工具
topic_type:
- apiref
api_name:
- BCDEdit /timeout
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: beb53eb705861dd5bd58f015ca9ddc0eb3669ae2
ms.sourcegitcommit: f2fbb6e54e085e9329288cee49860fe380be9c4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/06/2020
ms.locfileid: "91778965"
---
<a name="bcdedit-timeout"></a>BCDEdit/timeout
============

**BCDEdit/timeout**命令在启动管理器选择默认条目之前设置等待时间（以秒为单位）。 有关设置默认条目的信息，请运行 "bcdedit/？ 默认值 "。

``` syntax
bcdedit /timeout <timeout>
```

> [!NOTE]
> 设置 BCDEdit 选项之前，可能需要禁用或暂停计算机上的 BitLocker 和安全启动。

## <a name="parameters"></a>参数

**\<timeout\>***秒*

指定在启动管理器选择默认条目之前等待的时间（秒）。

## <a name="examples"></a>示例

以下命令将启动管理器设置 <timeout> 为30秒：

`bcdedit /timeout 30`
