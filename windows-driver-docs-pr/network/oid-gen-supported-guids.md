---
title: OID_GEN_SUPPORTED_GUIDS
description: 作为查询，OID_GEN_SUPPORTED_GUIDS OID 请求微型端口驱动程序返回 NDIS_GUID 类型的结构的数组。
ms.assetid: 6985727e-50f8-4dbf-b8cd-ce31d49e8294
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_SUPPORTED_GUIDS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d3c119c128f511a4c749aa374a9ef6d85279006d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844602"
---
# <a name="oid_gen_supported_guids"></a>OID\_代\_支持\_GUID


作为查询，OID\_GEN\_支持\_GUID OID 请求微型端口驱动程序返回类型为 NDIS\_GUID 的结构的数组。

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

数组中的每个结构都指定自定义的 GUID （全局唯一标识符）到自定义 OID 的映射，或指定微型端口驱动程序通过[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)函数发送的 NDIS\_状态的映射。

NDIS\_GUID 结构定义如下：

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
指定**Guid**映射到的自定义 OID。

<a href="" id="status"></a>**状态值**  
指定**Guid**映射到的 NDIS\_状态。

<a href="" id="size"></a>**规格**  
指定微型端口驱动程序返回的数组中的每个数据项的大小（以字节为单位）。 如果 fNDIS\_GUID\_ANSI\_STRING 或 fNDIS\_\_GUID，则设置 " **Size** " 设置为-1。 否则， **size**指定 GUID 表示的数据项的大小（以字节为单位）。 仅当设置了 fNDIS\_GUID\_ARRAY 标志时，才指定此成员。

<a href="" id="flags"></a>**随意**  
可以通过 OR 运算符组合下列标志，以指示 GUID 是映射到 OID 还是映射到 NDIS\_状态字符串，并指示为 GUID 提供的数据类型：

<a href="" id="fndis-guid-to-oid"></a>fNDIS\_GUID\_到\_OID  
指示 NDIS\_GUID 结构将 GUID 映射到 OID。

<a href="" id="fndis-guid-to-status"></a>fNDIS\_GUID\_到\_状态  
指示 NDIS\_GUID 结构将 GUID 映射到 NDIS\_状态字符串。

<a href="" id="fndis-guid-ansi-string"></a>fNDIS\_GUID\_ANSI\_字符串  
指示为 GUID 提供了以 null 结尾的 ANSI 字符串。

<a href="" id="fndis-guid-unicode-string"></a>fNDIS\_GUID\_UNICODE\_字符串  
指示为 GUID 提供了 Unicode 字符串。

<a href="" id="fndis-guid-array"></a>fNDIS\_GUID\_数组  
指示为 GUID 提供数据项的数组。 指定的**大小**指示数组中每个数据项的长度。

<a href="" id="fndis-guid-allow-read"></a>fNDIS\_GUID\_允许\_读取  
如果设置，则表示允许所有用户使用此 GUID 获取信息。

<a href="" id="fndis-guid-allow-write"></a>fNDIS\_GUID\_允许\_写入  
如果设置，则表示允许所有用户使用此 GUID 设置信息。

**注意**   默认情况下，只有具有管理员权限的用户才能访问微型端口驱动程序提供的自定义 WMI guid。 如果微型端口驱动程序支持该 GUID 的读取或写入操作，则具有管理员权限的用户始终可以读取或写入自定义 GUID。 将 fNDIS\_GUID\_允许\_READ and fNDIS\_GUID\_允许\_写入标志允许所有用户访问自定义 GUID。

 

请注意，微型端口驱动程序注册的所有自定义 Guid 必须将 fNDIS\_GUID\_设置为\_OID 或 fNDIS\_GUID\_为\_状态（绝不会设置两者）。 所有其他标志可以通过使用 OR 运算符（如果适用）组合在一起。

在下面的示例中，NDIS\_GUID 结构将 GUID 映射到 OID\_802\_3\_多播\_列表：

```C++
NDIS_GUID    NdisGuid = {{0x44795701, 0xa61b, 0x11d0, 0x8d, 0xd4,
                          0x00, 0xc0, 0x4f, 0xc3,
                          0x35, 0x8c},
                          OID_802_3_MULTICAST_LIST,
                          6,
                          fNDIS_GUID_TO_OID | fNDIS_GUID_ARRAY};
```

GUID 是 Windows Management Instrumentation （WMI）用于获取或设置信息的标识符。 NDIS 截获 WMI 发送到 NDIS 驱动程序的 GUID，将 GUID 映射到 OID，并将 OID 发送到该驱动程序。 驱动程序将数据项返回到 NDIS，然后将数据返回到 WMI。

NDIS 还会将 NIC 状态的更改转换为 WMI 识别的 Guid。 当微型端口驱动程序使用[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)函数报告 NIC 状态发生的更改时，ndis 会将微型端口驱动程序指示的 NDIS\_状态转换为 ndis 发送到 WMI 的 GUID。

如果微型端口驱动程序支持海关 Guid，则它必须支持 OID\_\_支持的\_GUID。 此 OID 返回到 NDIS，将自定义 Guid 映射到自定义 Oid 或 NDIS\_状态字符串。 使用 OID 查询微型端口驱动程序后\_生成\_支持\_GUID，NDIS 会将微型端口驱动程序的自定义 Guid 注册到 WMI。

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
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)

 

 




