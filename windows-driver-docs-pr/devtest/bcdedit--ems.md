---
title: BCDEdit /ems
description: BCDEdit /ems 选项可启用或禁用指定的操作系统启动项目的紧急管理服务 (EMS)。
ms.date: 09/23/2020
keywords:
- BCDEdit/ems 驱动程序开发工具
topic_type:
- apiref
api_name:
- BCDEdit /ems
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5e1c0dfa603f612990f946b8b196e303b3c91e38
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822585"
---
<a name="bcdedit-ems"></a>BCDEdit /ems
============

**BCDEdit/ems** 选项启用或禁用指定操作系统启动条目 (ems) 的紧急管理服务。

``` syntax
bcdedit /ems [{ID}] { on | off }
```

> [!NOTE]
> 设置 BCDEdit 选项之前，可能需要禁用或暂停计算机上的 BitLocker 和安全启动。

## <a name="parameters"></a>参数

 **{ID}**

{**ID**} 是与启动项关联的 GUID。 如果未指定 {**ID**}，则该命令将修改当前的操作系统启动项。 如果指定了启动目，则必须用大括号 { } 将与启动项关联的 GUID 括起来。

## <a name="comments"></a>注释

使用 [**BCDEdit/emssettings**](bcdedit--emssettings.md) 命令及其参数为所有启动条目建立 EMS 设置。 然后，使用 **BCDEdit/ems** 命令为特定启动条目启用 ems。

EMS 允许用户远程控制服务器的特定组件，即使在服务器未连接到网络或其他标准远程管理工具时也是如此。

## <a name="example"></a>示例

以下命令对标识符为 {49916baf-0e08-11db-9af4-000bdbd316a0} 的启动条目启用 EMS。

```console
bcdedit /ems {49916baf-0e08-11db-9af4-000bdbd316a0} on
```
