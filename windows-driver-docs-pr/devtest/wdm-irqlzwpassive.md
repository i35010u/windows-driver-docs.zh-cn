---
title: IrqlZwPassive 规则 (wdm)
description: IrqlZwPassive 规则指定驱动程序调用 ZwClose，仅当执行在 IRQL passive_level 调用时。
ms.assetid: d31612ad-e869-4fc7-bc09-e5b4d5362585
ms.date: 05/21/2018
keywords:
- IrqlZwPassive 规则 (wdm)
topic_type:
- apiref
api_name:
- IrqlZwPassive
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 37ebad03c0eafac5537d2c42652b54dcad512db2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331356"
---
# <a name="irqlzwpassive-rule-wdm"></a>IrqlZwPassive 规则 (wdm)


**IrqlZwPassive**规则指定驱动程序调用[ **ZwClose** ](https://msdn.microsoft.com/library/windows/hardware/ff566417)仅当执行在 IRQL = 被动\_级别。

|              |     |
|--------------|-----|
| 驱动程序模型 | WDM |

|                                   |                                                                                                                                    |
|-----------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x2001F) |

<a name="example"></a>示例
-------

下面的代码与此规则冲突：

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>IrqlZwPassive</strong>规则。</p>
使用以下步骤来分析你的代码：
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">准备你的代码 （使用角色类型声明）。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">运行的 Static Driver Verifier。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">查看和分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">以找到缺陷驱动程序中使用 Static Driver Verifier</a>。</p></td>
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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a> ，然后选择<a href="https://msdn.microsoft.com/library/windows/hardware/hh454208" data-raw-source="[DDI compliance checking](https://msdn.microsoft.com/library/windows/hardware/hh454208)">DDI 符合性检查</a>选项。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>适用对象
----------

[**ZwClose**](https://msdn.microsoft.com/library/windows/hardware/ff566417)
[**ZwCreateKey**](https://msdn.microsoft.com/library/windows/hardware/ff566425)
[**ZwDeleteKey** ](https://msdn.microsoft.com/library/windows/hardware/ff566437) 
[ **ZwEnumerateKey**](https://msdn.microsoft.com/library/windows/hardware/ff566447)
[**ZwEnumerateValueKey** ](https://msdn.microsoft.com/library/windows/hardware/ff566453) 
 [ **ZwFlushKey**](https://msdn.microsoft.com/library/windows/hardware/ff566457)
[**ZwOpenKey**](https://msdn.microsoft.com/library/windows/hardware/ff567014)
[**ZwQueryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff567060)
 [ **ZwQueryValueKey**](https://msdn.microsoft.com/library/windows/hardware/ff567069)
[**ZwSetValueKey**](https://msdn.microsoft.com/library/windows/hardware/ff567109)
 

 





