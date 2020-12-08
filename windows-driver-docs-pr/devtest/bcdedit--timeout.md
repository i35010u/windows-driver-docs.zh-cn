---
title: BCDEdit /timeout
description: '**BCDEdit/timeout** 命令在启动管理器选择默认条目之前设置等待时间（以秒为单位）。'
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
ms.openlocfilehash: a18dfe40fb1c5c2564600fac0db2dddbae410081
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786913"
---
<a name="bcdedit-timeout"></a>BCDEdit /timeout
============

**BCDEdit/timeout** 命令在启动管理器选择默认条目之前设置等待时间（以秒为单位）。 有关设置默认条目的信息，请运行 "bcdedit/？ 默认值 "。

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
