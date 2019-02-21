---
title: BCDEdit /emssettings
description: /Emssettings 选项设置为计算机的全局紧急管理服务 (EMS) 设置。 若要启用或禁用 EMS，请使用 /ems 选项。 /Emssettings 选项不启用或禁用的任何启动项的 EMS。
ms.assetid: 010e852d-ff97-4280-b35b-f1881e249e42
ms.date: 07/03/2018
keywords:
- BCDEdit /emssettings 驱动程序开发工具
topic_type:
- apiref
api_name:
- BCDEdit /emssettings
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 18757cc3041b8e5673218516f4368a083892f502
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523254"
---
# <a name="bcdedit-emssettings"></a>BCDEdit /emssettings


**/Emssettings**选项设置为计算机的全局紧急管理服务 (EMS) 设置。 若要启用或禁用 EMS，请使用 **/ems**选项。 **/Emssettings**选项不会启用或禁用的任何启动项的 EMS。

语法 

```
    bcdedit /emssettings [ BIOS ] | [ EMSPORT: port | [EMSBAUDRATE: baudrate] ] 
```

<a name="parameters"></a>参数
----------

**BIOS**   
指定系统将为 EMS 配置中使用 BIOS 设置。 这仅适用于具有提供的 BIOS 的 EMS 支持的系统。

 **EMSPORT:** *端口*   
指定要作为 EMS 端口使用的串行端口。 此参数不应指定与**BIOS**选项。

**EMSBAUDRATE:** *baudrate*   
指定要用于 EMS 的串行波特率。 此命令不应指定通过 BIOS。 *Baudrate*是可选的默认值为 9600 bps。

### <a name="comments"></a>备注

若要正确启用 EMS 控制台重定向，安装 Windows 后，Windows 需要知道计算机使用的带外通信的端口和传输速率。 Windows 使用这些相同的设置的 EMS 控制台重定向。

在使用 BIOS 固件和 ACPI 串行端口控制台重定向 (SPCR) 表的计算机，Windows 可以找到通过读取 SPCR 表中的条目来建立在 BIOS 中的带外设置。 在这些系统中，您可以使用**BIOS**参数指示 Windows 在端口设置，或者你 SPCR 表中进行查找可以使用**emsport:**<em>端口</em>和**emsbaudrate:**<em>baudrate</em>参数来替代 SPCR 表中的设置。

计算机上具有 BIOS 固件，但不是具有 SPCR 表，使用 BCDEdit 并 **/emssettings**命令**emsport:**<em>端口</em>参数来指定的端口和与**emsbaudrate:**<em>baudrate</em>参数指定的传输速率。

在所有系统上使用[ **BCDEdit /ems** ](bcdedit--ems.md)命令并指定要启用 EMS 控制台重定向的启动项目加载的操作系统上的启动项。

安装 Windows 之后，在本部分中所述的启动参数启用 EMS 控制台重定向。 有关全新安装或升级 Windows 过程中启用 EMS，"启用紧急管理服务"上搜索[Microsoft TechNet](https://go.microsoft.com/fwlink/p/?linkid=10111)网站。

有关详细示例，请参阅[启用 EMS 重定向的启动参数](https://msdn.microsoft.com/library/windows/hardware/ff542282)。

 

 





