---
title: 确定操作系统是否在安全模式下运行
description: 确定操作系统是否在安全模式下运行
keywords:
- 安全模式 WDK 内核
- 操作系统安全模式 WDK 内核
- InitSafeBootMode
- 阻止安全模式 WDK 内核
- 正在检查安全模式
- 验证安全模式
- 启动安全模式 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b2719e6db1cca3619bcf6381e7cd27ee302608e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803829"
---
# <a name="determining-whether-the-operating-system-is-running-in-safe-mode"></a>确定操作系统是否在安全模式下运行


本主题描述了设备驱动程序如何确定运行它的操作系统是否在安全模式下启动。 本主题还介绍如何防止驱动程序在安全模式下运行。

Microsoft Windows 操作系统内核将导出名为 **InitSafeBootMode** 的指针。 **InitSafeBootMode** 指向包含当前有效的安全模式设置的 ULONG 变量。 设备驱动程序可以检查这些设置，以确定操作系统是否在安全模式下运行。

下表列出了 **InitSafeBootMode** 变量的值的模式。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>“值”</th>
<th>“模式”</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>操作系统不处于安全模式。</p></td>
</tr>
<tr class="even">
<td><p>1</p></td>
<td><p>SAFEBOOT_MINIMAL</p></td>
</tr>
<tr class="odd">
<td><p>2</p></td>
<td><p>SAFEBOOT_NETWORK</p></td>
</tr>
<tr class="even">
<td><p>3*</p></td>
<td><p>SAFEBOOT_DSREPAIR</p></td>
</tr>
</tbody>
</table>

 

**注意** \*值3仅适用于 Windows 域控制器。  

 

若要使用 **InitSafeBootMode** 变量，必须在您的驱动程序中声明它，如下面的代码示例所示。

```cpp
extern PULONG InitSafeBootMode;
```

声明 **InitSafeBootMode** 后，可以使用以下代码示例来确定操作系统是否在安全模式下运行。

```cpp
if (*InitSafeBootMode > 0) {
    // The operating system is in Safe Mode.
    // Take appropriate action.
    //
}
```

若要防止驱动程序在安全模式下操作，请使用与你的驱动程序类型匹配的以下列表中的方法：

-   **函数驱动程序**

    如果函数驱动程序的服务启动类型为 "服务 \_ 启动 \_ 启动"，请在函数驱动程序的 *AddDevice* 例程中检查 **InitSafeBootMode** 的值。 如果系统处于安全模式，则返回失败状态。

    **注意**   永远不能从 **DriverEntry** 例程返回失败。

     

-   **筛选器驱动程序**

    如果筛选器驱动程序在系统启动时启动，请在筛选器驱动程序的 *AddDevice* 例程中检查 **InitSafeBootMode** 的值。 如果操作系统处于安全模式，请执行以下操作：

    1.  不要将筛选器设备对象附加到设备堆栈。
    2.  从筛选器驱动程序的 *AddDevice* 例程返回 success。
-   **其他驱动程序**

    对于除函数或筛选器驱动程序以外的驱动程序，请在驱动程序的 **DriverEntry** 例程中检查 **InitSafeBootMode** 的值。 如果操作系统处于安全模式，则返回失败状态。

 

 




