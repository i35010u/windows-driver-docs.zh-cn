---
title: BCDEdit /ems
description: /Ems 选项启用或禁用紧急管理服务 (EMS) 为指定的操作系统启动项目。
ms.assetid: 28a28fa9-e359-4fd7-be4d-9b4129db8ac7
ms.date: 05/21/2018
keywords:
- BCDEdit /ems 驱动程序开发工具
topic_type:
- apiref
api_name:
- BCDEdit /ems
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5e405ee52ad1c34459f4099e894136454152459d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361261"
---
<a name="bcdedit-ems"></a>BCDEdit /ems
============

**/Ems**选项启用或禁用紧急管理服务 (EMS) 为指定的操作系统启动项目。

``` syntax
    bcdedit /ems [{ID}] { on | off } 

   
```

<a name="parameters"></a>Parameters
----------

<strong>{ID}</strong>   

{**ID**} 是与启动条目关联的 GUID。 如果未指定 {**ID**}，命令将修改当前操作系统启动项目。 如果指定的启动项，则与启动项关联的 GUID 必须括在大括号 {} 中。

### <a name="comments"></a>备注

在 Windows Vista 和更高版本，使用[ **BCDEdit /emssettings** ](bcdedit--emssettings.md)命令和其参数，用于为所有启动项的 EMS 设置。 然后，使用**BCDEdit /ems**命令来为特定启动项启用 EMS。

EMS 允许用户远程控制服务器的特定组件，即使服务器未连接到网络或其他标准的远程管理工具。 有关 EMS 的内容，紧急管理服务上搜索[Microsoft TechNet](https://go.microsoft.com/fwlink/p/?linkid=10111)网站。

### <a name="example"></a>示例

以下命令将启用替换 {49916baf-0e08-11db-9af4-000bdbd316a0} 的标识符的启动项的 EMS。

```
bcdedit /ems {49916baf-0e08-11db-9af4-000bdbd316a0} on
```

 

 





