---
title: IrqlZwPassive 规则（wdm）
description: IrqlZwPassive 规则指定仅当驱动程序在 IRQL PASSIVE_LEVEL 执行时才调用 ZwClose。
ms.assetid: d31612ad-e869-4fc7-bc09-e5b4d5362585
ms.date: 05/21/2018
keywords:
- IrqlZwPassive 规则（wdm）
topic_type:
- apiref
api_name:
- IrqlZwPassive
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 02b039e9cd1c8a73408e044fa601344453b35a40
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917060"
---
# <a name="irqlzwpassive-rule-wdm"></a>IrqlZwPassive 规则（wdm）


**IrqlZwPassive**规则指定仅当驱动程序在 IRQL = 被动级别执行时才调用[**ZwClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose) \_ 。

**驱动程序模型： WDM**

|                                   |                                                                                                                                    |
|-----------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| 找到了具有此规则的 Bug 检查 | [**Bug 检查0xC4：驱动程序 \_\_检测到 \_ 验证程序冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)（0x2001F） |

<a name="example"></a>示例
-------

以下代码违反了此规则：

``` syntax
NTSTATUS 
DriverCloseResources (
    _In_ PDRIVER_CONTEXT Context
    )
{
    …

    NT_ASSERT(KeGetCurrentIrql() == PASSIVE_LEVEL);

    //
    // ExAcquireFastMutex sets the IRQL to APC_LEVEL, and the caller continues 
    // to run at APC_LEVEL after ExAcquireFastMutex returns.
    //
  
    ExAcquireFastMutex(&Context->FastMutex);
    
    ....
    
    if (NULL != Context->Handle) {

            //
            // RULE VIOLATION! - ZwClose can be called only at PASSIVE_LEVEL 
            //
            
            ZwClose(Context->Handle);      
            Context->Handle = NULL;
    }
    
    ....

    //
    // N.B. ExReleaseFastMutex restores the original IRQL.
    //
     
    ExReleaseFastMutex(&Context->FastMutex);
    
    ....
}
```

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>IrqlZwPassive</strong>规则。</p>
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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">驱动程序验证程序</a>，并选择 " <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking" data-raw-source="[DDI compliance checking](https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking)">DDI 相容性检查</a>" 选项。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>适用于
----------

[**ZwClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose) 
[**ZwCreateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatekey) 
[**ZwDeleteKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwdeletekey) 
[**ZwEnumerateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwenumeratekey) 
[**ZwEnumerateValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwenumeratevaluekey) 
[**ZwFlushKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwflushkey) 
[**ZwOpenKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopenkey) 
[**ZwQueryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwquerykey) 
[**ZwQueryValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwqueryvaluekey) 
[**ZwSetValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwsetvaluekey)
 

 





