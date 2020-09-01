---
title: IPrintOemDriverUI COM 接口
description: IPrintOemDriverUI COM 接口
ms.assetid: ed11789f-750d-4f29-b5e0-ab299a1388db
keywords:
- IPrintOemDriverUI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0246fe2782be6d8505e60d1cd5c5f43f15ec5d72
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217118"
---
# <a name="iprintoemdriverui-com-interface"></a>IPrintOemDriverUI COM 接口





使用 `IPrintOemDriverUI` COM 接口，UI 插件可以查看和修改由 Unidrv 或 Pscript 的 [打印机接口 DLL](printer-interface-dll.md) 管理的信息。

下表列出并描述了该接口定义的所有方法 `IPrintOemDriverUI` 。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>方法</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriverui-drvgetdriversetting" data-raw-source="[&lt;strong&gt;IPrintOemDriverUI::DrvGetDriverSetting&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriverui-drvgetdriversetting)"><strong>IPrintOemDriverUI：:D rvGetDriverSetting</strong></a></p></td>
<td><p>允许 UI 插件获取打印机功能和其他内部信息的当前状态。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriverui-drvupdateuisetting" data-raw-source="[&lt;strong&gt;IPrintOemDriverUI::DrvUpdateUISetting&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriverui-drvupdateuisetting)"><strong>IPrintOemDriverUI：:D rvUpdateUISetting</strong></a></p></td>
<td><p>允许 UI 插件通知驱动程序已修改的用户界面选项。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriverui-drvupgraderegistrysetting" data-raw-source="[&lt;strong&gt;IPrintOemDriverUI::DrvUpgradeRegistrySetting&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriverui-drvupgraderegistrysetting)"><strong>IPrintOemDriverUI：:D rvUpgradeRegistrySetting</strong></a></p></td>
<td><p>启用 UI 插件以更新注册表中存储的设备设置。</p></td>
</tr>
</tbody>
</table>

 

有关详细信息，请参阅 [实现打印机驱动程序 COM 接口](implementing-printer-driver-com-interfaces.md)。

 

