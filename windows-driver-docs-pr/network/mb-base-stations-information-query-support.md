---
title: MB 基站信息查询支持
description: MB 基站信息查询支持
ms.assetid: 200954a6-0f6c-4c00-86cb-510399f7b713
keywords:
- MB 基站配合信息查询中，移动宽带基站配合信息查询
ms.date: 08/14/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c11eb0217aadc3e82916e6d95600a37f57705dc
ms.sourcegitcommit: 0504cc497918ebb7b41a205f352046a66c0e26a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2019
ms.locfileid: "65405229"
---
# <a name="mb-base-stations-information-query-support"></a>MB 基站信息查询支持

## <a name="overview"></a>概述

基站信息查询接口用于提供基于位置服务与移动电话的基站信息，例如*基站 ID*，*时间提前*，和其他参数，可以用于计算移动订阅服务器的地理位置。 向移动电话的基站当前为订阅服务器上，提供服务，以及相邻手机基站有关收集的信息。 

本主题定义为 Windows，基站信息查询接口，如 MBIM 1.0 规范不提供此信息通过任何现有的 Cid。 此接口是在 Windows 10，版本 1709年及更高版本中提供。 

通过查询/响应操作检索服务和相邻单元参数。 本主题，以指示已更改的移动电话网络中的设备的位置中也定义通知。

## <a name="mbimcidbasestationsinfo"></a>MBIM_CID_BASE_STATIONS_INFO

此命令检索有关调制解调器到已知的服务及相邻单元格的信息。

服务：**MBB_UUID_BASIC_CONNECT_EXTENSIONS**

服务 UUID:**3d01dcc5-fef5-4d05-0d3a-bef7058e9aaf**

| CID | 命令代码 | 最低操作系统版本 |
| --- | --- | --- |
| MBIM_CID_BASE_STATIONS_INFO | 11 | Windows 10 版本 1709 |

### <a name="parameters"></a>Parameters

| | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| Command | 不适用 | MBIM_BASE_STATIONS_INFO_REQ | 不适用 |
| 响应 | 不 appliable | MBIM_BASE_STATIONS_INFO | 不适用 |

### <a name="query"></a>查询

MBIM_COMMAND_MSG InformationBuffer 包含 MBIM_BASE_STATIONS_INFO_REQ struture。 MBIM_COMMAND_DONE InformationBuffer 包含 MBIM_BASE_STATIONS_INFO 结构。

#### <a name="mbimbasestationsinforeq"></a>MBIM_BASE_STATIONS_INFO_REQ

