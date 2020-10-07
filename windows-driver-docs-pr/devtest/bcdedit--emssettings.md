---
title: BCDEdit /emssettings
description: /Emssettings 选项为计算机设置全局紧急管理服务 (EMS) 设置。 若要启用或禁用 EMS，请使用/ems 选项。 对于任何启动项，/emssettings 选项不会启用或禁用 EMS。
ms.assetid: 010e852d-ff97-4280-b35b-f1881e249e42
ms.date: 07/03/2018
keywords:
- BCDEdit/emssettings 驱动程序开发工具
topic_type:
- apiref
api_name:
- BCDEdit /emssettings
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 769e1114d4681226479f068183ce8401c4ab90b3
ms.sourcegitcommit: f2fbb6e54e085e9329288cee49860fe380be9c4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/06/2020
ms.locfileid: "91778769"
---
# <a name="bcdedit-emssettings"></a>BCDEdit /emssettings


**/Emssettings**选项为计算机设置全局紧急管理服务 (EMS) 设置。 若要启用或禁用 EMS，请使用 **/ems** 选项。 对于任何启动项， **/emssettings** 选项不会启用或禁用 EMS。

语法 

```
    bcdedit /emssettings [ BIOS ] | [ EMSPORT: port | [EMSBAUDRATE: baudrate] ] 
```

> [!NOTE]
> 设置 BCDEdit 选项之前，可能需要禁用或暂停计算机上的 BitLocker 和安全启动。

<a name="parameters"></a>参数
----------

**BIOS**   
指定系统将对 EMS 配置使用 BIOS 设置。 这仅适用于具有 BIOS 提供 EMS 支持的系统。

**EMSPORT：** *端口*   
指定要用作 EMS 端口的串行端口。 不应将此参数与 **BIOS** 选项一起指定。

**EMSBAUDRATE：** *波特率*   
指定用于 EMS 的串行波特率。 不应将此命令与 BIOS 一起指定。 *波特率*是可选的，默认值为 9600 bps。

### <a name="comments"></a>注释

若要在安装 Windows 后正确启用 EMS 控制台重定向，Windows 需要知道计算机用于带外通信的端口和传输速率。 Windows 将这些相同的设置用于 EMS 控制台重定向。

在带有 BIOS 固件和 ACPI 串行端口控制台重定向的计算机上 (SPCR) 表中，Windows 可以通过读取 SPCR 表中的条目来查找在 BIOS 中建立的带外设置。 在这些系统中，可以使用 **BIOS** 参数来指示 WINDOWS 在 SPCR 表中查找端口设置，也可以使用 **emsport：**<em>port</em> 和 **emsbaudrate：**<em>波特率</em> 参数覆盖 SPCR 表中的设置。

在具有 BIOS 固件但没有 SPCR 表的计算机上，使用 BCDEdit 和 **/emssettings** 命令和 **emsport：**<em>port</em> 参数指定端口，并使用 **emsbaudrate：**<em>波特率</em> 参数指定传输速率。

在所有系统上，使用 [**BCDEdit/ems**](bcdedit--ems.md) 命令并指定启动项，以在启动项加载的操作系统上启用 ems 控制台重定向。

此部分中所述的启动参数在安装 Windows 后启用 EMS 控制台重定向。 

有关详细示例，请参阅用于 [启用 EMS 重定向的启动参数](./boot-parameters-to-enable-ems-redirection.md)。

 

