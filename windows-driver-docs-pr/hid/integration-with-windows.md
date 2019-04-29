---
title: 与 Windows 集成
description: 与 Windows 集成
ms.assetid: 57721e38-5974-4080-b051-93b78a7f42c6
keywords:
- 属性表 WDK DirectInput 注册
- 游戏控制器 WDK DirectInput，注册
- 控制面板 WDK DirectInput，注册
- 属性表 WDK DirectInput，Windows 集成
- 游戏控制器 WDK DirectInput，Windows 集成
- 控制面板 WDK DirectInput，Windows 集成
- Windows 集成 WDK DirectInput 控制面板
- 注册属性表
- 注册设备 DirectInput 控件面板
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f3649c75c807479fc1040577ded80728582ce405
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364639"
---
# <a name="integration-with-windows"></a>与 Windows 集成





属性表页是一个 COM 对象，因为它需要注册。 可以通过一个 INF 文件或 DirectInput 的完成**IDirectInputJoyConfig8**接口。 示例 INF 文件是示例属性表中 DirectX 驱动程序开发工具包 (DDK) 的一部分。

**若要注册的属性表页：**

1.  使用 GuidGen 工具 （它包含在 Microsoft Windows SDK 中） 创建属性表的 CLSID (这是与输入中的一个相同**ConfigCLSID**条目前面所述)。 请记住，这是在特定于设备的属性表 GUID，它应与你的代码所示相同。

2.  在注册表中创建新的密钥**我的电脑\\HKEY\_类\_根\\CLSID**使用此新的 GUID （它应类似于 {B9EA2BE1-E8E9-11D0-9880-00AA0044480F})。

3.  在该注册表项，创建名为子项**InProcHandler32**并**InProcServer32**。

4.  内部**InProcServer32**密钥，请编辑 （默认） 条目以反映的位置和在属性表 DLL 的名称。

你的设备还必须正确注册为游戏的设备中。 这可能是为了通过 DirectInput，或通过 INF 文件。

**若要注册设备：**

1.  注册表项中**我的电脑\\HKEY\_本地\_机\\系统\\CurrentControlSet\\控件\\MediaProperties\\PrivateProperties\\游戏杆\\OEM**，输入你的设备密钥。 最好使此密钥命名为与你的设备 OEM 名称相同。

2.  创建以下项：

    <table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>密钥值</th>
    <th>密钥值类型</th>
    <th>密钥值类型的内容</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>ConfigCLSID</p></td>
    <td><p>字符串值</p></td>
    <td><p>"{你属性表 CLSID}"</p></td>
    </tr>
    <tr class="even">
    <td><p>OEMName</p></td>
    <td><p>字符串值</p></td>
    <td><p>"设备的产品名称"</p></td>
    </tr>
    </tbody>
    </table>

     

**请注意**  这些两个条目均需要开始最小值。 请参阅 DirectX DDK 有关所有可用的注册表项和其关联的服务的其他信息。

 

 

 




