---
title: DEVPKEY_DrvPkg_Icon
description: DEVPKEY_DrvPkg_Icon
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
ms.openlocfilehash: 96204b5dc34a3de6ba9cb87e98046b00eda8d24f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832343"
---
# <a name="devpkey_drvpkg_icon"></a>DEVPKEY_DrvPkg_Icon


DEVPKEY_DrvPkg_Icon 设备属性表示 Windows 用于直观表示设备实例的设备图标列表。

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
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>安装应用程序和安装程序的只读访问</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>是</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

列表中的每个图标都通过图标文件 (\*) 或对可执行文件中的图标资源的引用来指定。

将使用列表中的第一个图标作为默认值。 可以提供其他图标来提供设备的不同视觉表示形式。 Windows 包括一个用户界面，该用户界面允许用户选择显示哪个图标窗口。 例如，Microsoft DiscoveryCam 530 以蓝色、绿色和红色提供。 Microsoft 为每种颜色提供了一个图标。 默认情况下，Windows 使用蓝色图标，因为它是列表中的第一个。 但是，Windows 用户也可以选择绿色图标或红色图标。

图标列表是一个以 NULL 分隔的图标说明符列表。 图标说明符可以是图标文件的路径 (\* .ico) 或图标资源说明符，如下所示：

-   图标文件的路径格式为 *DirectoryPath \\ 。*

-   图标资源说明符包含以下项：

    ```cpp
    @executable-file-path,resource-identifier
    ```

    图标资源说明符的第一个字符是 at 符号 ( @ ) ，后跟 (*\* .exe* 或 *\* .dll* 文件) 的可执行文件的路径，后跟逗号分隔符 (、) ，然后是 *资源标识符* 项。

例如，图标说明符 " @shell32.dll ，-30" 表示可执行文件 "shell32.dll" 和资源标识符 "-30"。

资源标识符必须是与可执行文件中的资源对应的整数值，如下所示：

-   如果提供的标识符为负数，则 Windows 将使用其标识符等于提供的标识符的绝对值的可执行文件中的资源。

-   如果提供的标识符为零，Windows 将使用 execuable 文件中其标识符值最低的可执行文件中的资源。

-   如果提供的标识符为正（例如，值为 *n*），则 Windows 将使用该可执行文件中的资源，该文件的标识符为可执行文件中的 n + 1 最小值。 例如，如果 *n* 的值为1，则 Windows 将使用其标识符在可执行文件中的第二个最低值的资源。

可以设置 AddProperty 的 DEVPKEY_DrvPkg_Icon 值，该 [**指令**](./inf-addproperty-directive.md) 包含在安装设备的 inf 文件的 [**inf *DDInstall* 部分**](./inf-ddinstall-section.md) 中。 可以通过调用 [**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)来检索 DEVPKEY_DrvPkg_Icon 的值。

下面的示例演示如何使用 INF **AddProperty** 指令为 INF *DDInstall* 部分为 "SampleDDInstallSection" 安装的设备设置 DEVPKEY_DrvPkg_Icon：

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
<td align="left"><p>版本</p></td>
<td align="left"><p>在 Windows Vista 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Devpkey (包含 Devpkey) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**INF AddProperty 指令**](./inf-addproperty-directive.md)

[**INF *DDInstall* 部分**](./inf-ddinstall-section.md)

[**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

