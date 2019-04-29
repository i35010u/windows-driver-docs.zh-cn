---
title: VirtualStorport 规则集 (Storport)
description: 使用这些规则来验证您的驱动程序正确调用 DDIs Storport 虚拟微型端口 (VMiniport) 驱动程序特定的感兴趣的。
ms.assetid: 7223AFF1-7EB7-4E25-BC50-8A7BF4E4BE59
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: f9c493b16ac25e242b7640741547f14a7df08049
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380476"
---
# <a name="virtualstorport-rule-set-storport"></a>VirtualStorport 规则集 (Storport)


使用这些规则来验证您的驱动程序正确调用 DDIs Storport 虚拟微型端口 (VMiniport) 驱动程序特定的感兴趣的。

## <a name="in-this-section"></a>本节内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="storport-doubleexfreepool.md" data-raw-source="[&lt;strong&gt;DoubleExFreePool&lt;/strong&gt;](storport-doubleexfreepool.md)"><strong>DoubleExFreePool</strong></a></p></td>
<td align="left"><p>此规则将验证该驱动程序不会尝试两次免费的相同池内存块。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-doublekesetevent.md" data-raw-source="[&lt;strong&gt;DoubleKeSetEvent&lt;/strong&gt;](storport-doublekesetevent.md)"><strong>DoubleKeSetEvent</strong></a></p></td>
<td align="left"><p>此规则验证<strong>KeSetEvent</strong>两次在同一个事件对象上不会对其进行调用。 如果同一事件对象传递给该例程，该驱动程序未能通过该规则。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-iofreeirp.md" data-raw-source="[&lt;strong&gt;IoFreeIrp&lt;/strong&gt;](storport-iofreeirp.md)"><strong>IoFreeIrp</strong></a></p></td>
<td align="left"><p>此规则验证的已分配的 IRP <strong>IoAllocateIrp</strong>或者将由释放<strong>IoFreeIrp</strong>或其完成例程将获取或设置<strong>IoSetCompletionRoutine</strong>.</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-storportvirtualdevice.md" data-raw-source="[&lt;strong&gt;StorPortVirtualDevice&lt;/strong&gt;](storport-storportvirtualdevice.md)"><strong>StorPortVirtualDevice</strong></a></p></td>
<td align="left"><p>此规则验证在从退出时<a href="https://msdn.microsoft.com/library/windows/hardware/ff557390" data-raw-source="[&lt;strong&gt;HwStorFindAdapter&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557390)"> <strong>HwStorFindAdapter</strong> </a>例程<strong>VirtualDevice</strong>字段中<a href="https://msdn.microsoft.com/library/windows/hardware/ff563901" data-raw-source="[&lt;strong&gt;PORT_CONFIGURATION_INFORMATION (Storport)&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563901)"> <strong>PORT_CONFIGURATION(Storport) _INFORMATION</strong> </a>结构具有设置为<strong>FALSE</strong>。 该规则仅适用于物理 StorPort 微型端口。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-storportvirtualdevice2.md" data-raw-source="[&lt;strong&gt;StorPortVirtualDevice2&lt;/strong&gt;](storport-storportvirtualdevice2.md)"><strong>StorPortVirtualDevice2</strong></a></p></td>
<td align="left"><p>此规则验证在从退出时<a href="https://msdn.microsoft.com/library/windows/hardware/ff557390" data-raw-source="[&lt;strong&gt;HwStorFindAdapter&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557390)"> <strong>HwStorFindAdapter</strong> </a>例程<strong>VirtualDevice</strong>字段中<a href="https://msdn.microsoft.com/library/windows/hardware/ff563901" data-raw-source="[&lt;strong&gt;PORT_CONFIGURATION_INFORMATION (Storport)&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563901)"> <strong>PORT_CONFIGURATION(Storport) _INFORMATION</strong> </a>结构具有设置为<strong>TRUE</strong>。 该规则仅适用于虚拟 StorPort 微型端口。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-withincriticalregion.md" data-raw-source="[&lt;strong&gt;WithinCriticalRegion&lt;/strong&gt;](storport-withincriticalregion.md)"><strong>WithinCriticalRegion</strong></a></p></td>
<td align="left"><p>此规则验证的某些同步函数的驱动程序的调用都仅在禁用普通内核 APC 传递时。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-zwregistrycreate.md" data-raw-source="[&lt;strong&gt;ZwRegistryCreate&lt;/strong&gt;](storport-zwregistrycreate.md)"><strong>ZwRegistryCreate</strong></a></p></td>
<td align="left"><p>此规则将验证与创建注册表项的句柄<a href="https://msdn.microsoft.com/library/windows/hardware/ff566425" data-raw-source="[&lt;strong&gt;ZwCreateKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566425)"> <strong>ZwCreateKey</strong> </a>随后将由正确其他<em>ZwXxx</em>例程。 <a href="https://msdn.microsoft.com/library/windows/hardware/ff567014" data-raw-source="[&lt;strong&gt;ZwOpenKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567014)"> <strong>ZwOpenKey</strong> </a>不得在已打开的句柄上调用例程。 例程<a href="https://msdn.microsoft.com/library/windows/hardware/ff566447" data-raw-source="[&lt;strong&gt;ZwEnumerateKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566447)"> <strong>ZwEnumerateKey</strong></a>， <a href="https://msdn.microsoft.com/library/windows/hardware/ff566453" data-raw-source="[&lt;strong&gt;ZwEnumerateValueKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566453)"> <strong>ZwEnumerateValueKey</strong></a>， <a href="https://msdn.microsoft.com/library/windows/hardware/ff566457" data-raw-source="[&lt;strong&gt;ZwFlushKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566457)"> <strong>ZwFlushKey</strong> </a>， <a href="https://msdn.microsoft.com/library/windows/hardware/ff567060" data-raw-source="[&lt;strong&gt;ZwQueryKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567060)"> <strong>ZwQueryKey</strong></a>， <a href="https://msdn.microsoft.com/library/windows/hardware/ff567069" data-raw-source="[&lt;strong&gt;ZwQueryValueKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567069)"> <strong>ZwQueryValueKey</strong></a>， <a href="https://msdn.microsoft.com/library/windows/hardware/ff567109" data-raw-source="[&lt;strong&gt;ZwSetValueKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567109)"> <strong>ZwSetValueKey</strong></a>， <a href="https://msdn.microsoft.com/library/windows/hardware/ff566417" data-raw-source="[&lt;strong&gt;ZwClose&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566417)"> <strong>ZwClose</strong></a>，以及<a href="https://msdn.microsoft.com/library/windows/hardware/ff566437" data-raw-source="[&lt;strong&gt;ZwDeleteKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566437)"> <strong>ZwDeleteKey</strong> </a>必须在不调用未打开的句柄。 此外必须在返回前关闭句柄。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-zwregistryopen.md" data-raw-source="[&lt;strong&gt;ZwRegistryOpen&lt;/strong&gt;](storport-zwregistryopen.md)"><strong>ZwRegistryOpen</strong></a></p></td>
<td align="left"><p>此规则验证通过打开的句柄的注册表项<strong>ZwOpenKey</strong>的随后使用由其他 ZwXxx 例程的正确无误。 例程<strong>ZwEnumerateKey</strong>， <strong>ZwEnumerateValueKey</strong>， <strong>ZwFlushKey</strong>， <strong>ZwQueryKey</strong>， <strong>ZwQueryValueKey</strong>， <strong>ZwSetValueKey</strong>， <strong>ZwClose</strong>，并且<strong>ZwDeleteKey</strong>不得在未打开的句柄上调用。 此外必须在返回前关闭句柄。</p></td>
</tr>
</tbody>
</table>

 

**若要选择 VirtualStorport 规则集**

1.  Microsoft Visual Studio 中选择您的驱动程序项目 (.vcxProj)。 从**驱动程序**菜单上，单击**启动 Static Driver Verifier...**.

2.  单击**规则**选项卡。下**规则集**，选择**VirtualStorport**。

    若要选择的默认规则集从 Visual Studio 开发人员命令提示符窗口，请指定**VirtualStorport.sdv**与 **/check**选项。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:VirtualStorport.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅[以找到缺陷驱动程序中使用 Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/hh454281)并[Static Driver Verifier 命令 (MSBuild)](https://msdn.microsoft.com/library/windows/hardware/hh466459)。

 

 





