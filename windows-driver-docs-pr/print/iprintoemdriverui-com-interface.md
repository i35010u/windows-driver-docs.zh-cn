---
title: IPrintOemDriverUI COM 接口
description: IPrintOemDriverUI COM 接口
ms.assetid: ed11789f-750d-4f29-b5e0-ab299a1388db
keywords:
- IPrintOemDriverUI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea05008ba7661731aae11aceb9b83f1d9869045d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371141"
---
# <a name="iprintoemdriverui-com-interface"></a>IPrintOemDriverUI COM 接口





`IPrintOemDriverUI` COM 接口，插件的 UI 来查看和修改信息由[打印机接口 DLL](printer-interface-dll.md) Unidrv 或 Pscript。

下表列出并描述所有方法的`IPrintOemDriverUI`接口定义。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>方法</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553114" data-raw-source="[&lt;strong&gt;IPrintOemDriverUI::DrvGetDriverSetting&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553114)"><strong>IPrintOemDriverUI::DrvGetDriverSetting</strong></a></p></td>
<td><p>允许插件的 UI 获取打印机功能和其他内部信息的当前状态。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553115" data-raw-source="[&lt;strong&gt;IPrintOemDriverUI::DrvUpdateUISetting&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553115)"><strong>IPrintOemDriverUI::DrvUpdateUISetting</strong></a></p></td>
<td><p>允许插件的 UI 来通知已修改的用户界面选项的驱动程序。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553118" data-raw-source="[&lt;strong&gt;IPrintOemDriverUI::DrvUpgradeRegistrySetting&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553118)"><strong>IPrintOemDriverUI::DrvUpgradeRegistrySetting</strong></a></p></td>
<td><p>允许插件的 UI 更新存储在注册表中的设备设置。</p></td>
</tr>
</tbody>
</table>

 

有关详细信息，请参阅[实现打印机驱动程序 COM 接口](implementing-printer-driver-com-interfaces.md)。

 

 




