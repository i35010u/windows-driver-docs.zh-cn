---
title: WIA \_ DIP \_ 驱动程序 \_ 版本
description: WIA \_ DIP \_ 驱动程序 \_ 版本属性包含 wia 微型驱动程序的当前 DLL 版本。 WIA 服务创建并维护此属性。
keywords:
- WIA_DIP_DRIVER_VERSION 图像设备
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
ms.openlocfilehash: 2e058173eee7c06260b3f4fae2949fd7e00e0a3e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824519"
---
# <a name="wia_dip_driver_version"></a>WIA \_ DIP \_ 驱动程序 \_ 版本


WIA \_ DIP \_ 驱动程序 \_ 版本属性包含 wia 微型驱动程序的当前 DLL 版本。 WIA 服务创建并维护此属性。

## <span id="ddk_wia_dip_driver_version_si"></span><span id="DDK_WIA_DIP_DRIVER_VERSION_SI"></span>


属性类型： VT \_ BSTR

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

如果 WIA 微型驱动程序未提供版本资源，WIA 服务会提供值 "0.0.0.0" 作为默认值。 应用程序读取 WIA \_ DIP \_ 驱动程序 \_ 版本以确定 wia 微型驱动程序 DLL 的版本。

**注意**   从 Windows Vista 开始，通配符 IP 地址0.0.0.0 不可用。
此外，从 Windows Vista 开始，如果 **IPAutoconfigurationEnabled** 注册表项设置为值0，将禁用自动 ip 地址分配，并且不分配 ip 地址。 在这种情况下， **ipconfig** 命令行工具不会显示 IP 地址。 如果将密钥设置为非零值，则会自动分配 IP 地址。 此密钥可位于注册表中的以下路径：

**HKEY \_ 本地 \_ 计算机 \\ 系统 \\ 当前控制集 \\ 服务 \\ Tcpip \\ 参数 \\ IPAutoconfigurationEnabled**

**HKEY \_ 本地 \_ 计算机 \\ 系统 \\ 当前控制集 \\ 服务 \\ Tcpip \\ 参数 \\ 接口 \\ *GUID* \\ IPAutoconfigurationEnabled**

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 Microsoft Windows XP 和更高版本的操作系统中可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

 

 





