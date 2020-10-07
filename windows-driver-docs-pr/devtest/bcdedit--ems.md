---
title: BCDEdit /ems
description: BCDEdit/ems 选项启用或禁用指定操作系统启动条目 (EMS) 的紧急管理服务。
ms.assetid: 28a28fa9-e359-4fd7-be4d-9b4129db8ac7
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
ms.openlocfilehash: 3cf3bdc86fc3a3db211f46b1d3a95460762d307e
ms.sourcegitcommit: f2fbb6e54e085e9329288cee49860fe380be9c4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/06/2020
ms.locfileid: "91778772"
---
<a name="bcdedit-ems"></a>BCDEdit /ems
============

**BCDEdit/ems**选项启用或禁用指定操作系统启动条目 (ems) 的紧急管理服务。

``` syntax
bcdedit /ems [{ID}] { on | off }
```

> [!NOTE]
> 设置 BCDEdit 选项之前，可能需要禁用或暂停计算机上的 BitLocker 和安全启动。

## <a name="parameters"></a>参数

 **{ID} **

{**ID**} 是与启动项关联的 GUID。 如果未指定 {**ID**}，则该命令将修改当前的操作系统启动项。 如果指定了启动目，则必须用大括号 { } 将与启动项关联的 GUID 括起来。

## <a name="comments"></a>注释

使用 [**BCDEdit/emssettings**](bcdedit--emssettings.md) 命令及其参数为所有启动条目建立 EMS 设置。 然后，使用 **BCDEdit/ems** 命令为特定启动条目启用 ems。

EMS 允许用户远程控制服务器的特定组件，即使在服务器未连接到网络或其他标准远程管理工具时也是如此。

## <a name="example"></a>示例

以下命令对标识符为 {49916baf-0e08-11db-9af4-000bdbd316a0} 的启动条目启用 EMS。

```console
bcdedit /ems {49916baf-0e08-11db-9af4-000bdbd316a0} on
```
