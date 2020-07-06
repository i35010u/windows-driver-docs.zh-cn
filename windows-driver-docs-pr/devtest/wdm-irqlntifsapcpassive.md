---
title: IrqlNtifsApcPassive 规则（wdm）
description: IrqlNtifsApcPassive 规则指定，仅当该驱动程序以 IRQL = PASSIVE_LEVEL 或 IRQL <= APC_LEVEL 执行时，才调用该规则中列出的 DDIs。
ms.assetid: EDBF30AD-D122-4FF0-ACF9-8701E92B0A06
ms.date: 04/03/2020
keywords:
- IrqlNtifsApcPassive 规则（wdm）
topic_type:
- apiref
api_name:
- IrqlNtifsApcPassive
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: abeccdf83c014cabd11d6f8b657bb67795a053dc
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968548"
---
# <a name="irqlntifsapcpassive-rule-wdm"></a>IrqlNtifsApcPassive 规则（wdm）

**IrqlNtifsApcPassive**规则指定，仅当该驱动程序以 irql = PASSIVE_LEVEL 或 irql <= APC_LEVEL 执行时，才调用该规则中列出的 DDIs。

**驱动程序模型： WDM**

**找到了具有此规则的 bug 检查**： [**bug 检查0XC4：驱动程序 \_ 验证程序 \_ 检测到 \_ 冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)（0x20024）


<a name="example"></a>示例
-------

以下代码违反了此规则：

```cpp
//
// KeAcquireSpinLock raises the IRQL to DISPATCH_LEVEL.
//

KeAcquireSpinLock (&Lock, &OldIrql);

//
// ERROR: ZwWriteFile can only be called at IRQL == PASSIVE_LEVEL.
//

ZwWriteFile (Handle,
             NULL,
             NULL,
             NULL,
             IoStatusBlock,
             Buffer,
             BufferLength,
             NULL,
             NULL);

KeReleaseSpinLock (&Lock, OldIrql);
```

有关 IRQL 级别的详细信息，请参阅[调度例程和 IRQLs](https://docs.microsoft.com/windows-hardware/drivers/kernel/dispatch-routines-and-irqls)和[管理硬件优先级](https://docs.microsoft.com/windows-hardware/drivers/kernel/managing-hardware-priorities)。

<a name="how-to-test"></a>如何测试
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在编译时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>IrqlNtifsApcPassive</strong>规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">准备你的代码（使用角色类型声明）。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在运行时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">
<p>你可以使用 Verifier.exe 命令行为一个或多个驱动程序激活 DDI 符合性-其他 IRQL 规则。 有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/selecting-driver-verifier-options" data-raw-source="[Selecting Driver Verifier Options](https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking)">选择驱动程序验证程序选项</a>。 你必须重新启动计算机以激活或停用 DDI 符合性-其他 IRQL 规则。</p>
<p>在命令行中，DDI 符合性-额外的 IRQL 检查用规则类值35表示。 例如：</p>
<p><code>verifier /ruleclasses 35 /driver MyDriver.sys</code></p>
<p>OR</p>
<p><code>verifier /rc 35 /driver MyDriver.sys</code></p>
<p>重新启动计算机后，其他 IRQL 检查将处于活动状态。</p>
</td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

NtSetInformationFile

NtWriteFile

NtCreateFile

ZwWriteFile

CcCopyWrite

CcCopyWriteEx

CcDeferWrite

CcFastCopyWrite
