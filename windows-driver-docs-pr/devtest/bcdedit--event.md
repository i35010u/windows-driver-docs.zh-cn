---
title: BCDEdit/event
description: /Event 命令启用或禁用指定启动项的远程事件日志记录。
ms.assetid: 7bb5ad1b-d2fa-4697-b518-9aed0cbeacce
ms.date: 09/23/2020
keywords:
- BCDEdit/event 驱动程序开发工具
topic_type:
- apiref
api_name:
- BCDEdit /event
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: edfe07007159bbf09b17517c485a9d9125b98b80
ms.sourcegitcommit: f2fbb6e54e085e9329288cee49860fe380be9c4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/06/2020
ms.locfileid: "91778966"
---
<a name="bcdedit-event"></a>BCDEdit/event
============

**/Event**启用或禁用指定启动项的远程事件日志记录。

``` syntax
bcdedit /event [{ID}] { on | off }
```

> [!NOTE]
> 设置 BCDEdit 选项之前，可能需要禁用或暂停计算机上的 BitLocker 和安全启动。

## <a name="parameters"></a>参数

 <strong>{ID} </strong>

{**ID**} 指定要修改的项的标识符。  仅可指定 Windows 启动加载程序项。  如果未指定，则使用 {current}。 有关标识符的详细信息，请运行 "bcdedit/？ ID "。

## <a name="example"></a>示例

以下命令启用当前 Windows 操作系统启动条目的远程事件日志记录。

``` syntax
bcdedit /event ON
```

以下命令将为指定的操作系统条目禁用远程事件日志记录：

```syntax
bcdedit /event {cbd971bf-b7b8-4885-951a-fa03044f5d71} OFF
```