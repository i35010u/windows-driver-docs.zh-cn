---
title: 自定义的打印机安装操作
description: 自定义的打印机安装操作
ms.assetid: 888125e9-a057-4e86-9df8-0086cedb368d
keywords:
- 自定义的打印机安装程序操作 WDK
- INF 文件 WDK 打印，自定义安装程序操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b274191665945b0dd410f91545bac2adb1378405
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372383"
---
# <a name="customized-printer-setup-operations"></a>自定义的打印机安装操作





若要提供自定义的打印机安装程序操作，以便使用 Ntprint.dll、 默认值为 Windows 2000 和更高版本的打印机类安装程序安装的打印机，您可以包括**VendorSetup** INF 打印机的 INF 文件中的条目。

**重要**  :请注意， **VendorSetup**现已弃用，不能由任何*新*v3 或 v4 驱动程序开发的。 本主题提供引用，或现有的 v3 驱动程序已使用此 INF 指令的维护。

 

**请注意**  如果你打算在打印机驱动程序的安装过程中显示用户界面元素，则必须使用**VendorSetup** INF 条目。 但是，应使用**VendorSetup** INF 条目仅当绝对必要。 一个明显缺点是，其使用可以防止普通用户 （用户必须在这种情况下是管理员） 的插通过安装打印机。
不能安装未签名，或者设备驱动程序时或者当 （有符号或无符号） 驱动程序的 INF 文件包含使用服务器端安装的设备**VendorSetup** INF 条目。 未签名驱动程序时，安装程序会添加到已签名的驱动程序将会获得驱动程序的排名 0x8000。 如果驱动程序的 INF 文件包含**VendorSetup**条目，安装程序确定设备的安装需要用户交互 （它不能在服务器端的安装中） 和停止安装。 安装程序在驱动程序的排名为 0x8000 时也会停止服务器端安装或更大。 登录具有管理权限的用户，此时安装程序重新启动与客户端安装在设备安装时，可以继续安装。 其排名为 0x1000 的驱动程序或更大，并且不是，因此，硬件 ID 匹配，安装程序会提示用户输入一个驱动程序安装在新设备 DLL 中找到新硬件向导启动。 如果签名的驱动程序的 INF 文件包含**VendorSetup**条目，并且该驱动程序的排名为小于 0x1000，安装程序不启动发现新硬件向导。 有关详细信息，请参阅[设备安装组件](https://docs.microsoft.com/previous-versions/ff541277(v=vs.85))并[安装程序如何选择驱动程序](https://docs.microsoft.com/windows-hardware/drivers/install/how-setup-selects-drivers)。

 

格式**VendorSetup**条目如下所示：

VendorSetup =*文件名*， *FunctionName*

其中*文件名*是包含安装程序函数的 DLL 的名称和*FunctionName*是函数的名称。 DLL 必须安装在 %windir%\\system32 目录。 仅当通过插或添加打印机向导安装打印机时，打印机类安装程序在此 DLL 中调用的安装程序函数。 驱动程序仅安装 （例如，通过使用添加打印机驱动程序向导） 时，不会调用安装程序函数。

若要将一个或多个文件复制到 %windir%\\system32 目录中，可以将 INF 编写器定义的节的名称添加到 INF **DestinationDirs**部分。 在以下示例中，OEMVendorFiles 部分列出了所有要复制的文件。

```cpp
[DestinationDirs]
OEMVendorFiles = 11
...
[OEMVendorFiles]
vendor.dll
```

由指定的函数*FunctionName*必须符合以下原型：

`VOID WINAPI         `*FunctionName*`(HWND         hWnd, HINSTANCE hInstance, LPSTR lpszCmdLine, UINT  nCmdShow);`

其中*FunctionName*是安装程序函数的名称。 下表中显示函数的参数和及其说明。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>hWnd</em></p></td>
<td><p>指定父窗口句的柄。</p></td>
</tr>
<tr class="even">
<td><p><em>hInstance</em></p></td>
<td><p>指定调用进程的实例句柄。</p></td>
</tr>
<tr class="odd">
<td><p><em>lpszCmdLine</em></p></td>
<td><p>指定包含为刚安装的打印机的名称的 ANSI 字符串。 此字符串由分析得到<em>FunctionName</em>。</p></td>
</tr>
<tr class="even">
<td><p><em>nCmdShow</em></p></td>
<td><p>指定窗口的显示方式。 控制在窗口的显示方式的标志在 Winuser.h 中定义。</p></td>
</tr>
</tbody>
</table>

 

打印机类安装程序作为安装操作中的最后一个步骤之一调用安装程序函数。

 

 




