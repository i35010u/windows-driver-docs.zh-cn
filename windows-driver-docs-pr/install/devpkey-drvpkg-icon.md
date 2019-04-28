---
title: DEVPKEY_DrvPkg_Icon
description: DEVPKEY_DrvPkg_Icon
ms.assetid: 30aa817c-9dda-4504-b51a-78ef91d0cf01
keywords:
- DEVPKEY_DrvPkg_Icon 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_DrvPkg_Icon
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 03174c0f7843337bfd333921d34d130e73681972
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342364"
---
# <a name="devpkeydrvpkgicon"></a>DEVPKEY_DrvPkg_Icon


DEVPKEY_DrvPkg_Icon 设备属性表示 Windows 用来直观地表示设备实例设备图标的列表。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_DrvPkg_Icon</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-string-list.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING_LIST&lt;/strong&gt;](devprop-type-string-list.md)"><strong>DEVPROP_TYPE_STRING_LIST</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>通过安装应用程序和安装程序的只读访问权限</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>是</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

由一个图标文件的路径指定列表中的每个图标 (\*.ico) 或对可执行文件中的图标资源的引用。

在列表中的第一个图标用作默认值。 可提供其他图标，提供设备的不同的可视表示形式。 Windows 包含允许用户选择其图标 Windows 将显示一个用户界面。 例如，Microsoft DiscoveryCam 530 现已推出蓝色、 绿色和红色。 Microsoft 提供了每种颜色的图标。 Windows 默认情况下使用蓝色图标，因为它是列表中的第一个。 但是，Windows 用户还可以选择绿色图标或红色图标。

图标列表是 NULL 分隔图标说明符的列表。 图标说明符是一个图标文件路径 (\*.ico) 或一个图标资源说明符，按如下所示：

-   图标文件的路径的格式*DirectoryPath\\filename.ico。*

-   图标资源说明符具有以下条目：

    ```cpp
    @executable-file-path,resource-identifier
    ```

    图标资源说明符的第一个字符是 at 符号 (@) 后跟可执行文件的路径 (  *\*.exe*或 *\*.dll*文件) 后, 跟一个逗号分隔符 （，）然后*资源标识符*条目。

例如，图标说明符"@shell32.dll，-30"表示可执行文件"shell32.dll"和"-30"的资源标识符。

资源标识符必须是整数值，它对应于可执行文件内的资源，如下所示：

-   如果提供的标识符为负，Windows 将使用在其标识符等于提供的标识符的绝对值的可执行文件中的资源。

-   如果提供的标识符为零，Windows 将使用在其标识符 execuable 文件中具有的最小值的可执行文件中的资源。

-   如果提供的标识符为正，例如，值*n*，Windows 在其标识符是 n + 1 中的最低值的可执行文件的可执行文件中使用的资源。 例如，如果的值*n*为 1，Windows 使用其标识符中的可执行文件具有第二低的值的资源。

可以设置的值由 DEVPKEY_DrvPkg_Icon [ **INF AddProperty 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546318)包含在[ **INF *DDInstall*部分** ](https://msdn.microsoft.com/library/windows/hardware/ff547344)的安装设备的 INF 文件。 可以通过调用检索的值 DEVPKEY_DrvPkg_Icon [ **SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)。

下面是举例说明如何使用 INF **AddProperty**指令 INF 安装的设备设置 DEVPKEY_DrvPkg_Icon *DDInstall*部分"SampleDDInstallSection":

```cpp
[SampleDDinstallSection]
...
AddProperty=SampleAddPropertySection
...

[SampleAddPropertySection] 
DeviceIcon,,,,"SomeResource.dll,-2","SomeIcon.icon"
...
```

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>在 Windows Vista 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Devpkey.h （包括 Devpkey.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**INF AddProperty Directive**](https://msdn.microsoft.com/library/windows/hardware/ff546318)

[**INF *DDInstall*部分**](https://msdn.microsoft.com/library/windows/hardware/ff547344)

[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

 

 






