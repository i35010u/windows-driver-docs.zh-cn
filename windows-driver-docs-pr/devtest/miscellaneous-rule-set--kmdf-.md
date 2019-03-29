---
title: 其他规则集 (KMDF)
description: 使用这些规则，以验证您的驱动程序正确地遵循一组常规设备的要求正确处理对象时，密钥和驱动程序执行不进行调用到 DDIs 不适合非 PnP 驱动程序或不是采购订单的非 FDO 驱动程序wer 策略所有者。
ms.assetid: B8F9FBE1-ED27-47EC-ACFC-8BD354A5E72D
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 14ec67b8e46ea7e7d8676a0c8e79499df0222fbd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567226"
---
# <a name="miscellaneous-rule-set-kmdf"></a>其他规则集 (KMDF)


使用这些规则，以验证您的驱动程序正确地遵循一组常规设备的要求正确处理对象时，密钥和驱动程序执行不进行调用到 DDIs 不适合非 PnP 驱动程序或不是采购订单的非 FDO 驱动程序wer 策略所有者。

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
<td align="left"><p><a href="kmdf-accesshardwarekey.md" data-raw-source="[&lt;strong&gt;AccessHardwareKey&lt;/strong&gt;](kmdf-accesshardwarekey.md)"><strong>AccessHardwareKey</strong></a></p></td>
<td align="left"><p><a href="kmdf-accesshardwarekey.md" data-raw-source="[&lt;strong&gt;AccessHardwareKey&lt;/strong&gt;](kmdf-accesshardwarekey.md)"> <strong>AccessHardwareKey</strong> </a>规则指定总线驱动程序不应尝试访问的子设备的硬件密钥<a href="https://msdn.microsoft.com/library/windows/hardware/ff540828" data-raw-source="[&lt;em&gt;EvtChildListCreateDevice&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540828)"> <em>EvtChildListCreateDevice</em></a>.</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-addpdotostaticchildlist.md" data-raw-source="[&lt;strong&gt;AddPdotoStaticChildlist&lt;/strong&gt;](kmdf-addpdotostaticchildlist.md)"><strong>AddPdotoStaticChildlist</strong></a></p></td>
<td align="left"><p>AddPdotoStaticChildlist 规则指定 PDO 设备，framework 函数<a href="https://msdn.microsoft.com/library/windows/hardware/ff547225" data-raw-source="[&lt;strong&gt;WdfFdoAddStaticChild&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547225)"> <strong>WdfFdoAddStaticChild</strong> </a>驱动程序调用后，必须调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff548786" data-raw-source="[&lt;strong&gt;WdfPdoInitAllocate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548786)"> <strong>WdfPdoInitAllocate</strong> </a>并<a href="https://msdn.microsoft.com/library/windows/hardware/ff545926" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545926)"> <strong>WdfDeviceCreate</strong> </a>成功。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-childlistconfiguration.md" data-raw-source="[&lt;strong&gt;ChildListConfiguration&lt;/strong&gt;](kmdf-childlistconfiguration.md)"><strong>ChildListConfiguration</strong></a></p></td>
<td align="left"><p><a href="kmdf-childlistconfiguration.md" data-raw-source="[&lt;strong&gt;ChildListConfiguration&lt;/strong&gt;](kmdf-childlistconfiguration.md)"> <strong>ChildListConfiguration</strong> </a>规则指定支持的驱动程序<a href="https://msdn.microsoft.com/library/windows/hardware/ff540812" data-raw-source="[Dynamic Enumeration](https://msdn.microsoft.com/library/windows/hardware/ff540812)">动态枚举</a>必须调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff547258" data-raw-source="[&lt;strong&gt;WdfFdoInitSetDefaultChildListConfig&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547258)"> <strong>WdfFdoInitSetDefaultChildListConfig</strong> </a>之前，调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff545926" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545926)"> <strong>WdfDeviceCreate</strong> </a>函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-cleanup4ctldeviceregistered.md" data-raw-source="[&lt;strong&gt;Cleanup4CtlDeviceRegistered&lt;/strong&gt;](kmdf-cleanup4ctldeviceregistered.md)"><strong>Cleanup4CtlDeviceRegistered</strong></a></p></td>
<td align="left"><p><a href="kmdf-cleanup4ctldeviceregistered.md" data-raw-source="[&lt;strong&gt;Cleanup4CtlDeviceRegistered&lt;/strong&gt;](kmdf-cleanup4ctldeviceregistered.md)"> <strong>Cleanup4CtlDeviceRegistered</strong> </a>规则指定如果插即用 (PnP) 驱动程序调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff545926" data-raw-source="[&lt;strong&gt;WdfDeviceCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545926)"> <strong>WdfDeviceCreate</strong> </a>为控制设备对象，该驱动程序必须注册一个必需的事件回调函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-nonfdonotpowerpolicyownerapi.md" data-raw-source="[&lt;strong&gt;NonFDONotPowerPolicyOwnerAPI&lt;/strong&gt;](kmdf-nonfdonotpowerpolicyownerapi.md)"><strong>NonFDONotPowerPolicyOwnerAPI</strong></a></p></td>
<td align="left"><p><a href="kmdf-nonfdonotpowerpolicyownerapi.md" data-raw-source="[&lt;strong&gt;NonFDONotPowerPolicyOwnerAPI&lt;/strong&gt;](kmdf-nonfdonotpowerpolicyownerapi.md)"> <strong>NonFDONotPowerPolicyOwnerAPI</strong> </a>规则指定一个非 FDO 驱动程序不是电源策略所有者，是否某些 DDIs 不能调用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-nonpnpdrvpowerpolicyownerapi.md" data-raw-source="[&lt;strong&gt;NonPnPDrvPowerPolicyOwnerAPI&lt;/strong&gt;](kmdf-nonpnpdrvpowerpolicyownerapi.md)"><strong>NonPnPDrvPowerPolicyOwnerAPI</strong></a></p></td>
<td align="left"><p><a href="kmdf-nonpnpdrvpowerpolicyownerapi.md" data-raw-source="[&lt;strong&gt;NonPnPDrvPowerPolicyOwnerAPI&lt;/strong&gt;](kmdf-nonpnpdrvpowerpolicyownerapi.md)"> <strong>NonPnPDrvPowerPolicyOwnerAPI</strong> </a>规则指定非 PnP 驱动程序不能调用某些 DDIs 与电源管理相关。</p></td>
</tr>
</tbody>
</table>

 

**若要选择其他规则集**

1.  Microsoft Visual Studio 中选择您的驱动程序项目 (.vcxProj)。 从**驱动程序**菜单上，单击**启动 Static Driver Verifier...**.

2.  单击**规则**选项卡。下**规则集**，选择**杂项**。

    若要选择的默认规则集从 Visual Studio 开发人员命令提示符窗口，请指定**Miscellaneous.sdv**与 **/check**选项。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:Miscellaneous.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅[以找到缺陷驱动程序中使用 Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/hh454281)并[Static Driver Verifier 命令 (MSBuild)](https://msdn.microsoft.com/library/windows/hardware/hh466459)。

 

 





