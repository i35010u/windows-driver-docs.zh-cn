---
title: 更改默认启动项
description: 更改默认启动项
ms.assetid: 0dce10d4-f73a-49bd-8a24-a4aa14c82233
keywords:
- 默认引导条目
- Boot.ini 文件 WDK，默认启动项
- 启动 WDK，默认启动项目选项
- 确定启动项
- 当前引导条目 WDK
- NVRAM 启动选项 WDK，默认启动项
- EFI NVRAM 启动选项 WDK，默认启动项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a5f6f5e29e977095c2b28f19feb08199c11a37a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344053"
---
# <a name="changing-the-default-boot-entry"></a>更改默认启动项


## <span id="ddk_changing_the_default_boot_entry_tools"></span><span id="DDK_CHANGING_THE_DEFAULT_BOOT_ENTRY_TOOLS"></span>


默认启动项目是启动加载程序时引导菜单超时时间已到选择的项。 您可以更改默认启动项目，以确保您喜欢的操作系统配置为自动加载。

对于 Windows，可以使用 BCDEdit 更改默认启动项目。

### <a name="span-idusingbcdeditspanspan-idusingbcdeditspanusing-bcdedit"></a><span id="using_bcdedit"></span><span id="USING_BCDEDIT"></span>使用 BCDEdit

您可以指定默认引导条目使用 **/默认**选项。 若要指定默认的操作系统的语法如下所示：

```
bcdedit /default <ID>
```

*&lt;ID&gt;* 是与你想要将指定为默认值的操作系统相关联的 Windows 启动加载程序启动项目的 GUID。 必须包括大括号 ( **{}** ) 周围的 GUID，例如：

```
bcdedit /default {cbd971bf-b7b8-4885-951a-fa03044f5d71}
```

若要将默认启动项目更改为多重引导计算机上早期 Windows 操作系统加载程序，设置 *&lt;ID&gt;* 到 **{ntldr}** ，这是 GUID 的保留的名称这是与 Ntldr 相关联。 这可能会根据 Boot.ini 文件中的条目的另一个菜单。

```
bcdedit /default {ntldr}
```

 

 





