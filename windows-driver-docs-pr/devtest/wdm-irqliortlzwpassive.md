---
title: 'IrqlIoRtlZwPassive 规则 (wdm) '
description: IrqlIoRtlZwPassive 规则指定，仅当该驱动程序以 IRQL = PASSIVE_LEVEL 执行时，才调用该规则中列出的 DDIs。
ms.assetid: 9BAE267F-CA57-4743-8C8D-08716C134E16
ms.date: 04/03/2020
keywords:
- 'IrqlIoRtlZwPassive 规则 (wdm) '
topic_type:
- apiref
api_name:
- IrqlIoRtlZwPassive
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2136f7b5cba04680866c82d8e8f649d986e6fe35
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104110"
---
# <a name="irqliortlzwpassive-rule-wdm"></a>IrqlIoRtlZwPassive 规则 (wdm) 

**IrqlIoRtlZwPassive**规则指定，仅当该驱动程序以 IRQL = PASSIVE_LEVEL 执行时，才调用该规则中列出的 DDIs。

此规则为 PASSIVE_LEVEL 扩充了 DDI 相容性检查 IRQL 规则。 有关详细信息，请参阅针对 [WDM)  (Irql 规则集 ](./irql-rule-set--wdm-.md)。

**驱动程序模型： WDM**

**Bug 检查 () 发现此规则**： [**bug 检查0XC4：驱动程序 \_ 验证器 \_ 检测到 \_ 违反**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) (0x20023) 


<a name="example"></a>示例
-------

以下代码违反了此规则：

```cpp
//
// KeAcquireSpinLock raises the IRQL to DISPATCH_LEVEL.
//

KeAcquireSpinLock (&Lock, &OldIrql);

//
// ERROR: IoGetDriverDirectory can only be called at IRQL == PASSIVE_LEVEL.
//

IoGetDriverDirectory (DriverObject,
                      DriverDirectoryData,
                      0,
                      &DirectoryHandle);

KeReleaseSpinLock (&Lock, OldIrql);
```

有关 IRQL 级别的详细信息，请参阅 [调度例程和 IRQLs](../kernel/dispatch-routines-and-irqls.md) 和 [管理硬件优先级](../kernel/managing-hardware-priorities.md)。

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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>IrqlIoRtlZwPassive</strong> 规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](./using-static-driver-verifier-to-find-defects-in-drivers.md#preparing-your-source-code)">准备你的代码 (使用) 的角色类型声明。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](./using-static-driver-verifier-to-find-defects-in-drivers.md#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](./using-static-driver-verifier-to-find-defects-in-drivers.md#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅 <a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](./using-static-driver-verifier-to-find-defects-in-drivers.md)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
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
<p>你可以使用 Verifier.exe 命令行为一个或多个驱动程序激活 DDI 符合性-其他 IRQL 规则。 有关详细信息，请参阅 <a href="/windows-hardware/drivers/devtest/selecting-driver-verifier-options" data-raw-source="[Selecting Driver Verifier Options](./ddi-compliance-checking.md)">选择驱动程序验证程序选项</a>。 你必须重新启动计算机以激活或停用 DDI 符合性-其他 IRQL 规则。</p>
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

  IoCreateFileEx

  IoCreateFileSpecifyDeviceObjectHint

  IoGetDeviceDirectory

  IoGetDriverDirectory

  IoOpenDeviceInterfaceRegistryKey

  IoOpenDeviceRegistryKey

  RtlCreateRegistryKey

  RtlCreateSystemVolumeInformationFolder

  RtlWriteRegistryValue

  ZwCreateDirectoryObject

  ZwCreateFile

  ZwCreateKeyTransacted

  ZwDeleteFile

  ZwDeleteValueKey

  ZwFlushBuffersFileEx
  
  ZwFlushBuffersFile
  
  ZwRenameKey

  ZwSetEaFile

  ZwSetInformationFile

  ZwSetInformationKey