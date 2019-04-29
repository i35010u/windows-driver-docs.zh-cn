---
title: WIA\_DIP\_驱动程序\_版本
description: WIA\_DIP\_驱动程序\_属性包含 WIA 微型驱动程序的当前 DLL 版本的版本。 WIA 服务创建并维护此属性。
ms.assetid: 708d85b0-0daa-40d9-af38-6bf69834750b
keywords:
- WIA_DIP_DRIVER_VERSION 成像设备
topic_type:
- apiref
api_name:
- WIA_DIP_DRIVER_VERSION
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a27cc2cc42768583993ce8c338e7b65834b68f4d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383689"
---
# <a name="wiadipdriverversion"></a>WIA\_DIP\_驱动程序\_版本


WIA\_DIP\_驱动程序\_属性包含 WIA 微型驱动程序的当前 DLL 版本的版本。 WIA 服务创建并维护此属性。

## <span id="ddk_wia_dip_driver_version_si"></span><span id="DDK_WIA_DIP_DRIVER_VERSION_SI"></span>


属性类型：VT\_BSTR

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

如果 WIA 微型驱动程序不提供版本资源，WIA 服务默认情况下提供"0.0.0.0"的值。 应用程序读取 WIA\_DIP\_驱动程序\_版本以确定 WIA 微型驱动程序 DLL 的版本。

**请注意**  从 Windows Vista 开始，通配符 IP 地址 0.0.0.0 不可用。
如果还从 Windows Vista **IPAutoconfigurationEnabled**注册表项设置为值为 0，禁用自动 IP 地址分配，和任何 IP 地址分配。 在这种情况下， **ipconfig**命令行工具将不会显示一个 IP 地址。 如果项设置为非零值，自动分配 IP 地址。 此密钥也可位于注册表中的以下路径：

**HKEY\_本地\_MACHINE\\系统\\当前控件集\\Services\\Tcpip\\参数\\IPAutoconfigurationEnabled**

**HKEY\_本地\_MACHINE\\系统\\当前控件集\\Services\\Tcpip\\参数\\接口\\*GUID*\\IPAutoconfigurationEnabled**

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>在 Microsoft Windows XP 和更高版本操作系统中可用。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





