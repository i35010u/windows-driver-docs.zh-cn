---
title: 确定是否在安全模式下运行的操作系统
description: 确定是否在安全模式下运行的操作系统
ms.assetid: 5724a731-81a2-4c4e-a9e2-146859977e44
keywords:
- 安全模式 WDK 内核
- 操作系统安全模式 WDK 内核
- InitSafeBootMode
- 防止安全模式 WDK 内核
- 检查安全模式
- 验证安全模式
- 启动安全模式 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73420029be5b6649c4fd413888240137efbd167e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524759"
---
# <a name="determining-whether-the-operating-system-is-running-in-safe-mode"></a>确定是否在安全模式下运行的操作系统


本主题介绍如何将设备驱动程序可以确定运行的操作系统是否已在安全模式下启动。 本主题还介绍如何以阻止驱动程序在安全模式下操作。

Microsoft Windows 操作系统内核导出名为的指针**InitSafeBootMode**。 **InitSafeBootMode**指向 ULONG 变量包含当前正在起作用的安全模式设置。 设备驱动程序可以检查这些设置，以确定是否在安全模式下运行的操作系统。

下表列出的值的模式**InitSafeBootMode**变量。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>模式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>操作系统不是在安全模式下。</p></td>
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

 

**请注意**   \*值 3 适用于 Windows 域控制器。

 

若要使用**InitSafeBootMode**变量时，你必须将其声明中您的驱动程序，如以下代码示例所示。

```cpp
extern PULONG InitSafeBootMode;
```

声明后**InitSafeBootMode**，可以使用下面的代码示例以确定是否在安全模式下运行的操作系统。

```cpp
if (*InitSafeBootMode > 0) {
    // The operating system is in Safe Mode.
    // Take appropriate action.
    //
}
```

若要防止驱动程序在安全模式下运行，使用以下与匹配驱动程序类型的列表中的方法：

-   **功能的驱动程序**

    如果您函数的驱动程序具有启动类型的服务的服务\_引导\_开始，请检查的值**InitSafeBootMode**功能驱动程序中*AddDevice*例程。 如果系统在安全模式下，会返回失败状态。

    **请注意**  必须永远不会返回故障**DriverEntry**例程。

     

-   **筛选器驱动程序**

    如果在系统启动期间启动筛选器驱动程序，检查的值**InitSafeBootMode**筛选器驱动程序中*AddDevice*例程。 如果操作系统是在安全模式下，执行以下操作：

    1.  不要将筛选设备对象附加到设备堆栈。
    2.  从筛选器驱动程序返回成功*AddDevice*例程。
-   **其他驱动程序**

    函数或筛选器驱动程序以外的驱动程序，请检查的值**InitSafeBootMode**中的驱动程序**DriverEntry**例程。 如果操作系统是在安全模式下，会返回失败状态。

 

 




