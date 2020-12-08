---
title: 更改启动菜单超时
description: 更改启动菜单超时
keywords:
- Boot.ini 文件 WDK，菜单超时
- 启动选项 WDK，菜单超时
- 菜单超时 WDK 启动选项
- 超时 WDK 启动选项
- 启动菜单超时 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef44377641a15274e7e8e621524bc2f83cfe7760
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784075"
---
# <a name="changing-the-boot-menu-time-out"></a>更改启动菜单超时


## <span id="ddk_changing_the_boot_menu_time_out_tools"></span><span id="DDK_CHANGING_THE_BOOT_MENU_TIME_OUT_TOOLS"></span>


启动菜单超时确定加载默认启动条目之前启动菜单显示的时间。 它以秒为单位校准。

如果需要额外的时间来选择计算机上加载的操作系统，可以扩展超时值。 也可以缩短超时值，使默认操作系统的启动速度更快。

对于 Windows，你可以使用 BCDEdit 来更改默认启动菜单超时值。

### <a name="span-idusing_bcdeditspanspan-idusing_bcdeditspanusing-bcdedit"></a><span id="using_bcdedit"></span><span id="USING_BCDEDIT"></span>使用 BCDEdit

若要指定启动菜单超时值，请使用 **/timeout** 选项：

```
bcdedit /timeout <timeout>
```

使用 **/timeout** 选项并指定超时值（以秒为单位）。 例如，若要指定15秒的超时值：

```
bcdedit /timeout 15
```

 

 