MBIM_BASE_STATIONS_INFO_REQ 结构应为查询使用在 InformationBuffer 中。 它用于配置方面的单元格信息，如相邻单元格度量，若要在响应中发送的最大数目。 

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | MaxGSMCount | 大小 | 中的 GSM 网络测量报告返回 GSM 相邻单元格的最大项数[MBIM_GSM_NMR](#mbim_gsm_nmr)。 默认的容量为 15。 |
| 4 | 4 | MaxUMTSCount | 大小 | UMTS 测量结果列表中返回的 UMTS 相邻单元格的最大项数[MBIM_UMTS_MRL](#mbim_umts_mrl)。 默认的容量为 15。 |
| 8 | 4 | MaxTDSCDMACount | 大小 | TDSCDMA 测量结果列表中返回的 TDSCDMA 相邻单元格的最大项数[MBIM_TDSCDMA_MRL](#mbim_tdscdma_mrl)。 默认的容量为 15。 |
| 12 | 4 | MaxLTECount | 大小 | 在 LTE 测量结果列表中返回的 LTE 相邻单元格的最大项数[MBIM_LTE_MRL](#mbim_lte_mrl)。 默认的容量为 15。 |
| 16 | 4 | MaxCDMACount | 大小 | CDMA 测量结果列表中返回 CDMA 单元格的最大项数[MBIM_CDMA_MRL](#mbim_cdma_mrl)。 此列表包括为提供服务和相邻单元格。 默认的容量为 12。 |

### <a name="set"></a>设置

不适用。

### <a name="response"></a>响应

MBIM_BASE_STATIONS_INFO 结构应为响应在 MBIM_COMMAND_DONE InformationBuffer 中使用。

#### <a name="mbimbasestationsinfo"></a>MBIM_BASE_STATIONS_INFO

MBIM_BASE_STATIONS_INFO 结构包含关于服务和相邻的基站的信息。

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | SystemType | MBIM_DATA_CLASS | 指示单元格的信息对于哪些服务是有效的系统类型 （或类型）。 此成员是一个或多个系统类型 MBIM_DATA_CLASS 中定义的位掩码。 |
| 4 | 4 | GSMServingCellOffset | 偏移量 | 以字节为单位，计算从此结构的开头到包含 GSM 提供单元格的信息的缓冲区偏移量。 为单元格的技术不 GSM 时，此成员可以为 NULL。 |
| 8 | 4 | GSMServingCellSize | SIZE(0-44) | 大小 （字节），用于[MBIM_GSM_SERVING_CELL_INFO](#mbim_gsm_serving_cell_info)。 |
| 12 | 4 | UMTSServingCellOffset | 偏移量 | 以字节为单位，计算从此结构的开头到包含 UMTS 提供单元格的信息的缓冲区偏移量。 为单元格提供服务的技术不 UMTS 时，此成员可以为 NULL。 |
| 16 | 4 | UMTSServingCellSize | SIZE(0-60) | 大小 （字节），用于[MBIM_UMTS_SERVING_CELL_INFO](#mbim_umts_serving_cell_info)。 |
| 20 | 4 | TDSCDMAServingCellOffset | 偏移量 | 以字节为单位，计算从此结构的开头到包含 TDSCDMA 提供单元格的信息的缓冲区偏移量。 为单元格提供服务的技术不 TDSCDMA 时，此成员可以为 NULL。 |
| 24 | 4 | TDSCDMAServingCellSize | SIZE(0-48) | 大小 （字节），用于[MBIM_TDSCDMA_SERVING_CELL_INFO](#mbim_tdscdma_serving_cell_info)。 |
| 28 | 4 | LTEServingCellOffset | 偏移量 | 以字节为单位，计算从此结构的开头到包含 LTE 提供单元格的信息的缓冲区偏移量。 为单元格提供服务的技术不 LTE 时，此成员可以为 NULL。 |
| 32 | 4 | LTEServingCellSize | SIZE(0-48) | 大小 （字节），用于[MBIM_LTE_SERVING_CELL_INFO](#mbim_lte_serving_cell_info)。 |
| 36 | 4 | GSMNmrOffset | 偏移量 | 以字节为单位，计算从此结构的开头到包含 GSM 网络测量报表的缓冲区偏移量。 没有 GSM 相邻网络返回度量报表中时，此成员可以为 NULL。 |
| 40 | 4 | GSMNmrSize | 大小 | 总大小 （字节） 包含的格式的 GSM 网络测量报表的缓冲区[MBIM_GSM_NMR](#mbim_gsm_nmr)。 |
| 44 | 4 | UMTSMrlOffset | 偏移量 | 此结构的开头的偏移量以字节为单位计算的缓冲区包含 UMTS 测量结果列表。 没有 UMTS 相邻网络返回度量报表中时，此成员可以为 NULL。 |
| 48 | 4 | UMTSMrlSize | 大小 | 总大小，以字节为单位的缓冲区，其中包含 UMTS 测量结果列表中的格式[MBIM_UMTS_MRL](#mbim_umts_mrl)。 |
| 52 | 4 | TDSCDMAMrlOffset | 偏移量 | 此结构的开头的偏移量以字节为单位计算的缓冲区包含 TDSCDMA 测量结果列表。 没有 TDSCDMA 相邻网络返回度量报表中时，此成员可以为 NULL。 |
| 56 | 4 | TDSCDMAMrlSize | 大小 | 总大小，以字节为单位的缓冲区，其中包含 TDSCDMA 测量结果列表中的格式[MBIM_TDSCDMA_MRL](#mbim_tdscdma_mrl)。 |
| 60 | 4 | LTEMrlOffset | 偏移量 | 此结构的开头的偏移量以字节为单位计算的缓冲区包含 LTE 测量结果列表。 没有 LTE 相邻网络返回度量报表中时，此成员可以为 NULL。 |
| 64 | 4 | LTEMrlSize | 大小 | 总大小，以字节为单位的缓冲区，其中包含 LTE 测量结果列表中的格式[MBIM_LTE_MRL](#mbim_lte_mrl)。 |
| 68 | 4 | CDMAMrlOffset | 偏移量 | 此结构的开头的偏移量以字节为单位计算的缓冲区包含 CDMA 测量结果列表。 没有 CDMA 相邻网络返回度量报表中时，此成员可以为 NULL。 |
| 72 | 4 | CDMAMrlSize | 大小 | 总大小，以字节为单位，包含 CDMA 的缓冲区的测量结果列表中的格式[MBIM_CDMA_MRL](#mbim_cdma_mrl)。 |
| 76 |   | DataBuffer | DATABUFFER | 包含的数据缓冲区*GSMServingCell*， *UMTSServingCell*， *TDSCDMAServingCell*， *LTEServingCell*， *GSMNmr*， *UMTSMrl*， *TDSCDMAMrl*， *LTEMrl*，并*CDMAMrl*。 |

#### <a name="gsm-cell-data-structures"></a>GSM 单元格数据结构

##### <a name="mbimgsmservingcellinfo"></a>MBIM_GSM_SERVING_CELL_INFO

MBIM_GSM_SERVING_CELL_INFO 结构包含 GSM 服务单元的相关信息。

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ProviderIdOffset | 偏移量 | 以字节为单位，偏移量计算从此结构的开头到名为的数字 (0-9) 字符串*ProviderId*表示网络提供程序标识。 此字符串将是串联的三位移动国家/地区代码 (MCC) 和两个或三位移动网络代码 （mnc 是否）。 此成员可以为 NULL 时无*ProviderId*返回的信息。 |
| 4 | 4 | ProviderIdSize | SIZE(0-12) | 用于的大小*ProviderId*。 |
| 8 | 4 | LocationAreaCode | UINT32 | 位置区域代码 (0-65535)。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 12 | 4 | CellID | UINT32 | 单元格 ID (0-65535)。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 16 | 4 | TimingAdvance | UINT32 | 在位段，其中一位段是 48/13µs 计时提前 (0-255)。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 20 | 4 | ARFCN | UINT32 | 为单元格 （0-1023 个字符） 的绝对射频频道号。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 24 | 4 | BaseStationId | UINT32 | 基站 ID-基站颜色代码和网络标识代码。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 28 | 4 | RxLevel | UINT32 | 服务接收到的信号强度的单元格 （0 到 63 个） 其中 <p>`X = 0, if RSS < -110 dBm`</p><p>`X = 63, if RSS > -47 dBm`</p><p>`X = integer [RSS + 110], if -110 <= RSS <= -47`</p> 此信息不可用时，请使用 0xFFFFFFFF。 |
| 32 |   | DataBuffer | DATABUFFER | 包含的数据缓冲区*ProviderId*。 |

##### <a name="mbimgsmnmr"></a>MBIM_GSM_NMR

MBIM_GSM_NMR 结构包含相邻单元格内 GSM 网络度量报表 (NMR)。

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ElementCount (EC) | UINT32 | 此元素的 NMR 条目的计数。 |
| 4 |   | DataBuffer | DATABUFFER | NMR 的数组，记录每个记录指定为[MBIM_GSM_NMR_INFO](#mbim_gsm_nmr_info)结构。 |

##### <a name="mbimgsmnmrinfo"></a>MBIM_GSM_NMR_INFO

MBIM_GSM_NMR_INFO 结构包含相邻 GSM 单元的相关信息。

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ProviderIdOffset | 偏移量 | 以字节为单位，偏移量计算从此结构的开头到名为的数字 (0-9) 字符串*ProviderId*表示网络提供程序标识。 此字符串将是串联的三位移动国家/地区代码 (MCC) 和两个或三位移动网络代码 （mnc 是否）。 此成员可以为 NULL 时无*ProviderId*返回的信息。 |
| 4 | 4 | ProviderIdSize | SIZE(0-12) | 用于的大小*ProviderId*。 |
| 8 | 4 | LocationAreaCode | UINT32 | 位置区域代码 (0-65535)。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 12 | 4 | CellID | UINT32 | 单元格 ID (0-65535)。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 16 | 4 | ARFCN | UINT32 | 为单元格 （0-1023 个字符） 的绝对射频频道号。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 20 | 4 | BaseStationId | UINT32 | 为单元格 （0 到 63 个） 单选基站 ID。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 24 | 4 | RxLevel | UINT32 | 服务接收到的信号强度的单元格 （0 到 63 个） 其中 <p>`X = 0, if RSS < -110 dBm`</p><p>`X = 63, if RSS > -47 dBm`</p><p>`X = integer [RSS + 110], if -110 <= RSS <= -47`</p> 此信息不可用时，请使用 0xFFFFFFFF。 |
| 28 |   | DataBuffer | DATABUFFER | 包含的数据缓冲区*ProviderId*。 |

#### <a name="umts-cell-data-structures"></a>UMTS 单元格数据结构

##### <a name="mbimumtsservingcellinfo"></a>MBIM_UMTS_SERVING_CELL_INFO

MBIM_UMTS_SERVING_CELL_INFO 结构包含 UMTS 服务单元的相关信息。

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ProviderIdOffset | 偏移量 | 以字节为单位，偏移量计算从此结构的开头到名为的数字 (0-9) 字符串*ProviderId*表示网络提供程序标识。 此字符串将是串联的三位移动国家/地区代码 (MCC) 和两个或三位移动网络代码 （mnc 是否）。 此成员可以为 NULL 时无*ProviderId*返回的信息。 |
| 4 | 4 | ProviderIdSize | SIZE(0-12) | 用于的大小*ProviderId*。 |
| 8 | 4 | LocationAreaCode | UINT32 | 位置区域代码 (0-65535)。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 12 | 4 | CellID | UINT32 | 单元格 ID (0-268435455) 中。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 16 | 4 | FrequencyInfoUL | UINT32 | 频率信息上行 (0-16383)。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 20 | 4 | FrequencyInfoDL | UINT32 | 频率信息下行 (0-16383)。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 24 | 4 | FrequencyInfoNT | UINT32 | TDD (0-16383) 频率信息。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 28 | 4 | UARFCN | UINT32 | UTRA 绝对射频频道号为单元格 (0-16383)。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 32 | 4 | PrimaryScramblingCode | UINT32 | 主要在混合代码提供单元格 (0-511)。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 36 | 4 | RSCP | INT32 | 接收到信号代码的强大功能提供单元格。 范围是-120-25，1dBm 为单位。 此信息不可用时，请使用 0。 |
| 40 | 4 | ECNO | INT32 | 为单元格; 的信噪比信号每个接收的总 CPICH 的 PN 芯片接收到的能源比率。 范围为-50 英尺至 0，1dBm 为单位。 此信息不可用时，请使用 1。 |
| 44 | 4 | PathLoss | UINT32 | 为单元格 (第 46 173) 路径丢失。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 48 |   | DataBuffer | DATABUFFER | 包含的数据缓冲区*ProviderId*。 |

##### <a name="mbimumtsmrl"></a>MBIM_UMTS_MRL

MBIM_UMTS_MRL 结构包含 UMTS 的相邻单元格的测量的结果列表 (MRL)。

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ElementCount (EC) | UINT32 | 此元素的 MRL 条目的计数。 |
| 4 |   | DataBuffer | DATABUFFER | MRL 的数组，记录每个记录指定为[MBIM_UMTS_MRL_INFO](#mbim_gsm_nmr_info)结构。 |

##### <a name="mbimumtsmrlinfo"></a>MBIM_UMTS_MRL_INFO

MBIM_UMTS_MRL_INFO 结构包含相邻 UMTS 单元的相关信息。

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ProviderIdOffset | 偏移量 | 以字节为单位，偏移量计算从此结构的开头到名为的数字 (0-9) 字符串*ProviderId*表示网络提供程序标识。 此字符串将是串联的三位移动国家/地区代码 (MCC) 和两个或三位移动网络代码 （mnc 是否）。 此成员可以为 NULL 时无*ProviderId*返回的信息。 |
| 4 | 4 | ProviderIdSize | SIZE(0-12) | 用于的大小*ProviderId*。 |
| 8 | 4 | LocationAreaCode | UINT32 | 位置区域代码 (0-65535)。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 12 | 4 | CellID | UINT32 | 单元格 ID (0-268435455) 中。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 16 | 4 | UARFCN | UINT32 | UTRA 绝对射频频道号为单元格 (0-16383)。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 20 | 4 | PrimaryScramblingCode | UINT32 | 主要在混合代码提供单元格 (0-511)。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 24 | 4 | RSCP | INT32 | 接收到信号代码的强大功能提供单元格。 范围是-120-25，1dBm 为单位。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 28 | 4 | ECNO | INT32 | 为单元格; 的信噪比信号每个接收的总 CPICH 的 PN 芯片接收到的能源比率。 范围为-50 英尺至 0，1dBm 为单位。 此信息不可用时，请使用 1。 |
| 32 | 4 | PathLoss | UINT32 | 为单元格 (第 46 173) 路径丢失。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 36 |   | DataBuffer | DATABUFFER | 包含的数据缓冲区*ProviderId*。 |

#### <a name="tdscdma-cell-data-structures"></a>TDSCDMA 单元格数据结构

##### <a name="mbimtdscdmaservingcellinfo"></a>MBIM_TDSCDMA_SERVING_CELL_INFO

MBIM_TDSCDMA_SERVING_CELL_INFO 结构包含 TDSCDMA 服务单元的相关信息。

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ProviderIdOffset | 偏移量 | 以字节为单位，偏移量计算从此结构的开头到名为的数字 (0-9) 字符串*ProviderId*表示网络提供程序标识。 此字符串将是串联的三位移动国家/地区代码 (MCC) 和两个或三位移动网络代码 （mnc 是否）。 此成员可以为 NULL 时无*ProviderId*返回的信息。 |
| 4 | 4 | ProviderIdSize | SIZE(0-12) | 用于的大小*ProviderId*。 |
| 8 | 4 | LocationAreaCode | UINT32 | 位置区域代码 (0-65535)。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 12 | 4 | CellID | UINT32 | 单元格 ID (0-268435455) 中。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 16 | 4 | UARFCN | UINT32 | UTRA 绝对射频频道号为单元格 (0-16383)。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 20 | 4 | CellParameterID | UINT32 | 单元格参数 ID (0-127)。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 24 | 4 | TimingAdvance | UINT32 | 计时提前 （0-1023 个字符）。 此成员是所有的时间段的相同值。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 28 | 4 | RSCP | INT32 | 接收到信号代码的强大功能提供单元格。 范围是-120-25，1dBm 中问题 8 L3 筛选为单位。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 32 | 4 | PathLoss | UINT32 | 为单元格 (第 46 158) 路径丢失。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 36 |   | DataBuffer | DATABUFFER | 包含的数据缓冲区*ProviderId*。 |

##### <a name="mbimtdscdmamrl"></a>MBIM_TDSCDMA_MRL

MBIM_TDSCDMA_MRL 结构包含 TDSCDMA 的相邻单元格的测量的结果列表 (MRL)。

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ElementCount (EC) | UINT32 | 此元素的 MRL 条目的计数。 |
| 4 |   | DataBuffer | DATABUFFER | MRL 的数组，记录每个记录指定为[MBIM_TDSCDMA_MRL_INFO](#mbim_tdscdma_mrl_info)结构。 |

##### <a name="mbimtdscdmamrlinfo"></a>MBIM_TDSCDMA_MRL_INFO

MBIM_TDSCDMA_MRL_INFO 结构包含相邻 TDSCDMA 单元的相关信息。

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ProviderIdOffset | 偏移量 | 以字节为单位，偏移量计算从此结构的开头到名为的数字 (0-9) 字符串*ProviderId*表示网络提供程序标识。 此字符串将是串联的三位移动国家/地区代码 (MCC) 和两个或三位移动网络代码 （mnc 是否）。 此成员可以为 NULL 时无*ProviderId*返回的信息。 |
| 4 | 4 | ProviderIdSize | SIZE(0-12) | 用于的大小*ProviderId*。 |
| 8 | 4 | LocationAreaCode | UINT32 | 位置区域代码 (0-65535)。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 12 | 4 | CellID | UINT32 | 单元格 ID (0-268435455) 中。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 16 | 4 | UARFCN | UINT32 | UTRA 绝对射频频道号为单元格 (0-16383)。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 20 | 4 | CellParameterID | UINT32 | 单元格参数 ID (0-127)。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 24 | 4 | TimingAdvance | UINT32 | 计时提前 （0-1023 个字符）。 此成员是所有的时间段的相同值。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 28 | 4 | RSCP | INT32 | 接收到信号代码的强大功能提供单元格。 范围是-120-25，1dBm 中问题 8 L3 筛选为单位。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 32 | 4 | PathLoss | UINT32 | 为单元格 (第 46 158) 路径丢失。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 36 |   | DataBuffer | DATABUFFER | 包含的数据缓冲区*ProviderId*。 |

#### <a name="lte-cell-data-structures"></a>LTE 单元格数据结构

##### <a name="mbimlteservingcellinfo"></a>MBIM_LTE_SERVING_CELL_INFO

MBIM_LTE_SERVING_CELL_INFO 结构包含 LTE 服务单元的相关信息。

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ProviderIdOffset | 偏移量 | 以字节为单位，偏移量计算从此结构的开头到名为的数字 (0-9) 字符串*ProviderId*表示网络提供程序标识。 此字符串将是串联的三位移动国家/地区代码 (MCC) 和两个或三位移动网络代码 （mnc 是否）。 此成员可以为 NULL 时无*ProviderId*返回的信息。 |
| 4 | 4 | ProviderIdSize | SIZE(0-12) | 用于的大小*ProviderId*。 |
| 8 | 4 | CellID | UINT32 | 单元格 ID (0-268435455) 中。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 12 | 4 | EARFCN | UINT32 | 射频通道数为单元格 (0-65535)。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 16 | 4 | PhysicalCellID | UINT32 | 物理单元 ID (0-503) 中。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 20 | 4 | TAC | UINT32 | 跟踪区域代码 (0-65535)。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 24 | 4 | RSRP | INT32 | 平均参考信号收到电源。 范围是-44，1dBm 为单位的-140。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 28 | 4 | RSRQ | INT32 | 平均参考信号收到质量。 范围为-20 到-3，1dBm 为单位。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 32 | 4 | TimingAdvance | UINT32 | 计时提前 (0-255)。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 36 |   | DataBuffer | DATABUFFER | 包含的数据缓冲区*ProviderId*。 |

##### <a name="mbimltemrl"></a>MBIM_LTE_MRL

MBIM_LTE_MRL 结构包含 LTE 的相邻单元格的测量的结果列表 (MRL)。

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ElementCount (EC) | UINT32 | 此元素的 MRL 条目的计数。 |
| 4 |   | DataBuffer | DATABUFFER | MRL 的数组，记录每个记录指定为[MBIM_LTE_MRL_INFO](#mbim_lte_mrl_info)结构。 |

##### <a name="mbimltemrlinfo"></a>MBIM_LTE_MRL_INFO

MBIM_LTE_MRL_INFO 结构包含相邻 LTE 单元的相关信息。

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ProviderIdOffset | 偏移量 | 以字节为单位，偏移量计算从此结构的开头到名为的数字 (0-9) 字符串*ProviderId*表示网络提供程序标识。 此字符串将是串联的三位移动国家/地区代码 (MCC) 和两个或三位移动网络代码 （mnc 是否）。 此成员可以为 NULL 时无*ProviderId*返回的信息。 |
| 4 | 4 | ProviderIdSize | SIZE(0-12) | 用于的大小*ProviderId*。 |
| 8 | 4 | CellID | UINT32 | 单元格 ID (0-268435455) 中。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 12 | 4 | EARFCN | UINT32 | 射频通道数为单元格 (0-65535)。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 16 | 4 | PhysicalCellID | UINT32 | 物理单元 ID (0-503) 中。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 20 | 4 | TAC | UINT32 | 跟踪区域代码 (0-65535)。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 24 | 4 | RSRP | INT32 | 平均参考信号收到电源。 范围是-44，1dBm 为单位的-140。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 28 | 4 | RSRQ | INT32 | 平均参考信号收到质量。 范围为-20 到-3，1dBm 为单位。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 32 |   | DataBuffer | DATABUFFER | 包含的数据缓冲区*ProviderId*。 |

#### <a name="cdma-cell-data-structures"></a>CDMA 单元格数据结构

##### <a name="mbimcdmamrl"></a>MBIM_CDMA_MRL

MBIM_CDMA_MRL 结构包含为提供服务和相邻 CDMA 单元格的测量的结果列表 (MRL)。

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ElementCount (EC) | UINT32 | 此元素的 MRL 条目的计数。 |
| 4 |   | DataBuffer | DATABUFFER | MRL 的数组，记录每个记录指定为[MBIM_CDMA_MRL_INFO](#mbim_cdma_mrl_info)结构。 |

##### <a name="mbimcdmamrlinfo"></a>MBIM_CDMA_MRL_INFO

MBIM_CDMA_MRL_INFO 数据结构专为 CDMA2000 网络类型。 在同一时间可以有多个 CDMA2000 为单元格。 为提供服务的单元格和相邻单元格都将返回相同的列表中。 **ServingCellFlag**字段指示单元格是否为单元格。

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ServingCellFlag | UINT32 | 指示这是否为单元格。 值为 1 表示为一个单元格，而值为 0 表示相邻的单元格。 （值得注意的是在呼叫时），一次可能有多个服务单元格。 |
| 4 | 4 | NID | UINT32 | 网络 ID (0-65535)。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 8 | 4 | SID | UINT32 | 系统 ID (0-32767)。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 12 | 4 | BaseStationId | UINT32 | 基站 ID (0-65535)。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 16 | 4 | BaseLatitude | UINT32 | 基站纬度 (0-4194303) 中。 这是以 DWORD 的低 22 位中的补数表示形式表示的 0.25 秒为单位进行编码。 为有符号值北部纬度为正数。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 20 | 4 | BaseLongitude | UINT32 | 基站经度 (0-8388607) 中。 这是以 DWORD 的低 23 位中的补数表示形式表示的 0.25 秒为单位进行编码。 为有符号的值，东部经度为正数。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 24 | 4 | RefPN | UINT32 | 基站 PN 数 (0-511)。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 28 | 4 | GPSSeconds | UINT32 | GPS 秒或在该时间这来自基站到达。 此信息不可用时，请使用 0xFFFFFFFF。 |
| 32 | 4 | PilotStrength | UINT32 | 试验 （0 到 63 个） 的信号强度。 此信息不可用时，请使用 0xFFFFFFFF。 |

### <a name="unsolicited-event"></a>未经请求的事件

不适用。

### <a name="status-codes"></a>状态代码

此 CID 使用泛型状态代码 (请参阅使用的状态代码中的部分 9.4.5[公共标准，USB MBIM](https://go.microsoft.com/fwlink/p/?linkid=842064))。

## <a name="mbimcidlocationinfostatus"></a>MBIM_CID_LOCATION_INFO_STATUS

此 CID 检索指示设备的位置的移动电话信息的状态。 它还可能用于位置信息发生更改时提供的未经请求的通知。

服务：**MBB_UUID_BASIC_CONNECT_EXTENSIONS**

服务 UUID:**3d01dcc5-fef5-4d05-0d3a-bef7058e9aaf**

| CID | 命令代码 | 最低操作系统版本 |
| --- | --- | --- |
| MBIM_CID_LOCATION_INFO_STATUS | 12 | Windows 10 版本 1709 |

> [!NOTE]
> MBIM_CID_LOCATION_INFO_STATUS 从 Windows 10，版本 1709，开始定义，但当前不支持的操作系统。 调制解调器可以将此命令发送通知，但操作系统当前无法处理它。

### <a name="parameters"></a>Parameters

| | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| Command | 不适用 | 不适用 | 不适用 |
| 响应 | 不 appliable | MBIM_LOCATION_INFO | MBIM_LOCATION_INFO |

### <a name="query"></a>查询

不使用 MBIM_COMMAND_MSG InformationBuffer。 包含的 MBIM_COMMAND_DONE InformationBuffer [MBIM_LOCATION_INFO](#mbim_location_info)结构。

### <a name="set"></a>设置

不适用。

### <a name="response"></a>响应

#### <a name="mbimlocationinfo"></a>MBIM_LOCATION_INFO

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | LocationAreaCode | UINT32 | 当前位置 GSM/UMTS 区域代码。 当前的系统类型不适用时返回 0xFFFFFFFF。 |
| 4 | 4 | TrackingAreaCode | UINT32 | 跟踪当前位置的区号 LTE。 当前的系统类型不适用时返回 0xFFFFFFFF。 |
| 8 | 4 | CellID | UINT32 | 移动电话塔的 ID。 返回 0xFFFFFFFF 时*CellID*不可用。 |

### <a name="unsolicited-events"></a>未经请求的事件

事件 InformationBuffer 包含 MBIM_LOCATION_INFO 结构。

如果发送此事件的值*位置区号*/*跟踪区号*更改为有效的值。 此事件不会发送何时*CellID*更改时，或者当*位置区域代码*/*跟踪区号*变为无效。

### <a name="status-codes"></a>状态代码

此 CID 使用泛型状态代码 (请参阅使用的状态代码中的部分 9.4.5[公共标准，USB MBIM](https://go.microsoft.com/fwlink/p/?linkid=842064))。

## <a name="oidwwanbasestationsinfo"></a>OID_WWAN_BASE_STATIONS_INFO

MBIM_CID_BASE_STATIONS_INFO NDIS 等效项是[OID_WWAN_BASE_STATIONS_INFO](oid-wwan-base-stations-info.md)。

