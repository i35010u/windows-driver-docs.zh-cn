---
title: 更改启动菜单超时
description: 更改启动菜单超时
ms.assetid: 447fe656-4bb5-454e-bc89-bab58c8ffaea
keywords:
- Boot.ini 文件 WDK，菜单超时值
- 启动 WDK，菜单超时选项
- 菜单超时 WDK 启动选项
- 超时 WDK 启动选项
- 引导菜单超时 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba8c0ff7af8be4ae0f5161d9e026f8f030391ba0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375362"
---
# <a name="changing-the-boot-menu-time-out"></a>更改启动菜单超时


## <span id="ddk_changing_the_boot_menu_time_out_tools"></span><span id="DDK_CHANGING_THE_BOOT_MENU_TIME_OUT_TOOLS"></span>


引导菜单超时确定多长时间启动菜单显示之前加载的默认启动项目。 它被校准以秒为单位。

如果需要额外的时间来选择您的计算机加载的操作系统，您可以扩展的超时值。 或者，您可以缩短的超时值，以便更快地启动默认操作系统。

对于 Windows，可以使用 BCDEdit 更改默认引导菜单超时值。

### <a name="span-idusingbcdeditspanspan-idusingbcdeditspanusing-bcdedit"></a><span id="using_bcdedit"></span><span id="USING_BCDEDIT"></span>使用 BCDEdit

若要指定引导菜单超时值，请使用 **/timeout**选项：

```
bcdedit /timeout <timeout>
```

使用 **/timeout**选项，并以秒为单位指定超时值。 例如，若要指定 15 秒的超时值：

```
bcdedit /timeout 15
```

 

 





