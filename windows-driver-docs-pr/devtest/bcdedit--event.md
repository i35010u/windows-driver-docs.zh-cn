---
title: BCDEdit /event
description: /Event 命令启用或禁用指定启动项的远程事件日志记录。
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
ms.openlocfilehash: 1131c1526b8d02b69f69852c248f770521e5c80b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803591"
---
<a name="bcdedit-event"></a>BCDEdit /event
============

**/Event** 启用或禁用指定启动项的远程事件日志记录。

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
