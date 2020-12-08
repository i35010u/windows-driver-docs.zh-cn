---
title: OID_GEN_SUPPORTED_GUIDS
description: 作为查询，OID_GEN_SUPPORTED_GUIDS OID 请求微型端口驱动程序返回 NDIS_GUID 类型的结构的数组。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_SUPPORTED_GUIDS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: cac99554de401a6eb0494a4f860f8db377fa2760
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825441"
---
# <a name="oid_gen_supported_guids"></a>OID \_ 生成 \_ 支持的 \_ GUID


作为查询，OID 生成 \_ 支持的 \_ \_ guid oid 请求微型端口驱动程序返回类型为 NDIS GUID 的结构的数组 \_ 。

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

数组中的每个结构都指定自定义 GUID (全局唯一标识符) 映射到自定义 OID，或指定为 \_ 微型端口驱动程序通过 [**NdisMIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex) 函数发送的 NDIS 状态的映射。

NDIS \_ GUID 结构定义如下：

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

此结构的成员包含以下信息：

<a href="" id="guid"></a>**Guid.empty**  
指定为微型端口驱动程序定义的自定义 GUID。

<a href="" id="oid"></a>**Oid**  
指定 **Guid** 映射到的自定义 OID。

<a href="" id="status"></a>**状态值**  
指定 \_ **Guid** 映射到的 NDIS 状态。

<a href="" id="size"></a>**规格**  
指定微型端口驱动程序返回的数组中的每个数据项的大小（以字节为单位）。 如果设置了 fNDIS \_ guid \_ ANSI \_ string 或 fNDIS \_ guid \_ NDIS \_ string 标志，则 **Size** 设置为-1。 否则， **size** 指定 GUID 表示的数据项的大小（以字节为单位）。 仅当设置了 fNDIS \_ GUID 数组标志时，才指定此成员 \_ 。

<a href="" id="flags"></a>**随意**  
可以通过 OR 运算符组合以下标志，以指示 GUID 是映射到 OID 还是映射到 NDIS \_ 状态字符串，并指示为 GUID 提供的数据类型：

<a href="" id="fndis-guid-to-oid"></a>fNDIS \_ GUID \_ 到 \_ OID  
指示 NDIS \_ guid 结构将 GUID 映射到 OID。

<a href="" id="fndis-guid-to-status"></a>fNDIS \_ GUID \_ 到 \_ 状态  
指示 NDIS \_ guid 结构将 GUID 映射到 NDIS \_ 状态字符串。

<a href="" id="fndis-guid-ansi-string"></a>fNDIS \_ GUID \_ ANSI \_ 字符串  
指示为 GUID 提供了以 null 结尾的 ANSI 字符串。

<a href="" id="fndis-guid-unicode-string"></a>fNDIS \_ GUID \_ UNICODE \_ 字符串  
指示为 GUID 提供了 Unicode 字符串。

<a href="" id="fndis-guid-array"></a>fNDIS \_ GUID \_ 数组  
指示为 GUID 提供数据项的数组。 指定的 **大小** 指示数组中每个数据项的长度。

<a href="" id="fndis-guid-allow-read"></a>fNDIS \_ GUID \_ 允许 \_ 读取  
如果设置，则表示允许所有用户使用此 GUID 获取信息。

<a href="" id="fndis-guid-allow-write"></a>fNDIS \_ GUID \_ 允许 \_ 写入  
如果设置，则表示允许所有用户使用此 GUID 设置信息。

**注意**  
默认情况下，只有具有管理员权限的用户才能访问微型端口驱动程序提供的自定义 WMI Guid。 如果微型端口驱动程序支持该 GUID 的读取或写入操作，则具有管理员权限的用户始终可以读取或写入自定义 GUID。 设置 fNDIS \_ guid \_ allow \_ READ 和 fNDIS \_ guid \_ 允许 \_ 写入标志允许所有用户访问自定义 GUID。

 

请注意，微型端口驱动程序注册的所有自定义 Guid 必须将 fNDIS \_ guid 设置 \_ 为 \_ OID，或将 fNDIS guid 设置 \_ \_ 为 \_ STATUS， (从不同时设置这两个) 。 所有其他标志可以通过使用 OR 运算符（如果适用）组合在一起。

在下面的示例中，NDIS \_ guid 结构将 GUID 映射到 OID \_ 802 \_ 3 \_ 多播 \_ 列表：

```C++
NDIS_GUID    NdisGuid = {{0x44795701, 0xa61b, 0x11d0, 0x8d, 0xd4,
                          0x00, 0xc0, 0x4f, 0xc3,
                          0x35, 0x8c},
                          OID_802_3_MULTICAST_LIST,
                          6,
                          fNDIS_GUID_TO_OID | fNDIS_GUID_ARRAY};
```

GUID 是 Windows Management Instrumentation (WMI) 用于获取或设置信息的标识符。 NDIS 截获 WMI 发送到 NDIS 驱动程序的 GUID，将 GUID 映射到 OID，并将 OID 发送到该驱动程序。 驱动程序将数据项返回到 NDIS，然后将数据返回到 WMI。

NDIS 还会将 NIC 状态的更改转换为 WMI 识别的 Guid。 当微型端口驱动程序使用 [**NdisMIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex) 函数报告 NIC 状态发生的更改时，ndis 会将 \_ 微型端口驱动程序指示的 ndis 状态转换为 NDIS 发送到 WMI 的 GUID。

如果微型端口驱动程序支持海关 Guid，则它必须支持 OID 生成 \_ \_ 支持的 \_ guid。 此 OID 返回到 NDIS，将自定义 Guid 映射到自定义 Oid 或 NDIS \_ 状态字符串。 使用 OID 生成支持的 guid 查询微型端口驱动程序之后 \_ \_ \_ ，NDIS 会将微型端口驱动程序的自定义 GUID 注册到 WMI。

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
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NdisMIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)

 

