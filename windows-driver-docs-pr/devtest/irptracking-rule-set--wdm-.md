---
title: IrpTracking 规则集 (WDM)
description: 使用这些规则验证你的驱动程序是否正确跟踪 (IRP) 的 i/o 请求包，以便在完成 Irp 时不删除设备。
ms.assetid: 9AD62397-6840-42FF-ADEC-6836EDD16647
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6215f2c836d5a5c28e4dbf8997ffe304574f47e7
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89383949"
---
# <a name="irptracking-rule-set-wdm"></a>IrpTracking 规则集 (WDM)


使用这些规则验证你的驱动程序是否正确跟踪 (IRP) 的 i/o 请求包，以便在完成 Irp 时不删除设备。

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
<td align="left"><p><a href="wdm-ioreleaseremovelockandwaitoutsideremovedevice.md" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLockAndWaitOutsideRemoveDevice&lt;/strong&gt;](wdm-ioreleaseremovelockandwaitoutsideremovedevice.md)"><strong>IoReleaseRemoveLockAndWaitOutsideRemoveDevice</strong></a></p></td>
<td align="left"><p><a href="wdm-ioreleaseremovelockandwaitoutsideremovedevice.md" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLockAndWaitOutsideRemoveDevice&lt;/strong&gt;](wdm-ioreleaseremovelockandwaitoutsideremovedevice.md)"><strong>IoReleaseRemoveLockAndWaitOutsideRemoveDevice</strong></a>规则指定不应使用 PNP 驱动程序 IRP_MN_REMOVE_DEVICE IRP_MJ_PNP 之外调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLockAndWait&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait)"><strong>IoReleaseRemoveLockAndWait</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-nsremovelockmnremove.md" data-raw-source="[&lt;strong&gt;NsRemoveLockMnRemove&lt;/strong&gt;](wdm-nsremovelockmnremove.md)"><strong>NsRemoveLockMnRemove</strong></a></p></td>
<td align="left"><p>当使用 MinorFunction IRP_MN_REMOVE_DEVICE 处理 IRP_MJ_PNP 时， <a href="wdm-nsremovelockmnremove.md" data-raw-source="[&lt;strong&gt;NsRemoveLockMnRemove&lt;/strong&gt;](wdm-nsremovelockmnremove.md)"><strong>NsRemoveLockMnRemove</strong></a> 规则将验证驱动程序是否未返回 STATUS_NOT_SUPPORTED。 此规则仅适用于 FDO 和 FIDO 驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-nsremovelockmnsurpriseremove.md" data-raw-source="[&lt;strong&gt;NsRemoveLockMnSurpriseRemove&lt;/strong&gt;](wdm-nsremovelockmnsurpriseremove.md)"><strong>NsRemoveLockMnSurpriseRemove</strong></a></p></td>
<td align="left"><p>当使用 minorFunction IRP_MN_SUPRISE_REMOVAL 处理 IRP_MJ_PNP 请求时， <a href="wdm-nsremovelockmnsurpriseremove.md" data-raw-source="[&lt;strong&gt;NsRemoveLockMnSurpriseRemove&lt;/strong&gt;](wdm-nsremovelockmnsurpriseremove.md)"><strong>NsRemoveLockMnSurpriseRemove</strong></a> 规则将验证驱动程序是否未返回 STATUS_NOT_SUPPORTED。 此规则仅适用于 FDO 和 FIDO 驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-nsremovelockquerymnremove.md" data-raw-source="[&lt;strong&gt;NsRemoveLockQueryMnRemove&lt;/strong&gt;](wdm-nsremovelockquerymnremove.md)"><strong>NsRemoveLockQueryMnRemove</strong></a></p></td>
<td align="left"><p>当使用 MinorFunction IRP_MN_QUERY_REMOVE 处理 IRP_MJ_PNP 时， <a href="wdm-nsremovelockquerymnremove.md" data-raw-source="[&lt;strong&gt;NsRemoveLockQueryMnRemove&lt;/strong&gt;](wdm-nsremovelockquerymnremove.md)"><strong>NsRemoveLockQueryMnRemove</strong></a> 规则将验证驱动程序是否未返回 STATUS_NOT_SUPPORTED。 此规则仅适用于 FDO 和 FIDO 驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-removelock.md" data-raw-source="[&lt;strong&gt;RemoveLock&lt;/strong&gt;](wdm-removelock.md)"><strong>RemoveLock</strong></a></p></td>
<td align="left"><p><a href="wdm-removelock.md" data-raw-source="[&lt;strong&gt;RemoveLock&lt;/strong&gt;](wdm-removelock.md)"><strong>RemoveLock</strong></a>规则指定正确使用对<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)"><strong>IoAcquireRemoveLock</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)"><strong>IoReleaseRemoveLock</strong></a>的调用。 此外，在 IRP_MJ_PNP 或 IRP_MJ_POWER 例程的末尾，驱动程序不应 <strong>RemoveLock</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-removelockcheck.md" data-raw-source="[&lt;strong&gt;RemoveLockCheck&lt;/strong&gt;](wdm-removelockcheck.md)"><strong>RemoveLockCheck</strong></a></p></td>
<td align="left"><p>当使用 MinorFunction IRP_MN_REMOVE_DEVICE IRP_MJ_PNP 处理时， <a href="wdm-removelockcheck.md" data-raw-source="[&lt;strong&gt;RemoveLockCheck&lt;/strong&gt;](wdm-removelockcheck.md)"><strong>RemoveLockCheck</strong></a> 规则验证对 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)"><strong>IoAcquireRemoveLock</strong></a> 和 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLockAndWait&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait)"><strong>IoReleaseRemoveLockAndWait</strong></a> 的调用是否正确使用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-removelockforward.md" data-raw-source="[&lt;strong&gt;RemoveLockForward&lt;/strong&gt;](wdm-removelockforward.md)"><strong>RemoveLockForward</strong></a></p></td>
<td align="left"><p><a href="wdm-removelockforward.md" data-raw-source="[&lt;strong&gt;RemoveLockForward&lt;/strong&gt;](wdm-removelockforward.md)"><strong>RemoveLockForward</strong></a>规则在将 IRP 转发到另一台设备时，验证是否正确使用了对<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)"><strong>IoAcquireRemoveLock</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)"><strong>IoReleaseRemoveLock</strong></a>的调用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-removelockforward2.md" data-raw-source="[&lt;strong&gt;RemoveLockForward2&lt;/strong&gt;](wdm-removelockforward2.md)"><strong>RemoveLockForward2</strong></a></p></td>
<td align="left"><p>在将 IRP 转发到另一台设备时， <a href="wdm-removelockforward2.md" data-raw-source="[&lt;strong&gt;RemoveLockForward2&lt;/strong&gt;](wdm-removelockforward2.md)"><strong>RemoveLockForward2</strong></a> 规则验证对 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)"><strong>IoAcquireRemoveLock</strong></a> 和 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)"><strong>IoReleaseRemoveLock</strong></a> 的调用是否正确使用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-removelockforwarddevicecontrol.md" data-raw-source="[&lt;strong&gt;RemoveLockForwardDeviceControl&lt;/strong&gt;](wdm-removelockforwarddevicecontrol.md)"><strong>RemoveLockForwardDeviceControl</strong></a></p></td>
<td align="left"><p>当驱动程序使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a>将 IRP 转发到另一台设备时， <a href="wdm-removelockforwarddevicecontrol.md" data-raw-source="[&lt;strong&gt;RemoveLockForwardDeviceControl&lt;/strong&gt;](wdm-removelockforwarddevicecontrol.md)"><strong>RemoveLockForwardDeviceControl</strong></a>规则将验证是否正确使用了对<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)"><strong>IoAcquireRemoveLock</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)"><strong>IoReleaseRemoveLock</strong></a>的调用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-removelockforwarddevicecontrol2.md" data-raw-source="[&lt;strong&gt;RemoveLockForwardDeviceControl2&lt;/strong&gt;](wdm-removelockforwarddevicecontrol2.md)"><strong>RemoveLockForwardDeviceControl2</strong></a></p></td>
<td align="left"><p>当驱动程序使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a>将 IRP 转发到另一台设备时， <a href="wdm-removelockforwarddevicecontrol2.md" data-raw-source="[&lt;strong&gt;RemoveLockForwardDeviceControl2&lt;/strong&gt;](wdm-removelockforwarddevicecontrol2.md)"><strong>RemoveLockForwardDeviceControl2</strong></a>规则将验证是否正确使用了对<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)"><strong>IoAcquireRemoveLock</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)"><strong>IoReleaseRemoveLock</strong></a>的调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-removelockforwarddevicecontrolinternal.md" data-raw-source="[&lt;strong&gt;RemoveLockForwardDeviceControlInternal&lt;/strong&gt;](wdm-removelockforwarddevicecontrolinternal.md)"><strong>RemoveLockForwardDeviceControlInternal</strong></a></p></td>
<td align="left"><p>当使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a>将 IRP 转发到另一台设备时， <a href="wdm-removelockforwarddevicecontrolinternal.md" data-raw-source="[&lt;strong&gt;RemoveLockForwardDeviceControlInternal&lt;/strong&gt;](wdm-removelockforwarddevicecontrolinternal.md)"><strong>RemoveLockForwardDeviceControlInternal</strong></a>规则将验证是否正确地使用对<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)"><strong>IoAcquireRemoveLock</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)"><strong>IoReleaseRemoveLock</strong></a>的调用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-removelockforwarddevicecontrolinternal2.md" data-raw-source="[&lt;strong&gt;RemoveLockForwardDeviceControlInternal2&lt;/strong&gt;](wdm-removelockforwarddevicecontrolinternal2.md)"><strong>RemoveLockForwardDeviceControlInternal2</strong></a></p></td>
<td align="left"><p>当使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a>将 IRP 转发到另一台设备时， <a href="wdm-removelockforwarddevicecontrolinternal2.md" data-raw-source="[&lt;strong&gt;RemoveLockForwardDeviceControlInternal2&lt;/strong&gt;](wdm-removelockforwarddevicecontrolinternal2.md)"><strong>RemoveLockForwardDeviceControlInternal2</strong></a>规则将验证是否正确地使用对<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)"><strong>IoAcquireRemoveLock</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)"><strong>IoReleaseRemoveLock</strong></a>的调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-removelockforwardread.md" data-raw-source="[&lt;strong&gt;RemoveLockForwardRead&lt;/strong&gt;](wdm-removelockforwardread.md)"><strong>RemoveLockForwardRead</strong></a></p></td>
<td align="left"><p><a href="wdm-removelockforwardread.md" data-raw-source="[&lt;strong&gt;RemoveLockForwardRead&lt;/strong&gt;](wdm-removelockforwardread.md)"><strong>RemoveLockForwardRead</strong></a>规则验证是否正确使用了对<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)"><strong>IoAcquireRemoveLock</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)"><strong>IoReleaseRemoveLock</strong></a>的调用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-removelockforwardread2.md" data-raw-source="[&lt;strong&gt;RemoveLockForwardRead2&lt;/strong&gt;](wdm-removelockforwardread2.md)"><strong>RemoveLockForwardRead2</strong></a></p></td>
<td align="left"><p>当使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a>将 IRP 转发到另一台设备时， <a href="wdm-removelockforwardread2.md" data-raw-source="[&lt;strong&gt;RemoveLockForwardRead2&lt;/strong&gt;](wdm-removelockforwardread2.md)"><strong>RemoveLockForwardRead2</strong></a>规则将验证是否正确地使用了对<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)"><strong>IoAcquireRemoveLock</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)"><strong>IoReleaseRemoveLock</strong></a>的调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-removelockforwardwrite.md" data-raw-source="[&lt;strong&gt;RemoveLockForwardWrite&lt;/strong&gt;](wdm-removelockforwardwrite.md)"><strong>RemoveLockForwardWrite</strong></a></p></td>
<td align="left"><p>当使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a>将 IRP 转发到另一台设备时， <a href="wdm-removelockforwardwrite.md" data-raw-source="[&lt;strong&gt;RemoveLockForwardWrite&lt;/strong&gt;](wdm-removelockforwardwrite.md)"><strong>RemoveLockForwardWrite</strong></a>规则将验证是否正确地使用了对<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)"><strong>IoAcquireRemoveLock</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)"><strong>IoReleaseRemoveLock</strong></a>的调用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-removelockforwardwrite2.md" data-raw-source="[&lt;strong&gt;RemoveLockForwardWrite2&lt;/strong&gt;](wdm-removelockforwardwrite2.md)"><strong>RemoveLockForwardWrite2</strong></a></p></td>
<td align="left"><p>当使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a>将 IRP 转发到另一台设备时， <a href="wdm-removelockforwardwrite2.md" data-raw-source="[&lt;strong&gt;RemoveLockForwardWrite2&lt;/strong&gt;](wdm-removelockforwardwrite2.md)"><strong>RemoveLockForwardWrite2</strong></a>规则将验证是否正确地使用了对<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)"><strong>IoAcquireRemoveLock</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)"><strong>IoReleaseRemoveLock</strong></a>的调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-removelockmnremove.md" data-raw-source="[&lt;strong&gt;RemoveLockMnRemove&lt;/strong&gt;](wdm-removelockmnremove.md)"><strong>RemoveLockMnRemove</strong></a></p></td>
<td align="left"><p>当使用 MinorFunction IRP_MN_REMOVE_DEVICE IRP_MJ_PNP 处理时， <a href="wdm-removelockmnremove.md" data-raw-source="[&lt;strong&gt;RemoveLockMnRemove&lt;/strong&gt;](wdm-removelockmnremove.md)"><strong>RemoveLockMnRemove</strong></a> 规则验证对 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)"><strong>IoAcquireRemoveLock</strong></a> 和 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLockAndWait&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait)"><strong>IoReleaseRemoveLockAndWait</strong></a> 的调用是否正确使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-removelockmnremove2.md" data-raw-source="[&lt;strong&gt;RemoveLockMnRemove2&lt;/strong&gt;](wdm-removelockmnremove2.md)"><strong>RemoveLockMnRemove2</strong></a></p></td>
<td align="left"><p><a href="wdm-removelockmnremove2.md" data-raw-source="[&lt;strong&gt;RemoveLockMnRemove2&lt;/strong&gt;](wdm-removelockmnremove2.md)"><strong>RemoveLockMnRemove2</strong></a>规则验证在将 IRP 转发到较低版本的驱动程序之前处理 IRP_MN_REMOVE_DEVICE 请求时，对<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)"><strong>IoAcquireRemoveLock</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLockAndWait&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait)"><strong>IoReleaseRemoveLockAndWait</strong></a>的调用是否正确使用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-removelockmnsurpriseremove.md" data-raw-source="[&lt;strong&gt;RemoveLockMnSurpriseRemove&lt;/strong&gt;](wdm-removelockmnsurpriseremove.md)"><strong>RemoveLockMnSurpriseRemove</strong></a></p></td>
<td align="left"><p>当使用 MinorFunction IRP_MN_SUPRISE_REMOVAL IRP_MJ_PNP 处理时， <a href="wdm-removelockmnsurpriseremove.md" data-raw-source="[&lt;strong&gt;RemoveLockMnSurpriseRemove&lt;/strong&gt;](wdm-removelockmnsurpriseremove.md)"><strong>RemoveLockMnSurpriseRemove</strong></a> 规则验证对 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)"><strong>IoAcquireRemoveLock</strong></a> 和 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLockAndWait&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait)"><strong>IoReleaseRemoveLockAndWait</strong></a> 的调用是否正确使用。 在将 IRP 转发到堆栈之前，驱动程序应该获取删除锁定。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-removelockquerymnremove.md" data-raw-source="[&lt;strong&gt;RemoveLockQueryMnRemove&lt;/strong&gt;](wdm-removelockquerymnremove.md)"><strong>RemoveLockQueryMnRemove</strong></a></p></td>
<td align="left"><p>当使用 MinorFunction IRP_MN_QUERY_REMOVE_DEVICE IRP_MJ_PNP 处理时， <a href="wdm-removelockquerymnremove.md" data-raw-source="[&lt;strong&gt;RemoveLockQueryMnRemove&lt;/strong&gt;](wdm-removelockquerymnremove.md)"><strong>RemoveLockQueryMnRemove</strong></a> 规则验证对 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)"><strong>IoAcquireRemoveLock</strong></a> 和 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)"><strong>IoReleaseRemoveLock</strong></a> 的调用是否正确使用。 在将 IRP 转发到堆栈之前，驱动程序应该获取删除锁定。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-removelockrelease2.md" data-raw-source="[&lt;strong&gt;RemoveLockRelease2&lt;/strong&gt;](wdm-removelockrelease2.md)"><strong>RemoveLockRelease2</strong></a></p></td>
<td align="left"><p>规则 <a href="wdm-removelockrelease2.md" data-raw-source="[&lt;strong&gt;RemoveLockRelease2&lt;/strong&gt;](wdm-removelockrelease2.md)"><strong>RemoveLockRelease2</strong></a> 验证是否在严格替换中使用对 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)"><strong>IoAcquireRemoveLock</strong></a> 和 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)"><strong>IoReleaseRemoveLock</strong></a> 的调用。 而且，在调度例程结束时，驱动程序不应持有删除锁定。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-removelockreleasecleanup.md" data-raw-source="[&lt;strong&gt;RemoveLockReleaseCleanup&lt;/strong&gt;](wdm-removelockreleasecleanup.md)"><strong>RemoveLockReleaseCleanup</strong></a></p></td>
<td align="left"><p><a href="wdm-removelockreleasecleanup.md" data-raw-source="[&lt;strong&gt;RemoveLockReleaseCleanup&lt;/strong&gt;](wdm-removelockreleasecleanup.md)"><strong>RemoveLockReleaseCleanup</strong></a>规则指定在严格替换中使用对<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)"><strong>IoAcquireRemoveLock</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)"><strong>IoReleaseRemoveLock</strong></a>的调用。 对 <strong>IoAcquireRemoveLock</strong> 的每次调用都必须具有对 <strong>IoReleaseRemoveLock</strong>的匹配调用。 而且，在调度例程结束时，驱动程序不应持有删除锁定。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-removelockreleaseclose.md" data-raw-source="[&lt;strong&gt;RemoveLockReleaseClose&lt;/strong&gt;](wdm-removelockreleaseclose.md)"><strong>RemoveLockReleaseClose</strong></a></p></td>
<td align="left"><p>规则 <a href="wdm-removelockreleaseclose.md" data-raw-source="[&lt;strong&gt;RemoveLockReleaseClose&lt;/strong&gt;](wdm-removelockreleaseclose.md)"><strong>RemoveLockReleaseClose</strong></a> 验证是否在严格替换中使用对 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)"><strong>IoAcquireRemoveLock</strong></a> 和 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)"><strong>IoReleaseRemoveLock</strong></a> 的调用。 而且，在调度例程结束时，驱动程序不应持有删除锁定。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-removelockreleasecreate.md" data-raw-source="[&lt;strong&gt;RemoveLockReleaseCreate&lt;/strong&gt;](wdm-removelockreleasecreate.md)"><strong>RemoveLockReleaseCreate</strong></a></p></td>
<td align="left"><p><a href="wdm-removelockreleasecreate.md" data-raw-source="[&lt;strong&gt;RemoveLockReleaseCreate&lt;/strong&gt;](wdm-removelockreleasecreate.md)"><strong>RemoveLockReleaseCreate</strong></a>规则验证是否在严格替换中使用对<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)"><strong>IoAcquireRemoveLock</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)"><strong>IoReleaseRemoveLock</strong></a>的调用。 而且，在调度例程结束时，驱动程序不应持有删除锁定。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-removelockreleasedevicecontrol.md" data-raw-source="[&lt;strong&gt;RemoveLockReleaseDeviceControl&lt;/strong&gt;](wdm-removelockreleasedevicecontrol.md)"><strong>RemoveLockReleaseDeviceControl</strong></a></p></td>
<td align="left"><p><a href="wdm-removelockreleasedevicecontrol.md" data-raw-source="[&lt;strong&gt;RemoveLockReleaseDeviceControl&lt;/strong&gt;](wdm-removelockreleasedevicecontrol.md)"><strong>RemoveLockReleaseDeviceControl</strong></a>规则验证是否在严格替换中使用对<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)"><strong>IoAcquireRemoveLock</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)"><strong>IoReleaseRemoveLock</strong></a>的调用。 而且，在调度例程结束时，驱动程序不应持有删除锁定。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-removelockreleaseinternaldevicecontrol.md" data-raw-source="[&lt;strong&gt;RemoveLockReleaseInternalDeviceControl&lt;/strong&gt;](wdm-removelockreleaseinternaldevicecontrol.md)"><strong>RemoveLockReleaseInternalDeviceControl</strong></a></p></td>
<td align="left"><p><a href="wdm-removelockreleaseinternaldevicecontrol.md" data-raw-source="[&lt;strong&gt;RemoveLockReleaseInternalDeviceControl&lt;/strong&gt;](wdm-removelockreleaseinternaldevicecontrol.md)"><strong>RemoveLockReleaseInternalDeviceControl</strong></a>规则验证是否在严格替换中使用对<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)"><strong>IoAcquireRemoveLock</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)"><strong>IoReleaseRemoveLock</strong></a>的调用。 而且，在调度例程结束时，驱动程序不应持有删除锁定。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-removelockreleasepnp.md" data-raw-source="[&lt;strong&gt;RemoveLockReleasePnp&lt;/strong&gt;](wdm-removelockreleasepnp.md)"><strong>RemoveLockReleasePnp</strong></a></p></td>
<td align="left"><p><a href="wdm-removelockreleasepnp.md" data-raw-source="[&lt;strong&gt;RemoveLockReleasePnp&lt;/strong&gt;](wdm-removelockreleasepnp.md)"><strong>RemoveLockReleasePnp</strong></a>规则验证是否在严格替换中使用对<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)"><strong>IoAcquireRemoveLock</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)"><strong>IoReleaseRemoveLock</strong></a>的调用。 而且，在调度例程结束时，驱动程序不应持有删除锁定。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-removelockreleasepower.md" data-raw-source="[&lt;strong&gt;RemoveLockReleasePower&lt;/strong&gt;](wdm-removelockreleasepower.md)"><strong>RemoveLockReleasePower</strong></a></p></td>
<td align="left"><p><a href="wdm-removelockreleasepower.md" data-raw-source="[&lt;strong&gt;RemoveLockReleasePower&lt;/strong&gt;](wdm-removelockreleasepower.md)"><strong>RemoveLockReleasePower</strong></a>规则验证是否在严格替换中使用对<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)"><strong>IoAcquireRemoveLock</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)"><strong>IoReleaseRemoveLock</strong></a>的调用。 而且，在调度例程结束时，驱动程序不应持有删除锁定。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-removelockreleaseread.md" data-raw-source="[&lt;strong&gt;RemoveLockReleaseRead&lt;/strong&gt;](wdm-removelockreleaseread.md)"><strong>RemoveLockReleaseRead</strong></a></p></td>
<td align="left"><p><a href="wdm-removelockreleaseread.md" data-raw-source="[&lt;strong&gt;RemoveLockReleaseRead&lt;/strong&gt;](wdm-removelockreleaseread.md)"><strong>RemoveLockReleaseRead</strong></a>规则验证是否在严格替换中使用对<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)"><strong>IoAcquireRemoveLock</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)"><strong>IoReleaseRemoveLock</strong></a>的调用。 而且，在调度例程结束时，驱动程序不应持有删除锁定。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-removelockreleaseshutdown.md" data-raw-source="[&lt;strong&gt;RemoveLockReleaseShutdown&lt;/strong&gt;](wdm-removelockreleaseshutdown.md)"><strong>RemoveLockReleaseShutdown</strong></a></p></td>
<td align="left"><p><a href="wdm-removelockreleaseshutdown.md" data-raw-source="[&lt;strong&gt;RemoveLockReleaseShutdown&lt;/strong&gt;](wdm-removelockreleaseshutdown.md)"><strong>RemoveLockReleaseShutdown</strong></a>规则验证是否在严格替换中使用对<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)"><strong>IoAcquireRemoveLock</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)"><strong>IoReleaseRemoveLock</strong></a>的调用。 而且，在调度例程结束时，驱动程序不应持有删除锁定。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-removelockreleasesystemcontrol.md" data-raw-source="[&lt;strong&gt;RemoveLockReleaseSystemControl&lt;/strong&gt;](wdm-removelockreleasesystemcontrol.md)"><strong>RemoveLockReleaseSystemControl</strong></a></p></td>
<td align="left"><p><a href="wdm-removelockreleasesystemcontrol.md" data-raw-source="[&lt;strong&gt;RemoveLockReleaseSystemControl&lt;/strong&gt;](wdm-removelockreleasesystemcontrol.md)"><strong>RemoveLockReleaseSystemControl</strong></a>规则验证是否在严格替换中使用对<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)"><strong>IoAcquireRemoveLock</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)"><strong>IoReleaseRemoveLock</strong></a>的调用。 而且，在调度例程结束时，驱动程序不应持有删除锁定。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-removelockreleasewrite.md" data-raw-source="[&lt;strong&gt;RemoveLockReleaseWrite&lt;/strong&gt;](wdm-removelockreleasewrite.md)"><strong>RemoveLockReleaseWrite</strong></a></p></td>
<td align="left"><p><a href="wdm-removelockreleasewrite.md" data-raw-source="[&lt;strong&gt;RemoveLockReleaseWrite&lt;/strong&gt;](wdm-removelockreleasewrite.md)"><strong>RemoveLockReleaseWrite</strong></a>规则验证是否在严格替换中使用对<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)"><strong>IoAcquireRemoveLock</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)"><strong>IoReleaseRemoveLock</strong></a>的调用。 而且，在调度例程结束时，驱动程序不应持有删除锁定。</p></td>
</tr>
</tbody>
</table>

 

**选择 IrpTracking 规则集**

1.  选择你的驱动程序项目 () 在 Microsoft Visual Studio 中。 在 " **驱动程序** " 菜单中，单击 " **启动静态驱动程序验证程序 ...**"。

2.  单击 " **规则** " 选项卡。在 " **规则集**" 下，选择 **IrpTracking**。

    若要从 Visual Studio 开发人员命令提示符窗口中选择默认规则集，请使用 **/check**选项指定**IrpTracking。 sdv** 。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:IrpTracking.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅 [使用静态驱动程序验证器查找驱动程序中的缺陷](./using-static-driver-verifier-to-find-defects-in-drivers.md) 和 [静态驱动程序验证程序命令 (MSBuild) ](./-static-driver-verifier-commands--msbuild-.md)。

 

