---
title: 更改默认启动项
description: 更改默认启动项
keywords:
- 默认启动条目
- Boot.ini 文件 WDK、默认启动条目
- 启动选项 WDK，默认启动项
- 标识启动项
- 当前启动项 WDK
- NVRAM 启动选项 WDK，默认启动条目
- EFI NVRAM 启动选项 WDK，默认启动项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1906397cc832cf942aa98d774d72cd5fa5b6e500
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784067"
---
# <a name="changing-the-default-boot-entry"></a>更改默认启动项


## <span id="ddk_changing_the_default_boot_entry_tools"></span><span id="DDK_CHANGING_THE_DEFAULT_BOOT_ENTRY_TOOLS"></span>


默认启动项是启动加载程序在启动菜单超时过期时选择的项。 你可以更改默认启动项以确保自动加载你喜欢的操作系统配置。

对于 Windows，你可以使用 BCDEdit 来更改默认启动项。

### <a name="span-idusing_bcdeditspanspan-idusing_bcdeditspanusing-bcdedit"></a><span id="using_bcdedit"></span><span id="USING_BCDEDIT"></span>使用 BCDEdit

可以使用 **/默认 27000** 选项指定默认启动项。 指定默认操作系统的语法如下所示：

```
bcdedit /default <ID>
```

*&lt; ID &gt;* 是与要指定为默认操作系统的操作系统相关联的 Windows 启动加载程序启动项的 GUID。 必须围绕 GUID 包括大括号 (**{}**) ，例如：

```
bcdedit /default {cbd971bf-b7b8-4885-951a-fa03044f5d71}
```

若要将默认启动项目更改为多重引导计算机上早期的 Windows 操作系统加载程序，请将 *&lt; ID &gt;* 设置为 **{ntldr}**，这是与 ntldr 关联的 GUID 的保留名称。 根据 Boot.ini 文件中的条目，这可能会显示另一个菜单。

```
bcdedit /default {ntldr}
```

 

 





