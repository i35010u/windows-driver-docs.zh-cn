---
title: VirtualStorport 规则集 (Storport)
description: 使用这些规则验证你的驱动程序是否正确地调用 (VMiniport) 驱动程序的 Storport 虚拟小型端口。
ms.assetid: 7223AFF1-7EB7-4E25-BC50-8A7BF4E4BE59
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5e0fb9adcfaa5a5158aec367c08af25240fd332f
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89381757"
---
# <a name="virtualstorport-rule-set-storport"></a>VirtualStorport 规则集 (Storport)


使用这些规则验证你的驱动程序是否正确地调用 (VMiniport) 驱动程序的 Storport 虚拟小型端口。

## <a name="in-this-section"></a>在本节中


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="storport-doubleexfreepool.md" data-raw-source="[&lt;strong&gt;DoubleExFreePool&lt;/strong&gt;](storport-doubleexfreepool.md)"><strong>DoubleExFreePool</strong></a></p></td>
<td align="left"><p>此规则验证驱动程序是否不会尝试释放相同的池内存块。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-doublekesetevent.md" data-raw-source="[&lt;strong&gt;DoubleKeSetEvent&lt;/strong&gt;](storport-doublekesetevent.md)"><strong>DoubleKeSetEvent</strong></a></p></td>
<td align="left"><p>此规则验证是否未在同一事件对象上两次调用 <strong>KeSetEvent</strong> 。 如果将相同的事件对象传递到例程，则驱动程序将无法满足规则。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-iofreeirp.md" data-raw-source="[&lt;strong&gt;IoFreeIrp&lt;/strong&gt;](storport-iofreeirp.md)"><strong>IoFreeIrp</strong></a></p></td>
<td align="left"><p>此规则验证 <strong>IoAllocateIrp</strong> 分配的 IRP 是否将由 <strong>IoFreeIrp</strong> 或其完成例程进行释放，以由 <strong>IoSetCompletionRoutine</strong>设置。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-storportvirtualdevice.md" data-raw-source="[&lt;strong&gt;StorPortVirtualDevice&lt;/strong&gt;](storport-storportvirtualdevice.md)"><strong>StorPortVirtualDevice</strong></a></p></td>
<td align="left"><p>此规则验证是否在退出<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter" data-raw-source="[&lt;strong&gt;HwStorFindAdapter&lt;/strong&gt;](/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter)"><strong>HwStorFindAdapter</strong></a>例程时， <a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff563901(v=vs.85)" data-raw-source="[&lt;strong&gt;PORT_CONFIGURATION_INFORMATION (Storport)&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff563901(v=vs.85))"><strong>PORT_CONFIGURATION_INFORMATION (Storport) </strong></a>结构中的 " <strong>VirtualDevice</strong> " 字段已设置为 " <strong>FALSE</strong>"。 此规则仅适用于物理 StorPort 微型端口。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-storportvirtualdevice2.md" data-raw-source="[&lt;strong&gt;StorPortVirtualDevice2&lt;/strong&gt;](storport-storportvirtualdevice2.md)"><strong>StorPortVirtualDevice2</strong></a></p></td>
<td align="left"><p>此规则验证是否在退出<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter" data-raw-source="[&lt;strong&gt;HwStorFindAdapter&lt;/strong&gt;](/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter)"><strong>HwStorFindAdapter</strong></a>例程时， <a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff563901(v=vs.85)" data-raw-source="[&lt;strong&gt;PORT_CONFIGURATION_INFORMATION (Storport)&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff563901(v=vs.85))"><strong>PORT_CONFIGURATION_INFORMATION (Storport) </strong></a>结构中的 " <strong>VirtualDevice</strong> " 字段已设置为 " <strong>TRUE</strong>"。 此规则仅适用于虚拟 StorPort 微型端口。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-withincriticalregion.md" data-raw-source="[&lt;strong&gt;WithinCriticalRegion&lt;/strong&gt;](storport-withincriticalregion.md)"><strong>WithinCriticalRegion</strong></a></p></td>
<td align="left"><p>此规则验证是否只有在禁用正常内核 APC 传递时才对驱动程序的某些同步函数进行调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-zwregistrycreate.md" data-raw-source="[&lt;strong&gt;ZwRegistryCreate&lt;/strong&gt;](storport-zwregistrycreate.md)"><strong>ZwRegistryCreate</strong></a></p></td>
<td align="left"><p>此规则验证使用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatekey" data-raw-source="[&lt;strong&gt;ZwCreateKey&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatekey)"><strong>ZwCreateKey</strong></a> 创建的注册表项的句柄以后是否可以由其他 <em>ZwXxx</em> 例程正确使用。 不能对已打开的句柄调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopenkey" data-raw-source="[&lt;strong&gt;ZwOpenKey&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopenkey)"><strong>ZwOpenKey</strong></a> 例程。 不能在未打开的句柄上调用例程 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwenumeratekey" data-raw-source="[&lt;strong&gt;ZwEnumerateKey&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwenumeratekey)"><strong>ZwEnumerateKey</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwenumeratevaluekey" data-raw-source="[&lt;strong&gt;ZwEnumerateValueKey&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwenumeratevaluekey)"><strong>ZwEnumerateValueKey</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwflushkey" data-raw-source="[&lt;strong&gt;ZwFlushKey&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwflushkey)"><strong>ZwFlushKey</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwquerykey" data-raw-source="[&lt;strong&gt;ZwQueryKey&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwquerykey)"><strong>ZwQueryKey</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwqueryvaluekey" data-raw-source="[&lt;strong&gt;ZwQueryValueKey&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwqueryvaluekey)"><strong>ZwQueryValueKey</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwsetvaluekey" data-raw-source="[&lt;strong&gt;ZwSetValueKey&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwsetvaluekey)"><strong>ZwSetValueKey</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose" data-raw-source="[&lt;strong&gt;ZwClose&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)"><strong>ZwClose</strong></a>和 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwdeletekey" data-raw-source="[&lt;strong&gt;ZwDeleteKey&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwdeletekey)"><strong>ZwDeleteKey</strong></a> 。 还必须在返回前关闭句柄。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-zwregistryopen.md" data-raw-source="[&lt;strong&gt;ZwRegistryOpen&lt;/strong&gt;](storport-zwregistryopen.md)"><strong>ZwRegistryOpen</strong></a></p></td>
<td align="left"><p>此规则验证通过 <strong>ZwOpenKey</strong> 打开的注册表项的句柄以后是否可以由其他 ZwXxx 例程正确使用。 不能在未打开的句柄上调用例程 <strong>ZwEnumerateKey</strong>、 <strong>ZwEnumerateValueKey</strong>、 <strong>ZwFlushKey</strong>、 <strong>ZwQueryKey</strong>、 <strong>ZwQueryValueKey</strong>、 <strong>ZwSetValueKey</strong>、 <strong>ZwClose</strong>和 <strong>ZwDeleteKey</strong> 。 还必须在返回前关闭句柄。</p></td>
</tr>
</tbody>
</table>

 

**选择 VirtualStorport 规则集**

1.  选择你的驱动程序项目 () 在 Microsoft Visual Studio 中。 在 " **驱动程序** " 菜单中，单击 " **启动静态驱动程序验证程序 ...**"。

2.  单击 " **规则** " 选项卡。在 " **规则集**" 下，选择 **VirtualStorport**。

    若要从 Visual Studio 开发人员命令提示符窗口中选择默认规则集，请使用 **/check**选项指定**VirtualStorport。 sdv** 。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:VirtualStorport.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅 [使用静态驱动程序验证器查找驱动程序中的缺陷](./using-static-driver-verifier-to-find-defects-in-drivers.md) 和 [静态驱动程序验证程序命令 (MSBuild) ](./-static-driver-verifier-commands--msbuild-.md)。

 

