---
title: 其他规则集 (WDM)
description: 使用这些规则来验证您的驱动程序正确地遵循一组常规的要求正确处理的注册表项、 字符串和设备对象指针。
ms.assetid: 50E8BFFE-AC38-4023-9FFB-DC53B749A603
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0cb9e0f4a10983552c1cc75fb58caf91687e37c3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361286"
---
# <a name="miscellaneous-rule-set-wdm"></a>其他规则集 (WDM)


使用这些规则来验证您的驱动程序正确地遵循一组常规的要求正确处理的注册表项、 字符串和设备对象指针。

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
<td align="left"><p><a href="wdm-adddevice.md" data-raw-source="[&lt;strong&gt;AddDevice&lt;/strong&gt;](wdm-adddevice.md)"><strong>AddDevice</strong></a></p></td>
<td align="left"><p><a href="wdm-adddevice.md" data-raw-source="[&lt;strong&gt;AddDevice&lt;/strong&gt;](wdm-adddevice.md)"> <strong>AddDevice</strong> </a>规则指定的驱动程序<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device" data-raw-source="[&lt;strong&gt;AddDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)"> <strong>AddDevice</strong> </a>例程调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioattachdevicetodevicestack" data-raw-source="[&lt;strong&gt;IoAttachDeviceToDeviceStack&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioattachdevicetodevicestack)"> <strong>IoAttachDeviceToDeviceStack</strong> </a>仅在调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice" data-raw-source="[&lt;strong&gt;IoCreateDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice)"> <strong>IoCreateDevice</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-danglingdeviceobjectreference.md" data-raw-source="[&lt;strong&gt;DanglingDeviceObjectReference&lt;/strong&gt;](wdm-danglingdeviceobjectreference.md)"><strong>DanglingDeviceObjectReference</strong></a></p></td>
<td align="left"><p><a href="wdm-danglingdeviceobjectreference.md" data-raw-source="[&lt;strong&gt;DanglingDeviceObjectReference&lt;/strong&gt;](wdm-danglingdeviceobjectreference.md)"> <strong>DanglingDeviceObjectReference</strong> </a>规则指定驱动程序调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obdereferenceobject" data-raw-source="[&lt;strong&gt;ObDereferenceObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obdereferenceobject)"> <strong>ObDereferenceObject</strong> </a>与同一设备对象指针， <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iogetattacheddevicereference" data-raw-source="[&lt;strong&gt;IoGetAttachedDeviceReference&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iogetattacheddevicereference)"> <strong>IoGetAttachedDeviceReference</strong> </a>返回。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-pnpsamedeviceobject.md" data-raw-source="[&lt;strong&gt;PnpSameDeviceObject&lt;/strong&gt;](wdm-pnpsamedeviceobject.md)"><strong>PnpSameDeviceObject</strong></a></p></td>
<td align="left"><p><a href="wdm-pnpsamedeviceobject.md" data-raw-source="[&lt;strong&gt;PnpSameDeviceObject&lt;/strong&gt;](wdm-pnpsamedeviceobject.md)"> <strong>PnpSameDeviceObject</strong> </a>规则指定驱动程序调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioattachdevicetodevicestack" data-raw-source="[&lt;strong&gt;IoAttachDeviceToDeviceStack&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioattachdevicetodevicestack)"> <strong>IoAttachDeviceToDeviceStack</strong> </a>用一个指针指向一个有效目标设备对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-targetrelationneedsref.md" data-raw-source="[&lt;strong&gt;TargetRelationNeedsRef&lt;/strong&gt;](wdm-targetrelationneedsref.md)"><strong>TargetRelationNeedsRef</strong></a></p></td>
<td align="left"><p><a href="wdm-targetrelationneedsref.md" data-raw-source="[&lt;strong&gt;TargetRelationNeedsRef&lt;/strong&gt;](wdm-targetrelationneedsref.md)"> <strong>TargetRelationNeedsRef</strong> </a>规则指定的处理时<em>TargetDeviceRelation</em>查询，请在驱动程序<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;strong&gt;DispatchPnP&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)"> <strong>DispatchPnP</strong> </a>例程调用以下函数以引用子设备 PDO 之一：</p>
<ul>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obfreferenceobject" data-raw-source="[&lt;strong&gt;ObReferenceObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obfreferenceobject)"><strong>ObReferenceObject</strong></a></p></li>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbyhandle" data-raw-source="[&lt;strong&gt;ObReferenceObjectByHandle&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbyhandle)"><strong>ObReferenceObjectByHandle</strong></a></p></li>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbypointer" data-raw-source="[&lt;strong&gt;ObReferenceObjectByPointer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbypointer)"><strong>ObReferenceObjectByPointer</strong></a></p></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-zwregistrycreate.md" data-raw-source="[&lt;strong&gt;ZwRegistryCreate&lt;/strong&gt;](wdm-zwregistrycreate.md)"><strong>ZwRegistryCreate</strong></a></p></td>
<td align="left"><p><a href="wdm-zwregistrycreate.md" data-raw-source="[&lt;strong&gt;ZwRegistryCreate&lt;/strong&gt;](wdm-zwregistrycreate.md)"> <strong>ZwRegistryCreate</strong> </a>规则指定后调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatekey" data-raw-source="[&lt;strong&gt;ZwCreateKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatekey)"> <strong>ZwCreateKey</strong></a>，驱动程序可以调用以下注册表仅在保存到注册表项的打开句柄时的函数 (即，任何调用之前<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntclose" data-raw-source="[&lt;strong&gt;ZwClose&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntclose)"> <strong>ZwClose</strong> </a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwdeletekey" data-raw-source="[&lt;strong&gt;ZwDeleteKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwdeletekey)"> <strong>ZwDeleteKey</strong> </a>若要关闭或删除的句柄的注册表项):</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-zwregistryopen.md" data-raw-source="[&lt;strong&gt;ZwRegistryOpen&lt;/strong&gt;](wdm-zwregistryopen.md)"><strong>ZwRegistryOpen</strong></a></p></td>
<td align="left"><p><a href="storport-zwregistryopen.md" data-raw-source="[&lt;strong&gt;ZwRegistryOpen&lt;/strong&gt;](storport-zwregistryopen.md)"> <strong>ZwRegistryOpen</strong> </a>规则指定后调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopenkey" data-raw-source="[&lt;strong&gt;ZwOpenKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopenkey)"> <strong>ZwOpenKey</strong></a>，驱动程序调用的以下注册表函数同时打开的句柄保留到注册表项 (在调用前，即<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntclose" data-raw-source="[&lt;strong&gt;ZwClose&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntclose)"> <strong>ZwClose</strong> </a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwdeletekey" data-raw-source="[&lt;strong&gt;ZwDeleteKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwdeletekey)"> <strong>ZwDeleteKey</strong></a>):</p></td>
</tr>
</tbody>
</table>

 

**若要选择其他规则集**

1.  Microsoft Visual Studio 中选择您的驱动程序项目 (.vcxProj)。 从**驱动程序**菜单上，单击**启动 Static Driver Verifier...** .

2.  单击**规则**选项卡。下**规则集**，选择**杂项**。

    若要选择的默认规则集从 Visual Studio 开发人员命令提示符窗口，请指定**Miscellaneous.sdv**与 **/check**选项。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:Miscellaneous.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅[以找到缺陷驱动程序中使用 Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)并[Static Driver Verifier 命令 (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)。

 

 





