---
title: PropVariant 帮助程序
description: V2 传感器驱动程序使用 PropVariant helper 函数操作与传感器关联的 PROPVARIANT 结构。
ms.assetid: 5A5A008A-399F-4464-ADD0-7F2DDACB6D4B
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 673d3c36291d9541ab4b212fee96a22f7212c2eb
ms.sourcegitcommit: d5f54510b9500413dd3084b59cb8869f2f6b13cf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68866771"
---
# <a name="sensor-propvariant-helpers"></a>传感器 PropVariant 帮助器

V2 传感器驱动程序使用 PropVariant helper 函数操作与传感器关联的[PropVariant](https://docs.microsoft.com/windows/win32/api/propidlbase/ns-propidlbase-propvariant)结构。

Helper 函数与传感器设备驱动程序软件接口 (DDSI) 一起使用。

| Helper 函数 | Action | 备注 |
| --- | --- | --- |
| InitPropVariantFromFloat | 初始化[PROPVARIANT](https://docs.microsoft.com/windows/win32/api/propidlbase/ns-propidlbase-propvariant)结构。 | 此函数接收 FLOAT, 然后基于该变量创建并初始化[PROPVARIANT](https://docs.microsoft.com/windows/win32/api/propidlbase/ns-propidlbase-propvariant)结构。 |
| PropKeyFindKeyGetPropVariant | 检索[PROPVARIANT](https://docs.microsoft.com/windows/win32/api/propidlbase/ns-propidlbase-propvariant)结构。 | |
| PropKeyFindKeySetPropVariant | 设置[PROPVARIANT](https://docs.microsoft.com/windows/win32/api/propidlbase/ns-propidlbase-propvariant)结构。 | |
| PropKeyFindKeyGetFileTime | 检索与数据文件关联的时间戳。 |这是与提供的属性键匹配的[PROPVARIANT](https://docs.microsoft.com/windows/win32/api/propidlbase/ns-propidlbase-propvariant)结构的*filetime*成员。 |
| PropKeyFindKeyGetGuid | 检索传感器的 GUID。 | 这是与提供的属性键匹配的[PROPVARIANT](https://docs.microsoft.com/windows/win32/api/propidlbase/ns-propidlbase-propvariant)结构的*puuid*成员。 |
| PropKeyFindKeyGetBool | 从与传感器关联的[PROPVARIANT](https://docs.microsoft.com/windows/win32/api/propidlbase/ns-propidlbase-propvariant)结构检索一个 BOOL 值。 | |
| PropKeyFindKeyGetUlong | 从与传感器关联的[PROPVARIANT](https://docs.microsoft.com/windows/win32/api/propidlbase/ns-propidlbase-propvariant)结构检索 ULONG 值。 | |
| PropKeyFindKeyGetUshort | 从与传感器关联的[PROPVARIANT](https://docs.microsoft.com/windows/win32/api/propidlbase/ns-propidlbase-propvariant)结构检索 USHORT 值。 | |
| PropKeyFindKeyGetFloat | 从与传感器关联的[PROPVARIANT](https://docs.microsoft.com/windows/win32/api/propidlbase/ns-propidlbase-propvariant)结构中检索 FLOAT 值。 | |
| PropKeyFindKeyGetDouble | 从与传感器关联的[PROPVARIANT](https://docs.microsoft.com/windows/win32/api/propidlbase/ns-propidlbase-propvariant)结构检索双精度值。 | |
| PropKeyFindKeyGetInt32 | 从与传感器关联的[PROPVARIANT](https://docs.microsoft.com/windows/win32/api/propidlbase/ns-propidlbase-propvariant)结构检索32位值。 | |
| PropKeyFindKeyGetInt64 | 从与传感器关联的[PROPVARIANT](https://docs.microsoft.com/windows/win32/api/propidlbase/ns-propidlbase-propvariant)结构检索64位值。 | |
| PropKeyFindKeyGetNthUlong | 从基于提供的属性键的集合列表内的[PROPVARIANT](https://docs.microsoft.com/windows/win32/api/propidlbase/ns-propidlbase-propvariant)中检索第 n 个 ULONG 值。 | |
| PropKeyFindKeyGetNthUshort | 从基于提供的属性键的集合列表内的[PROPVARIANT](https://docs.microsoft.com/windows/win32/api/propidlbase/ns-propidlbase-propvariant)中检索第 n 个 UShort 值。 | |
| PropKeyFindKeyGetNthInt64 | 从基于提供的属性键的集合列表内的[PROPVARIANT](https://docs.microsoft.com/windows/win32/api/propidlbase/ns-propidlbase-propvariant)中检索第 n 个 Int64 值。 | |
| IsKeyPresentInPropertyList | 返回一个 BOOL 值。 | 布尔值指示是否在与传感器关联的[ **\_传感器属性\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_property_list)结构中找到了属性键。|
| IsKeyPresentInCollectionList | 返回一个 BOOL 值。 | 布尔值指示是否在[ **\_传感器集合\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_collection_list)结构中找到了属性键。 与传感器关联的。 |
| IsCollectionListSame | 返回一个 BOOL 值。 | 比较两[**个\_传感器\_集合列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_collection_list)结构以确定它们是否相同。 |
| PropVariantGetInformation | 检索有关与传感器关联的[PROPVARIANT](https://docs.microsoft.com/windows/win32/api/propidlbase/ns-propidlbase-propvariant)结构的大小、偏移量和其他信息。 | |
| PropertiesListCopy | 将信息从源属性列表复制到目标。 | 有关详细信息, 请参阅[ **\_传感器属性\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ns-sensorsdef-sensor_property_list)。 |
|PropertiesListGetFillableCount | 返回某个大小的缓冲区可能包含的元素数。 | |

## <a name="requirements"></a>要求

|                          |                        |
|--------------------------|------------------------|
| 最低受支持的客户端 | Windows 8.1            |
| 最低受支持的服务器 | Windows Server 2012 R2 |
| Header                   | Sensorsutils         |

## <a name="related-topics"></a>相关主题

[封送处理 helper 函数](marshalling-helper-functions.md)
