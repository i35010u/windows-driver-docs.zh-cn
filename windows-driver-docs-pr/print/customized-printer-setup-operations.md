---
title: 自定义的打印机安装操作
description: 自定义的打印机安装操作
ms.assetid: 888125e9-a057-4e86-9df8-0086cedb368d
keywords:
- 自定义打印机设置操作 WDK
- INF 文件 WDK 打印，自定义安装操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79f5c378d13ba3e98b082c5c4a435093c6898102
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216818"
---
# <a name="customized-printer-setup-operations"></a>自定义的打印机安装操作

若要为使用 Ntprint.dll 的打印机（默认的 Windows 2000 和更高版本的打印机类安装程序）提供自定义的打印机设置操作，可以在打印机的 INF 文件中包含一个 **VendorSetup** inf 条目。

> [!IMPORTANT]
> 请注意， **VendorSetup** 现已弃用，不应由你开发的任何 *新* 的 v3 或 v4 驱动程序使用。 本主题仅供参考，或用于维护已使用此 INF 指令的现有 v3 驱动程序。

 请注意，如果你计划在安装打印机驱动程序的过程中显示用户界面元素，则必须使用 **VendorSetup** INF 条目。 但是，仅当绝对必要时，才应使用 **VendorSetup** INF 条目。 一项重大缺点是，其使用会阻止普通用户通过即插即用来安装打印机 (用户在这种情况下必须是管理员) 。

如果设备驱动程序未签名，或者 (的已签名或未签名的) 驱动程序的 INF 文件包含 **VendorSetup** INF 项，则无法使用服务器端安装来安装设备。 当驱动程序无符号时，安装程序会将0x8000 添加到该驱动程序的排名（如果它是已签名的驱动程序）。 如果驱动程序的 INF 文件包含 **VendorSetup** 项，安装程序会确定设备安装是否需要用户交互 (这种情况不能出现在服务器端安装中) 并停止安装。

如果驱动程序的级别为0x8000 或更大，则安装程序也会停止服务器端安装。 当具有管理权限的用户登录时，安装可以继续，此时安装程序将重新启动设备安装作为客户端安装。 对于排名为0x1000 或更大的驱动程序，并且不是，因此，硬件 ID 匹配，安装程序会在新的设备 DLL 中启动 "发现新硬件" 向导，该向导会提示用户安装驱动程序。

如果签名的驱动程序的 INF 文件包含 **VendorSetup** 项，并且驱动程序的排名小于0x1000，则安装程序不会启动 "发现新硬件" 向导。 有关详细信息，请参阅 [设备安装组件](/previous-versions/ff541277(v=vs.85)) 和 [安装程序选择驱动程序的方式](../install/how-windows-selects-a-driver-for-a-device.md)。

**VendorSetup**条目的格式如下所示：

VendorSetup = *FileName*， *FunctionName*

其中 *FileName* 是包含安装程序函数的 DLL 的名称，而 *FunctionName* 是函数的名称。 DLL 必须安装在% windir% \\ system32 目录中。 仅当通过即插即用或通过添加打印机向导安装打印机时，打印机类安装程序才会调用此 DLL 中的安装程序函数。 如果只安装了驱动程序，则不会调用安装函数 (例如，通过使用 "添加打印机驱动程序向导") 。

若要将一个或多个文件复制到% windir% \\ system32 目录，可以将 inf 写入器定义的部分的名称添加到 Inf **DestinationDirs** 部分。 在下面的示例中，"OEMVendorFiles" 部分列出了所有要复制的文件。

```inf
[DestinationDirs]
OEMVendorFiles = 11
...
[OEMVendorFiles]
vendor.dll
```

*FunctionName*指定的函数必须与以下原型匹配：

`VOID WINAPI`*FunctionName*`(HWND hWnd, HINSTANCE hInstance, LPSTR lpszCmdLine, UINT  nCmdShow);`

其中 *FunctionName* 是安装程序函数的名称。 下表显示了函数的参数及其说明。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>hWnd</em></p></td>
<td><p>指定父窗口的句柄。</p></td>
</tr>
<tr class="even">
<td><p><em>hInstance</em></p></td>
<td><p>指定调用进程的实例句柄。</p></td>
</tr>
<tr class="odd">
<td><p><em>lpszCmdLine</em></p></td>
<td><p>指定包含刚刚安装的打印机名称的 ANSI 字符串。 此字符串由 <em>FunctionName</em>解析。</p></td>
</tr>
<tr class="even">
<td><p><em>nCmdShow</em></p></td>
<td><p>指定窗口的显示方式。 控制窗口显示方式的标志是在 Winuser.h 中定义的。</p></td>
</tr>
</tbody>
</table>

打印机类安装程序会将安装程序函数作为安装操作中的最后一个步骤来调用。