---
title: OID_GEN_SUPPORTED_GUIDS
description: 为查询，OID_GEN_SUPPORTED_GUIDS OID 请求微型端口驱动程序，以返回类型 NDIS_GUID 的结构数组。
ms.assetid: 6985727e-50f8-4dbf-b8cd-ce31d49e8294
ms.date: 08/08/2017
keywords: -OID_GEN_SUPPORTED_GUIDS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5019d616ab3821d511e391d8d2e5e510d8419084
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526637"
---
# <a name="oidgensupportedguids"></a>OID\_GEN\_支持\_GUID


为查询，OID\_GEN\_支持\_GUID OID 请求微型端口驱动程序，以返回类型 NDIS 的结构数组\_GUID。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
可选。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
可选。

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
可选。

<a name="remarks"></a>备注
-------

数组中的每个结构指定的映射的自定义 GUID （全局唯一标识符） 是一个自定义的 OID 或 NDIS\_微型端口驱动程序将通过发送的状态[ **NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600)函数。

NDIS\_GUID 结构定义，如下所示：

```C++
typedef struct _NDIS_GUID {
    GUID             Guid;
    union {
        NDIS_OID     Oid;
        NDIS_STATUS  Status;
    };
    ULONG            Size;
    ULONG            Flags;
} NDIS_GUID, *PNDIS_GUID;
```

此结构的成员包含下列信息：

<a href="" id="guid"></a>**guid**  
指定为微型端口驱动程序定义的自定义 GUID。

<a href="" id="oid"></a>**oid**  
指定向其自定义 OID **Guid**映射。

<a href="" id="status"></a>**状态**  
指定 NDIS\_状态设置为这**Guid**映射。

<a href="" id="size"></a>**大小**  
以字节为单位的微型端口驱动程序返回的数组中每个数据项中指定的大小。 如果 fNDIS\_GUID\_ANSI\_字符串或 fNDIS\_GUID\_NDIS\_设置字符串标志，则**大小**设置为-1。 否则为**大小**以字节为单位的 GUID 表示的数据项中指定的大小。 指定此成员时，才 fNDIS\_GUID\_数组标志设置。

<a href="" id="flags"></a>**标志**  
可以使用 OR 运算符，以指示 GUID 映射到 OID 或 NDIS 组合以下标志\_状态字符串，还可以指示的 GUID 为提供的数据类型：

<a href="" id="fndis-guid-to-oid"></a>fNDIS\_GUID\_TO\_OID  
指示 NDIS\_GUID 结构映射到 OID 的 GUID。

<a href="" id="fndis-guid-to-status"></a>fNDIS\_GUID\_TO\_状态  
指示 NDIS\_GUID 结构将 GUID 映射到 NDIS\_状态字符串。

<a href="" id="fndis-guid-ansi-string"></a>fNDIS\_GUID\_ANSI\_STRING  
指示以 null 结尾的 ANSI 字符串，提供的 guid。

<a href="" id="fndis-guid-unicode-string"></a>fNDIS\_GUID\_UNICODE\_字符串  
指示 Unicode 字符串，提供的 guid。

<a href="" id="fndis-guid-array"></a>fNDIS\_GUID\_ARRAY  
指示数据项的数组，提供的 guid。 指定**大小**指示数组中每个数据项的长度。

<a href="" id="fndis-guid-allow-read"></a>fNDIS\_GUID\_ALLOW\_READ  
设置时，指示允许所有用户使用此 GUID 来获取信息。

<a href="" id="fndis-guid-allow-write"></a>fNDIS\_GUID\_允许\_编写  
设置时，指示允许所有用户可使用此 GUID 来设置的信息。

**请注意**  默认情况下提供的微型端口驱动程序的自定义 WMI Guid 是仅具有管理员权限的用户可以访问。 具有管理员权限的用户始终可以读取或写入一个自定义 GUID，如果微型端口驱动程序支持读取或写入该 GUID 的操作。 设置 fNDIS\_GUID\_允许\_读取和 fNDIS\_GUID\_允许\_写标志以允许所有用户访问自定义 GUID。

 

请注意，所有自定义 Guid 注册的微型端口驱动程序必须设置任一 fNDIS\_GUID\_TO\_OID 或 fNDIS\_GUID\_TO\_状态 （永远不会同时设置）。 所有其他标志可能会根据使用 OR 运算符组合。

在下面的示例中，NDIS\_GUID 结构将 GUID 映射到 OID\_802\_3\_多播\_列表：

```C++
NDIS_GUID    NdisGuid = {{0x44795701, 0xa61b, 0x11d0, 0x8d, 0xd4,
                          0x00, 0xc0, 0x4f, 0xc3,
                          0x35, 0x8c},
                          OID_802_3_MULTICAST_LIST,
                          6,
                          fNDIS_GUID_TO_OID | fNDIS_GUID_ARRAY};
```

GUID 是通过 Windows Management Instrumentation (WMI) 用于获取或设置信息的标识符。 NDIS 截获由 WMI 发送到 NDIS 驱动程序的 GUID，它将 GUID 映射到 OID，并向驱动程序发送 OID。 驱动程序返回的数据项目到 NDIS，然后将数据返回到 WMI。

NDIS 还将通过 WMI 识别的 Guid 转换为 NIC 状态变化。 微型端口驱动程序中使用 NIC 状态的更改进行报告时[ **NdisMIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563600)函数，NDIS 转换 NDIS\_到 GUID 的 NDIS 所表示的微型端口驱动程序状态将发送到 WMI。

如果微型端口驱动程序支持海关 Guid，它必须支持 OID\_GEN\_支持\_GUID。 此 OID 返回到 NDIS 的自定义 Guid 到自定义 Oid 或 NDIS 映射\_状态字符串。 查询使用 OID 的微型端口驱动程序后\_GEN\_支持\_GUID，NDIS 向 WMI 注册微型端口驱动程序的自定义 Guid。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600)

 

 




