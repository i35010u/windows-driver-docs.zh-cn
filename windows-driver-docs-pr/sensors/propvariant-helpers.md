---
title: PropVariant 帮助程序
description: V2 传感器驱动程序使用 PropVariant helper 函数操作与传感器关联的 PROPVARIANT 结构。
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6574314b8d664a74ae2f11dd42000869daca9f72
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812263"
---
# <a name="sensor-propvariant-helpers"></a>传感器 PropVariant 帮助器

V2 传感器驱动程序使用 PropVariant helper 函数操作与传感器关联的 [PropVariant](/windows/win32/api/propidlbase/ns-propidlbase-propvariant) 结构。

Helper 函数与传感器设备驱动程序软件接口一起使用 (DDSI) 。

| Helper 函数 | 操作 | 注释 |
| --- | --- | --- |
| InitPropVariantFromFloat | 初始化 [PROPVARIANT](/windows/win32/api/propidlbase/ns-propidlbase-propvariant) 结构。 | 此函数接收 FLOAT，然后基于该变量创建并初始化 [PROPVARIANT](/windows/win32/api/propidlbase/ns-propidlbase-propvariant) 结构。 |
| PropKeyFindKeyGetPropVariant | 检索 [PROPVARIANT](/windows/win32/api/propidlbase/ns-propidlbase-propvariant) 结构。 | |
| PropKeyFindKeySetPropVariant | 设置 [PROPVARIANT](/windows/win32/api/propidlbase/ns-propidlbase-propvariant) 结构。 | |
| PropKeyFindKeyGetFileTime | 检索与数据文件关联的时间戳。 |这是与提供的属性键匹配的 [PROPVARIANT](/windows/win32/api/propidlbase/ns-propidlbase-propvariant)结构的 *filetime* 成员。 |
| PropKeyFindKeyGetGuid | 检索传感器的 GUID。 | 这是与提供的属性键匹配的 [PROPVARIANT](/windows/win32/api/propidlbase/ns-propidlbase-propvariant)结构的 *puuid* 成员。 |
| PropKeyFindKeyGetBool | 从与传感器关联的 [PROPVARIANT](/windows/win32/api/propidlbase/ns-propidlbase-propvariant) 结构检索一个 BOOL 值。 | |
| PropKeyFindKeyGetUlong | 从与传感器关联的 [PROPVARIANT](/windows/win32/api/propidlbase/ns-propidlbase-propvariant) 结构检索 ULONG 值。 | |
| PropKeyFindKeyGetUshort | 从与传感器关联的 [PROPVARIANT](/windows/win32/api/propidlbase/ns-propidlbase-propvariant) 结构检索 USHORT 值。 | |
| PropKeyFindKeyGetFloat | 从与传感器关联的 [PROPVARIANT](/windows/win32/api/propidlbase/ns-propidlbase-propvariant) 结构中检索 FLOAT 值。 | |
| PropKeyFindKeyGetDouble | 从与传感器关联的 [PROPVARIANT](/windows/win32/api/propidlbase/ns-propidlbase-propvariant) 结构检索双精度值。 | |
| PropKeyFindKeyGetInt32 | 从与传感器关联的 [PROPVARIANT](/windows/win32/api/propidlbase/ns-propidlbase-propvariant) 结构检索32位值。 | |
| PropKeyFindKeyGetInt64 | 从与传感器关联的 [PROPVARIANT](/windows/win32/api/propidlbase/ns-propidlbase-propvariant) 结构检索64位值。 | |
| PropKeyFindKeyGetNthUlong | 从基于提供的属性键的集合列表内的 [PROPVARIANT](/windows/win32/api/propidlbase/ns-propidlbase-propvariant) 中检索第 n 个 ULONG 值。 | |
| PropKeyFindKeyGetNthUshort | 从基于提供的属性键的集合列表内的 [PROPVARIANT](/windows/win32/api/propidlbase/ns-propidlbase-propvariant) 中检索第 n 个 UShort 值。 | |
| PropKeyFindKeyGetNthInt64 | 从基于提供的属性键的集合列表内的 [PROPVARIANT](/windows/win32/api/propidlbase/ns-propidlbase-propvariant) 中检索第 n 个 Int64 值。 | |
| IsKeyPresentInPropertyList | 返回一个 BOOL 值。 | 布尔值指示是否在与传感器关联的 [**传感器 \_ 属性 \_ 列表**](/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_property_list) 结构中找到了属性键。|
| IsKeyPresentInCollectionList | 返回一个 BOOL 值。 | 布尔值指示是否在 [**传感器 \_ 集合 \_ 列表**](/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list) 结构中找到了属性键。 与传感器关联的。 |
| IsCollectionListSame | 返回一个 BOOL 值。 | 比较两个 [**传感器 \_ 集合 \_ 列表**](/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_collection_list) 结构以确定它们是否相同。 |
| PropVariantGetInformation | 检索有关与传感器关联的 [PROPVARIANT](/windows/win32/api/propidlbase/ns-propidlbase-propvariant) 结构的大小、偏移量和其他信息。 | |
| PropertiesListCopy | 将信息从源属性列表复制到目标。 | 有关详细信息，请参阅 [**传感器 \_ 属性 \_ 列表**](/windows-hardware/drivers/ddi/sensorsdef/ns-sensorsdef-sensor_property_list) 。 |
|PropertiesListGetFillableCount | 返回某个大小的缓冲区可能包含的元素数。 | |

## <a name="requirements"></a>要求

**支持的最低客户端**： Windows 8。1

**支持的最低服务器**： Windows Server 2012 R2

**标头**： Sensorsutils


## <a name="related-topics"></a>相关主题

[帮助程序函数的封送处理](marshalling-helper-functions.md)
