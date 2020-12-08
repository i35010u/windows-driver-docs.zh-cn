---
title: 其他规则集 (KMDF)
description: 使用这些规则来验证驱动程序是否正确地遵循了对设备对象、密钥的正确处理的一般要求，以及该驱动程序不会对非 PnP 驱动程序或不是电源策略所有者的非 FDO 驱动程序调用 DDIs。
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: d9c2fe6ad66fe34ada391c7086e5f51d865c7f3d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837319"
---
# <a name="miscellaneous-rule-set-kmdf"></a>其他规则集 (KMDF)


使用这些规则来验证驱动程序是否正确地遵循了对设备对象、密钥的正确处理的一般要求，以及该驱动程序不会对非 PnP 驱动程序或不是电源策略所有者的非 FDO 驱动程序调用 DDIs。

## <a name="in-this-section"></a>在本节中


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
<td align="left"><p><a href="kmdf-accesshardwarekey.md" data-raw-source="[&lt;strong&gt;AccessHardwareKey&lt;/strong&gt;](kmdf-accesshardwarekey.md)"><strong>AccessHardwareKey</strong></a></p></td>
<td align="left"><p><a href="kmdf-accesshardwarekey.md" data-raw-source="[&lt;strong&gt;AccessHardwareKey&lt;/strong&gt;](kmdf-accesshardwarekey.md)"><strong>AccessHardwareKey</strong></a>规则指定总线驱动程序不应尝试从<a href="/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_create_device" data-raw-source="[&lt;em&gt;EvtChildListCreateDevice&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_create_device)"><em>EvtChildListCreateDevice</em></a>访问子设备的硬件密钥。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-addpdotostaticchildlist.md" data-raw-source="[&lt;strong&gt;AddPdotoStaticChildlist&lt;/strong&gt;](kmdf-addpdotostaticchildlist.md)"><strong>AddPdotoStaticChildlist</strong></a></p></td>
<td align="left"><p>AddPdotoStaticChildlist 规则指定对于 PDO 设备，必须在驱动程序成功调用<a href="/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitallocate" data-raw-source="[&lt;strong&gt;WdfPdoInitAllocate&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitallocate)"><strong>WdfPdoInitAllocate</strong></a>和<a href="/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)"><strong>WdfDeviceCreate</strong></a>后调用 framework 函数<a href="/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoaddstaticchild" data-raw-source="[&lt;strong&gt;WdfFdoAddStaticChild&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoaddstaticchild)"><strong>WdfFdoAddStaticChild</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-childlistconfiguration.md" data-raw-source="[&lt;strong&gt;ChildListConfiguration&lt;/strong&gt;](kmdf-childlistconfiguration.md)"><strong>ChildListConfiguration</strong></a></p></td>
<td align="left"><p><a href="kmdf-childlistconfiguration.md" data-raw-source="[&lt;strong&gt;ChildListConfiguration&lt;/strong&gt;](kmdf-childlistconfiguration.md)"><strong>ChildListConfiguration</strong></a>规则指定支持<a href="/windows-hardware/drivers/wdf/dynamic-enumeration" data-raw-source="[Dynamic Enumeration](../wdf/dynamic-enumeration.md)">动态枚举</a>的驱动程序必须先调用<a href="/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitsetdefaultchildlistconfig" data-raw-source="[&lt;strong&gt;WdfFdoInitSetDefaultChildListConfig&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitsetdefaultchildlistconfig)"><strong>WdfFdoInitSetDefaultChildListConfig</strong></a> ，然后才能调用<a href="/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)"><strong>WdfDeviceCreate</strong></a>函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-cleanup4ctldeviceregistered.md" data-raw-source="[&lt;strong&gt;Cleanup4CtlDeviceRegistered&lt;/strong&gt;](kmdf-cleanup4ctldeviceregistered.md)"><strong>Cleanup4CtlDeviceRegistered</strong></a></p></td>
<td align="left"><p><a href="kmdf-cleanup4ctldeviceregistered.md" data-raw-source="[&lt;strong&gt;Cleanup4CtlDeviceRegistered&lt;/strong&gt;](kmdf-cleanup4ctldeviceregistered.md)"><strong>Cleanup4CtlDeviceRegistered</strong></a>规则指定如果即插即用 (PnP) 驱动程序为控制设备对象调用<a href="/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)"><strong>WdfDeviceCreate</strong></a> ，则驱动程序必须注册某个必需的事件回调函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-nonfdonotpowerpolicyownerapi.md" data-raw-source="[&lt;strong&gt;NonFDONotPowerPolicyOwnerAPI&lt;/strong&gt;](kmdf-nonfdonotpowerpolicyownerapi.md)"><strong>NonFDONotPowerPolicyOwnerAPI</strong></a></p></td>
<td align="left"><p><a href="kmdf-nonfdonotpowerpolicyownerapi.md" data-raw-source="[&lt;strong&gt;NonFDONotPowerPolicyOwnerAPI&lt;/strong&gt;](kmdf-nonfdonotpowerpolicyownerapi.md)"><strong>NonFDONotPowerPolicyOwnerAPI</strong></a>规则指定如果非 FDO 驱动程序不是电源策略所有者，则无法调用某些 DDIs。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-nonpnpdrvpowerpolicyownerapi.md" data-raw-source="[&lt;strong&gt;NonPnPDrvPowerPolicyOwnerAPI&lt;/strong&gt;](kmdf-nonpnpdrvpowerpolicyownerapi.md)"><strong>NonPnPDrvPowerPolicyOwnerAPI</strong></a></p></td>
<td align="left"><p><a href="kmdf-nonpnpdrvpowerpolicyownerapi.md" data-raw-source="[&lt;strong&gt;NonPnPDrvPowerPolicyOwnerAPI&lt;/strong&gt;](kmdf-nonpnpdrvpowerpolicyownerapi.md)"><strong>NonPnPDrvPowerPolicyOwnerAPI</strong></a>规则指定非 PnP 驱动程序无法调用与电源管理相关的特定 DDIs。</p></td>
</tr>
</tbody>
</table>

 

**选择杂项规则集**

1.  选择你的驱动程序项目 () 在 Microsoft Visual Studio 中。 在 " **驱动程序** " 菜单中，单击 " **启动静态驱动程序验证程序 ...**"。

2.  单击 " **规则** " 选项卡。在 " **规则集**" 下，选择 " **杂项**"。

    若要从 Visual Studio 开发人员命令提示符窗口中选择默认规则集，请使用 **/check** 选项指定 **sdv** 。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:Miscellaneous.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅 [使用静态驱动程序验证器查找驱动程序中的缺陷](./using-static-driver-verifier-to-find-defects-in-drivers.md) 和 [静态驱动程序验证程序命令 (MSBuild) ](./-static-driver-verifier-commands--msbuild-.md)。

