---
title: BCDEdit /ems
description: /Ems 选项启用或禁用指定操作系统启动项的紧急管理服务（EMS）。
ms.assetid: 28a28fa9-e359-4fd7-be4d-9b4129db8ac7
ms.date: 05/21/2018
keywords:
- BCDEdit/ems 驱动程序开发工具
topic_type:
- apiref
api_name:
- BCDEdit /ems
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6adc1e2cb94f1e2911f4c0df376459f9ec9c096a
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209489"
---
<a name="bcdedit-ems"></a>BCDEdit /ems
============

**/Ems**选项启用或禁用指定操作系统启动项的紧急管理服务（ems）。

``` syntax
    bcdedit /ems [{ID}] { on | off } 

   
```

<a name="parameters"></a>参数
----------

<strong>识别</strong>   

{**ID**} 是与启动项关联的 GUID。 如果未指定 {**ID**}，则该命令将修改当前的操作系统启动项。 如果指定了启动项，则与启动项关联的 GUID 必须括在大括号 {} 中。

### <a name="comments"></a>备注

使用[**BCDEdit/emssettings**](bcdedit--emssettings.md)命令及其参数为所有启动条目建立 EMS 设置。 然后，使用**BCDEdit/ems**命令为特定启动条目启用 ems。

EMS 允许用户远程控制服务器的特定组件，即使在服务器未连接到网络或其他标准远程管理工具时也是如此。 

### <a name="example"></a>示例

以下命令对标识符为 {49916baf-0e08-11db-9af4-000bdbd316a0} 的启动条目启用 EMS。

```
bcdedit /ems {49916baf-0e08-11db-9af4-000bdbd316a0} on
```

 

 





