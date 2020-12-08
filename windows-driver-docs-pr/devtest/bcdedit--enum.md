---
title: BCDEdit /enum
description: BCDEdit/enum 命令引导配置数据 (BCD) 存储中列出条目。
ms.date: 09/24/2020
keywords:
- BCDEdit/enum 驱动程序开发工具
topic_type:
- apiref
api_name:
- BCDEdit /enum
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b3dd27d5ab37cafb2ea687d38e30468fc203e3b2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803593"
---
<a name="bcdedit-enum"></a>BCDEdit /enum
============

**BCDEdit/enum** 命令引导配置数据 (BCD) 存储中列出条目。 /Enum 命令是默认值，因此，运行不带参数的 "bcdedit" 等效于运行 "bcdedit/enum ACTIVE"。

```syntax
bcdedit [/store <filename>] /enum [<type> | <id>] [/v]
```

> [!CAUTION]
>使用 BCDEdit 查看 BCD 存储需要管理权限。 使用 BCDEdit /set 命令更改某些启动项目选项可能导致计算机无法运行。 请改为使用系统配置实用程序 (MSConfig.exe) 更改启动设置。

## <a name="parameters"></a>参数

**\<filename\>**

指定要使用的存储区。 如果未指定此选项，则使用系统存储区。 有关详细信息，请运行 "bcdedit/？ store "。

**\<type\>**

指定要列出的条目类型。 <type> 可以是下列其中一项：

*主动* -启动管理器显示顺序中的所有条目。 这是默认值。

*固件* -所有固件应用程序。

*BOOTAPP* -所有启动环境应用程序。

*BOOTMGR* -启动管理器。

*OSLOADER* -所有操作系统条目。

*Resume* -从休眠项中恢复所有内容。

*Inherit* -All 继承项。

*所有* -所有条目。

**\<id\>**

指定要列出的项的标识符。  如果提供了标识符，则只会列出指定的对象。 有关标识符的详细信息，请运行 "bcdedit/？ ID "。

**/v**

显示完整的条目标识符，而不是使用众所周知标识符的名称。

## <a name="examples"></a>示例

以下命令列出所有操作系统加载程序启动条目。

`bcdedit /enum OSLOADER`

以下命令列出所有启动管理器条目。

`bcdedit /enum BOOTMGR`

以下命令仅列出默认启动项。

`bcdedit /enum {default}`

以下命令启用标识符为 {49916baf-0e08-11db-9af4-000bdbd316a0} 的启动项的 enum。

`bcdedit /enum {49916baf-0e08-11db-9af4-000bdbd316a0} on`
