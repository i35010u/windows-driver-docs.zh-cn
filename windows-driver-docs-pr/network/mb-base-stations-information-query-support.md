---
title: MB 基站信息查询支持
description: MB 基站信息查询支持
ms.assetid: 200954a6-0f6c-4c00-86cb-510399f7b713
keywords:
- MB 基站信息查询，移动宽带基站信息查询
ms.date: 08/14/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2af61546eece7a6996d22d7328748442aa32a295
ms.sourcegitcommit: 74a8dc9ef1da03857dec5cab8d304e2869ba54a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90759919"
---
# <a name="mb-base-stations-information-query-support"></a>MB 基站信息查询支持

## <a name="overview"></a>概述

"基站信息查询接口" 用于提供基于位置的服务和蜂窝基站信息，如 *基站 ID*、 *时间提前*和其他可用于计算移动订阅者地理位置的参数。 收集的信息与当前为订阅者提供服务的移动电话基站以及邻居移动基站相关。 

本主题为 Windows 定义了基站信息查询接口，因为 MBIM 1.0 规范不会通过任何现有 Cid 提供此信息。 此接口在 Windows 10 版本1709及更高版本中可用。 

通过查询/响应操作检索服务和邻居单元参数。 本主题中还定义了一个通知，以指示设备在移动电话网络中的位置已更改。

## <a name="mbim_cid_base_stations_info"></a><a name="mbim_cid_base_stations_info"></a>MBIM_CID_BASE_STATIONS_INFO

此命令检索有关调制解调器已知的服务和邻居单元的信息。

服务： **MBB_UUID_BASIC_CONNECT_EXTENSIONS**

服务 UUID： **3d01dcc5-fef5-4d05-0d3a-bef7058e9aaf**

| CID | 命令代码 | 最低操作系统版本 |
| --- | --- | --- |
| MBIM_CID_BASE_STATIONS_INFO | 11 | Windows 10 版本 1709 |

### <a name="parameters"></a>参数

| 类型 | Set | 查询 | 通知 |
| --- | --- | --- | --- |
| 命令 | 不适用 | MBIM_BASE_STATIONS_INFO_REQ | 不适用 |
| 响应 | 不适用 | MBIM_BASE_STATIONS_INFO | 不适用 |

### <a name="query"></a>查询

MBIM_COMMAND_MSG 的 InformationBuffer 包含 MBIM_BASE_STATIONS_INFO_REQ struture。 MBIM_COMMAND_DONE 的 InformationBuffer 包含 MBIM_BASE_STATIONS_INFO 的结构。

#### <a name="mbim_base_stations_info_req"></a><a name="mbim_base_stations_info_req"></a>MBIM_BASE_STATIONS_INFO_REQ

MBIM_BASE_STATIONS_INFO_REQ 结构应在 InformationBuffer for 查询中使用。 它用于配置单元信息的各个方面，如要发送的响应中的邻居单元格度量的最大数目。 

| 偏移量 | 大小 | 字段 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | MaxGSMCount | SIZE | GSM 网络度量报表中返回的 GSM 相邻单元的最大项数 [MBIM_GSM_NMR](#mbim_gsm_nmr)。 默认容量为15。 |
| 4 | 4 | MaxUMTSCount | SIZE | 在 [MBIM_UMTS_MRL](#mbim_umts_mrl)中，在 UMTS 度量结果列表中返回的相邻单元 UMTS 的最大项数。 默认容量为15。 |
| 8 | 4 | MaxTDSCDMACount | SIZE | 在 [MBIM_TDSCDMA_MRL](#mbim_tdscdma_mrl)中，在 TDSCDMA 度量结果列表中返回的相邻单元 TDSCDMA 的最大项数。 默认容量为15。 |
| 12 | 4 | MaxLTECount | SIZE | [MBIM_LTE_MRL](#mbim_lte_mrl)的 lte 度量结果列表中返回的 lte 相邻单元的最大项数。 默认容量为15。 |
| 16 | 4 | MaxCDMACount | SIZE | [MBIM_CDMA_MRL](#mbim_cdma_mrl)中 CDMA 度量结果列表中返回的 CDMA 单元的最大项数。 此列表包括服务和相邻单元。 默认容量为12。 |

### <a name="set"></a>Set

不适用。

### <a name="response"></a>响应

MBIM_BASE_STATIONS_INFO 结构应用于响应的 MBIM_COMMAND_DONE InformationBuffer。

#### <a name="mbim_base_stations_info"></a><a name="mbim_base_stations_info"></a>MBIM_BASE_STATIONS_INFO

MBIM_BASE_STATIONS_INFO 结构包含有关服务和邻居基站的信息。

| 偏移量 | 大小 | 字段 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | SystemType | MBIM_DATA_CLASS | 指示为其提供单元信息的) 的系统类型 (或类型。 此成员是 MBIM_DATA_CLASS 中定义的一个或多个系统类型的位掩码。 |
| 4 | 4 | GSMServingCellOffset | OFFSET | 从该结构的开头计算的偏移量（以字节为单位），到包含 GSM 服务单元信息的缓冲区。 如果服务单元的技术不是 GSM，此成员可能为 NULL。 |
| 8 | 4 | GSMServingCellSize | 大小 (0-44)  | 用于 [MBIM_GSM_SERVING_CELL_INFO](#mbim_gsm_serving_cell_info)的大小（以字节为单位）。 |
| 12 | 4 | UMTSServingCellOffset | OFFSET | 从该结构的开头算起的偏移量（以字节为单位），该偏移量为包含 UMTS 服务单元信息的缓冲区。 当提供服务单元的技术不 UMTS 时，此成员可能为 NULL。 |
| 16 | 4 | UMTSServingCellSize | 大小 (0-60)  | 用于 [MBIM_UMTS_SERVING_CELL_INFO](#mbim_umts_serving_cell_info)的大小（以字节为单位）。 |
| 20 | 4 | TDSCDMAServingCellOffset | OFFSET | 从该结构的开头算起的偏移量（以字节为单位），该偏移量为包含 TDSCDMA 服务单元信息的缓冲区。 当提供服务单元的技术不 TDSCDMA 时，此成员可能为 NULL。 |
| 24 | 4 | TDSCDMAServingCellSize | 大小 (0-48)  | 用于 [MBIM_TDSCDMA_SERVING_CELL_INFO](#mbim_tdscdma_serving_cell_info)的大小（以字节为单位）。 |
| 28 | 4 | LTEServingCellOffset | OFFSET | 从该结构的开头算起的偏移量（以字节为单位），该偏移量为包含用于提供提供服务的单元信息的缓冲区。 如果服务单元的技术不是 LTE，此成员可能为 NULL。 |
| 32 | 4 | LTEServingCellSize | 大小 (0-48)  | 用于 [MBIM_LTE_SERVING_CELL_INFO](#mbim_lte_serving_cell_info)的大小（以字节为单位）。 |
| 36 | 4 | GSMNmrOffset | OFFSET | 从该结构的开头计算的偏移量（以字节为单位），到包含 GSM 网络测量报告的缓冲区。 如果度量值报告中未返回 GSM 相邻网络，此成员可为 NULL。 |
| 40 | 4 | GSMNmrSize | SIZE | 缓冲区的总大小（以字节为单位），该缓冲区包含 GSM 网络测量报告，格式为 [MBIM_GSM_NMR](#mbim_gsm_nmr)。 |
| 44 | 4 | UMTSMrlOffset | OFFSET | 从该结构的开头算起的偏移量（以字节为单位），该偏移量为包含 UMTS 测量结果列表的缓冲区。 如果度量值报告中未返回 UMTS 邻居网络，此成员可为 NULL。 |
| 48 | 4 | UMTSMrlSize | SIZE | 缓冲区的总大小（以字节为单位），该缓冲区包含以 [MBIM_UMTS_MRL](#mbim_umts_mrl)格式表示的 UMTS 度量结果列表。 |
| 52 | 4 | TDSCDMAMrlOffset | OFFSET | 从该结构的开头算起的偏移量（以字节为单位），该偏移量为包含 TDSCDMA 测量结果列表的缓冲区。 如果度量值报告中未返回 TDSCDMA 邻居网络，此成员可为 NULL。 |
| 56 | 4 | TDSCDMAMrlSize | SIZE | 缓冲区的总大小（以字节为单位），该缓冲区包含以 [MBIM_TDSCDMA_MRL](#mbim_tdscdma_mrl)格式表示的 TDSCDMA 度量结果列表。 |
| 60 | 4 | LTEMrlOffset | OFFSET | 从该结构的开头计算的偏移量（以字节为单位），到包含 LTE 度量结果列表的缓冲区。 如果度量值报告中未返回任何 LTE 邻接网络，此成员可能为 NULL。 |
| 64 | 4 | LTEMrlSize | SIZE | 缓冲区的总大小（以字节为单位），该缓冲区包含以 [MBIM_LTE_MRL](#mbim_lte_mrl)格式表示的 LTE 度量结果列表。 |
| 68 | 4 | CDMAMrlOffset | OFFSET | 从该结构的开头算起的偏移量（以字节为单位），该偏移量为包含 CDMA 测量结果列表的缓冲区。 如果度量值报告中未返回 CDMA 邻居网络，此成员可为 NULL。 |
| 72 | 4 | CDMAMrlSize | SIZE | 缓冲区的总大小（以字节为单位），该缓冲区包含以 [MBIM_CDMA_MRL](#mbim_cdma_mrl)格式表示的 CDMA 度量结果列表。 |
| 76 |   | DataBuffer | DATABUFFER | 包含 *GSMServingCell*、 *UMTSServingCell*、 *TDSCDMAServingCell*、 *LTEServingCell*、 *GSMNmr*、 *UMTSMrl*、 *TDSCDMAMrl*、 *LTEMrl*和 *CDMAMrl*的数据缓冲区。 |

#### <a name="gsm-cell-data-structures"></a>GSM 单元数据结构

##### <a name="mbim_gsm_serving_cell_info"></a><a name="mbim_gsm_serving_cell_info"></a>MBIM_GSM_SERVING_CELL_INFO

MBIM_GSM_SERVING_CELL_INFO 结构包含有关 GSM 服务单元的信息。

| 偏移量 | 大小 | 字段 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ProviderIdOffset | OFFSET | 从该结构的开头算起的偏移量（以字节为单位），该偏移量是一个数字 (0-9) 名为 *ProviderId* 的字符串，用于表示网络提供程序标识。 此字符串是三位数 Mobile 国家/地区代码的串联 (MCC) 和两个或三个数字的移动网络代码 (MNC) 。 当没有返回 *ProviderId* 信息时，此成员可能为 NULL。 |
| 4 | 4 | ProviderIdSize | 大小 (0-12)  | 用于 *ProviderId*的大小。 |
| 8 | 4 | LocationAreaCode | UINT32 | 位置区代码 (0-65535) 。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 12 | 4 | CellID | UINT32 | 单元 ID (0-65535) 。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 16 | 4 | TimingAdvance | UINT32 | 计时提前 (0-255) 位，其中位句点是 48/13μs。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 20 | 4 | ARFCN | UINT32 | 服务单元 (0-1023) 的绝对射频通道号。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 24 | 4 | BaseStationId | UINT32 | 基站 ID-基站颜色代码和网络标识代码。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 28 | 4 | RxLevel | UINT32 | 所接收的服务单元的信号强度 (0-63) ，其中 <p>`X = 0, if RSS < -110 dBm`</p><p>`X = 63, if RSS > -47 dBm`</p><p>`X = integer [RSS + 110], if -110 <= RSS <= -47`</p> 如果此信息不可用，则使用0xFFFFFFFF。 |
| 32 |   | DataBuffer | DATABUFFER | 包含 *ProviderId*的数据缓冲区。 |

##### <a name="mbim_gsm_nmr"></a><a name="mbim_gsm_nmr"></a>MBIM_GSM_NMR

MBIM_GSM_NMR 结构包含相邻 GSM 单元 (NMR) 的网络度量报表。

| 偏移量 | 大小 | 字段 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | Elementcount 多于 (EC)  | UINT32 | 此元素后面的 NMR 项的计数。 |
| 4 |   | DataBuffer | DATABUFFER | NMR 记录的数组，每个记录都指定为 [MBIM_GSM_NMR_INFO](#mbim_gsm_nmr_info) 结构。 |

##### <a name="mbim_gsm_nmr_info"></a><a name="mbim_gsm_nmr_info"></a>MBIM_GSM_NMR_INFO

MBIM_GSM_NMR_INFO 结构包含有关相邻 GSM 单元的信息。

| 偏移量 | 大小 | 字段 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ProviderIdOffset | OFFSET | 从该结构的开头算起的偏移量（以字节为单位），该偏移量是一个数字 (0-9) 名为 *ProviderId* 的字符串，用于表示网络提供程序标识。 此字符串是三位数 Mobile 国家/地区代码的串联 (MCC) 和两个或三个数字的移动网络代码 (MNC) 。 当没有返回 *ProviderId* 信息时，此成员可能为 NULL。 |
| 4 | 4 | ProviderIdSize | 大小 (0-12)  | 用于 *ProviderId*的大小。 |
| 8 | 4 | LocationAreaCode | UINT32 | 位置区代码 (0-65535) 。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 12 | 4 | CellID | UINT32 | 单元 ID (0-65535) 。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 16 | 4 | ARFCN | UINT32 | 服务单元 (0-1023) 的绝对射频通道号。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 20 | 4 | BaseStationId | UINT32 | 服务单元的收音机基站 ID (0-63) 。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 24 | 4 | RxLevel | UINT32 | 所接收的服务单元的信号强度 (0-63) ，其中 <p>`X = 0, if RSS < -110 dBm`</p><p>`X = 63, if RSS > -47 dBm`</p><p>`X = integer [RSS + 110], if -110 <= RSS <= -47`</p> 如果此信息不可用，则使用0xFFFFFFFF。 |
| 28 |   | DataBuffer | DATABUFFER | 包含 *ProviderId*的数据缓冲区。 |

#### <a name="umts-cell-data-structures"></a>UMTS 单元数据结构

##### <a name="mbim_umts_serving_cell_info"></a><a name="mbim_umts_serving_cell_info"></a>MBIM_UMTS_SERVING_CELL_INFO

MBIM_UMTS_SERVING_CELL_INFO 结构包含 UMTS 服务单元的相关信息。

| 偏移量 | 大小 | 字段 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ProviderIdOffset | OFFSET | 从该结构的开头算起的偏移量（以字节为单位），该偏移量是一个数字 (0-9) 名为 *ProviderId* 的字符串，用于表示网络提供程序标识。 此字符串是三位数 Mobile 国家/地区代码的串联 (MCC) 和两个或三个数字的移动网络代码 (MNC) 。 当没有返回 *ProviderId* 信息时，此成员可能为 NULL。 |
| 4 | 4 | ProviderIdSize | 大小 (0-12)  | 用于 *ProviderId*的大小。 |
| 8 | 4 | LocationAreaCode | UINT32 | 位置区代码 (0-65535) 。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 12 | 4 | CellID | UINT32 | 单元 ID (0-268435455) 。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 16 | 4 | FrequencyInfoUL | UINT32 | 频率信息上行 (0-16383) 。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 20 | 4 | FrequencyInfoDL | UINT32 | 频率信息下行 (0-16383) 。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 24 | 4 | FrequencyInfoNT | UINT32 | TDD (0-16383) 的频率信息。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 28 | 4 | UARFCN | UINT32 | 服务单元 (0-16383) 的 UTRA 绝对射频通道号。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 32 | 4 | PrimaryScramblingCode | UINT32 | 服务单元 (0-511) 的主要编码代码。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 36 | 4 | RSCP | INT32 | 为服务单元提供的信号码的幂。 范围为-120 到-25，单位为1dBm。 如果此信息不可用，则使用0。 |
| 40 | 4 | ECNO | INT32 | 服务单元的信噪比的信号;CPICH 的每个 PN 芯片的接收能耗与接收的总数之比。 范围为-50 到0，单位为1dBm。 如果此信息不可用，请使用1。 |
| 44 | 4 | PathLoss | UINT32 | 服务单元 (46-173) 的路径丢失。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 48 |   | DataBuffer | DATABUFFER | 包含 *ProviderId*的数据缓冲区。 |

##### <a name="mbim_umts_mrl"></a><a name="mbim_umts_mrl"></a>MBIM_UMTS_MRL

MBIM_UMTS_MRL 结构包含邻近 UMTS 单元 (MRL) 的已测量结果列表。

| 偏移量 | 大小 | 字段 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | Elementcount 多于 (EC)  | UINT32 | 此元素后面的 MRL 项的计数。 |
| 4 |   | DataBuffer | DATABUFFER | MRL 记录的数组，每个记录都指定为 [MBIM_UMTS_MRL_INFO](#mbim_gsm_nmr_info) 结构。 |

##### <a name="mbim_umts_mrl_info"></a><a name="mbim_umts_mrl_info"></a>MBIM_UMTS_MRL_INFO

MBIM_UMTS_MRL_INFO 结构包含有关相邻 UMTS 单元格的信息。

| 偏移量 | 大小 | 字段 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ProviderIdOffset | OFFSET | 从该结构的开头算起的偏移量（以字节为单位），该偏移量是一个数字 (0-9) 名为 *ProviderId* 的字符串，用于表示网络提供程序标识。 此字符串是三位数 Mobile 国家/地区代码的串联 (MCC) 和两个或三个数字的移动网络代码 (MNC) 。 当没有返回 *ProviderId* 信息时，此成员可能为 NULL。 |
| 4 | 4 | ProviderIdSize | 大小 (0-12)  | 用于 *ProviderId*的大小。 |
| 8 | 4 | LocationAreaCode | UINT32 | 位置区代码 (0-65535) 。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 12 | 4 | CellID | UINT32 | 单元 ID (0-268435455) 。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 16 | 4 | UARFCN | UINT32 | 服务单元 (0-16383) 的 UTRA 绝对射频通道号。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 20 | 4 | PrimaryScramblingCode | UINT32 | 服务单元 (0-511) 的主要编码代码。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 24 | 4 | RSCP | INT32 | 为服务单元提供的信号码的幂。 范围为-120 到-25，单位为1dBm。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 28 | 4 | ECNO | INT32 | 服务单元的信噪比的信号;CPICH 的每个 PN 芯片的接收能耗与接收的总数之比。 范围为-50 到0，单位为1dBm。 如果此信息不可用，请使用1。 |
| 32 | 4 | PathLoss | UINT32 | 服务单元 (46-173) 的路径丢失。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 36 |   | DataBuffer | DATABUFFER | 包含 *ProviderId*的数据缓冲区。 |

#### <a name="tdscdma-cell-data-structures"></a>TDSCDMA 单元数据结构

##### <a name="mbim_tdscdma_serving_cell_info"></a><a name="mbim_tdscdma_serving_cell_info"></a>MBIM_TDSCDMA_SERVING_CELL_INFO

MBIM_TDSCDMA_SERVING_CELL_INFO 结构包含 TDSCDMA 服务单元的相关信息。

| 偏移量 | 大小 | 字段 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ProviderIdOffset | OFFSET | 从该结构的开头算起的偏移量（以字节为单位），该偏移量是一个数字 (0-9) 名为 *ProviderId* 的字符串，用于表示网络提供程序标识。 此字符串是三位数 Mobile 国家/地区代码的串联 (MCC) 和两个或三个数字的移动网络代码 (MNC) 。 当没有返回 *ProviderId* 信息时，此成员可能为 NULL。 |
| 4 | 4 | ProviderIdSize | 大小 (0-12)  | 用于 *ProviderId*的大小。 |
| 8 | 4 | LocationAreaCode | UINT32 | 位置区代码 (0-65535) 。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 12 | 4 | CellID | UINT32 | 单元 ID (0-268435455) 。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 16 | 4 | UARFCN | UINT32 | 服务单元 (0-16383) 的 UTRA 绝对射频通道号。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 20 | 4 | CellParameterID | UINT32 | 单元参数 ID (0-127) 。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 24 | 4 | TimingAdvance | UINT32 | 计时提前 (0-1023) 。 对于所有 timeslots，此成员的值都相同。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 28 | 4 | RSCP | INT32 | 为服务单元提供的信号码的幂。 范围为-120 到-25，以1dBm 在问题8中筛选的单位。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 32 | 4 | PathLoss | UINT32 | 服务单元 (46-158) 的路径丢失。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 36 |   | DataBuffer | DATABUFFER | 包含 *ProviderId*的数据缓冲区。 |

##### <a name="mbim_tdscdma_mrl"></a><a name="mbim_tdscdma_mrl"></a>MBIM_TDSCDMA_MRL

MBIM_TDSCDMA_MRL 结构包含邻近 TDSCDMA 单元 (MRL) 的已测量结果列表。

| 偏移量 | 大小 | 字段 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | Elementcount 多于 (EC)  | UINT32 | 此元素后面的 MRL 项的计数。 |
| 4 |   | DataBuffer | DATABUFFER | MRL 记录的数组，每个记录都指定为 [MBIM_TDSCDMA_MRL_INFO](#mbim_tdscdma_mrl_info) 结构。 |

##### <a name="mbim_tdscdma_mrl_info"></a><a name="mbim_tdscdma_mrl_info"></a>MBIM_TDSCDMA_MRL_INFO

MBIM_TDSCDMA_MRL_INFO 结构包含有关相邻 TDSCDMA 单元格的信息。

| 偏移量 | 大小 | 字段 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ProviderIdOffset | OFFSET | 从该结构的开头算起的偏移量（以字节为单位），该偏移量是一个数字 (0-9) 名为 *ProviderId* 的字符串，用于表示网络提供程序标识。 此字符串是三位数 Mobile 国家/地区代码的串联 (MCC) 和两个或三个数字的移动网络代码 (MNC) 。 当没有返回 *ProviderId* 信息时，此成员可能为 NULL。 |
| 4 | 4 | ProviderIdSize | 大小 (0-12)  | 用于 *ProviderId*的大小。 |
| 8 | 4 | LocationAreaCode | UINT32 | 位置区代码 (0-65535) 。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 12 | 4 | CellID | UINT32 | 单元 ID (0-268435455) 。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 16 | 4 | UARFCN | UINT32 | 服务单元 (0-16383) 的 UTRA 绝对射频通道号。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 20 | 4 | CellParameterID | UINT32 | 单元参数 ID (0-127) 。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 24 | 4 | TimingAdvance | UINT32 | 计时提前 (0-1023) 。 对于所有 timeslots，此成员的值都相同。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 28 | 4 | RSCP | INT32 | 为服务单元提供的信号码的幂。 范围为-120 到-25，以1dBm 在问题8中筛选的单位。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 32 | 4 | PathLoss | UINT32 | 服务单元 (46-158) 的路径丢失。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 36 |   | DataBuffer | DATABUFFER | 包含 *ProviderId*的数据缓冲区。 |

#### <a name="lte-cell-data-structures"></a>LTE 单元数据结构

##### <a name="mbim_lte_serving_cell_info"></a><a name="mbim_lte_serving_cell_info"></a>MBIM_LTE_SERVING_CELL_INFO

MBIM_LTE_SERVING_CELL_INFO 结构包含有关 LTE 服务单元的信息。

| 偏移量 | 大小 | 字段 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ProviderIdOffset | OFFSET | 从该结构的开头算起的偏移量（以字节为单位），该偏移量是一个数字 (0-9) 名为 *ProviderId* 的字符串，用于表示网络提供程序标识。 此字符串是三位数 Mobile 国家/地区代码的串联 (MCC) 和两个或三个数字的移动网络代码 (MNC) 。 当没有返回 *ProviderId* 信息时，此成员可能为 NULL。 |
| 4 | 4 | ProviderIdSize | 大小 (0-12)  | 用于 *ProviderId*的大小。 |
| 8 | 4 | CellID | UINT32 | 单元 ID (0-268435455) 。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 12 | 4 | EARFCN | UINT32 | 服务单元 (0-65535) 的射频通道号。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 16 | 4 | PhysicalCellID | UINT32 | 物理单元 ID (0-503) 。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 20 | 4 | TAC | UINT32 | 跟踪区域代码 (0-65535) 。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 24 | 4 | RSRP | INT32 | 平均参考信号接收功率。 范围为-140 到-44，单位为1dBm。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 28 | 4 | RSRQ | INT32 | 平均引用信号接收质量。 范围为-20 到-3，单位为1dBm。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 32 | 4 | TimingAdvance | UINT32 | 计时提前 (0-255) 。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 36 |   | DataBuffer | DATABUFFER | 包含 *ProviderId*的数据缓冲区。 |

##### <a name="mbim_lte_mrl"></a><a name="mbim_lte_mrl"></a>MBIM_LTE_MRL

MBIM_LTE_MRL 结构包含 "已测量的结果" 列表 (相邻的 LTE 单元的 MRL) 。

| 偏移量 | 大小 | 字段 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | Elementcount 多于 (EC)  | UINT32 | 此元素后面的 MRL 项的计数。 |
| 4 |   | DataBuffer | DATABUFFER | MRL 记录的数组，每个记录都指定为 [MBIM_LTE_MRL_INFO](#mbim_lte_mrl_info) 结构。 |

##### <a name="mbim_lte_mrl_info"></a><a name="mbim_lte_mrl_info"></a>MBIM_LTE_MRL_INFO

MBIM_LTE_MRL_INFO 结构包含有关相邻的 LTE 单元格的信息。

| 偏移量 | 大小 | 字段 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ProviderIdOffset | OFFSET | 从该结构的开头算起的偏移量（以字节为单位），该偏移量是一个数字 (0-9) 名为 *ProviderId* 的字符串，用于表示网络提供程序标识。 此字符串是三位数 Mobile 国家/地区代码的串联 (MCC) 和两个或三个数字的移动网络代码 (MNC) 。 当没有返回 *ProviderId* 信息时，此成员可能为 NULL。 |
| 4 | 4 | ProviderIdSize | 大小 (0-12)  | 用于 *ProviderId*的大小。 |
| 8 | 4 | CellID | UINT32 | 单元 ID (0-268435455) 。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 12 | 4 | EARFCN | UINT32 | 服务单元 (0-65535) 的射频通道号。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 16 | 4 | PhysicalCellID | UINT32 | 物理单元 ID (0-503) 。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 20 | 4 | TAC | UINT32 | 跟踪区域代码 (0-65535) 。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 24 | 4 | RSRP | INT32 | 平均参考信号接收功率。 范围为-140 到-44，单位为1dBm。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 28 | 4 | RSRQ | INT32 | 平均引用信号接收质量。 范围为-20 到-3，单位为1dBm。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 32 |   | DataBuffer | DATABUFFER | 包含 *ProviderId*的数据缓冲区。 |

#### <a name="cdma-cell-data-structures"></a>CDMA 单元数据结构

##### <a name="mbim_cdma_mrl"></a><a name="mbim_cdma_mrl"></a>MBIM_CDMA_MRL

MBIM_CDMA_MRL 结构包含) 和邻近 CDMA 单元的已测量结果列表 (MRL。

| 偏移量 | 大小 | 字段 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | Elementcount 多于 (EC)  | UINT32 | 此元素后面的 MRL 项的计数。 |
| 4 |   | DataBuffer | DATABUFFER | MRL 记录的数组，每个记录都指定为 [MBIM_CDMA_MRL_INFO](#mbim_cdma_mrl_info) 结构。 |

##### <a name="mbim_cdma_mrl_info"></a><a name="mbim_cdma_mrl_info"></a>MBIM_CDMA_MRL_INFO

MBIM_CDMA_MRL_INFO 的数据结构是为 CDMA2000 网络类型设计的。 可以同时有多个 CDMA2000 服务单元。 在同一列表中将返回提供单元格和相邻单元格的。 **ServingCellFlag**字段指示单元格是否为服务单元。

| 偏移量 | 大小 | 字段 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ServingCellFlag | UINT32 | 指示这是否为服务单元。 如果值为1，则表示服务单元格，值为0时表示相邻单元格。 在调用) 时，一次可能有多个服务单元格 (值得注意。 |
| 4 | 4 | NID | UINT32 | 网络 ID (0-65535) 。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 8 | 4 | SID | UINT32 | 系统 ID (0-32767) 。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 12 | 4 | BaseStationId | UINT32 | 基站 ID (0-65535) 。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 16 | 4 | BaseLatitude | UINT32 | 基站纬度 (0-4194303) 。 这是以0.25 秒为单位编码的，以两个在 DWORD 低22位内的补码表示形式表示。 作为有符号值，北纬度为正值。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 20 | 4 | BaseLongitude | UINT32 | 基站经度 (0-8388607) 。 这是以0.25 秒为单位编码的，以两个在 DWORD 低23位内的补码表示形式表示。 作为有符号值，东经度为正值。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 24 | 4 | RefPN | UINT32 | 基本工作站 PN 编号 (0-511) 。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 28 | 4 | GPSSeconds | UINT32 | GPS 秒数，或此到达基站的时间。 如果此信息不可用，则使用0xFFFFFFFF。 |
| 32 | 4 | PilotStrength | UINT32 | 试点 (0-63) 的信号强度。 如果此信息不可用，则使用0xFFFFFFFF。 |

### <a name="unsolicited-event"></a>主动事件

不适用。

### <a name="status-codes"></a>状态代码

此 CID 使用一般状态代码 (参阅 [公共 USB MBIM standard](https://go.microsoft.com/fwlink/p/?linkid=842064)) 的9.4.5 节中的状态代码的使用。

## <a name="mbim_cid_location_info_status"></a><a name="mbim_cid_location_info_status"></a>MBIM_CID_LOCATION_INFO_STATUS

此 CID 检索表示设备位置的手机网络信息的状态。 当位置信息发生更改时，也可以使用它来传递未经请求的通知。

服务： **MBB_UUID_BASIC_CONNECT_EXTENSIONS**

服务 UUID： **3d01dcc5-fef5-4d05-0d3a-bef7058e9aaf**

| CID | 命令代码 | 最低操作系统版本 |
| --- | --- | --- |
| MBIM_CID_LOCATION_INFO_STATUS | 12 | Windows 10 版本 1709 |

> [!NOTE]
> MBIM_CID_LOCATION_INFO_STATUS 是从 Windows 10 版本1709开始定义的，但操作系统当前不支持。 调制解调器可以将此命令作为通知发送，但操作系统当前不会对其进行处理。

### <a name="parameters"></a>参数

| 类型 | Set | 查询 | 通知 |
| --- | --- | --- | --- |
| 命令 | 不适用 | 不适用 | 不适用 |
| 响应 | Not appliable | MBIM_LOCATION_INFO | MBIM_LOCATION_INFO |

### <a name="query"></a>查询

不使用 MBIM_COMMAND_MSG 的 InformationBuffer。 MBIM_COMMAND_DONE 的 InformationBuffer 包含 [MBIM_LOCATION_INFO](#mbim_location_info) 的结构。

### <a name="set"></a>Set

不适用。

### <a name="response"></a>响应

#### <a name="mbim_location_info"></a><a name="mbim_location_info"></a>MBIM_LOCATION_INFO

| 偏移量 | 大小 | 字段 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | LocationAreaCode | UINT32 | 当前位置的 GSM/UMTS 区号。 如果当前系统类型不适用，则返回0xFFFFFFFF。 |
| 4 | 4 | TrackingAreaCode | UINT32 | 当前位置的 LTE 跟踪区域代码。 如果当前系统类型不适用，则返回0xFFFFFFFF。 |
| 8 | 4 | CellID | UINT32 | 移动电话塔的 ID。 如果 *CellID* 不可用，则返回0xffffffff。 |

### <a name="unsolicited-events"></a>未经请求的事件

事件 InformationBuffer 包含 MBIM_LOCATION_INFO 结构。

如果*Location area code* / *跟踪区域代码*的值更改为有效值，则发送此事件。 此事件不会在*CellID*更改时或*位置区域代码* / *跟踪区域代码*变为无效时发送。

### <a name="status-codes"></a>状态代码

此 CID 使用一般状态代码 (参阅 [公共 USB MBIM standard](https://go.microsoft.com/fwlink/p/?linkid=842064)) 的9.4.5 节中的状态代码的使用。

## <a name="oid_wwan_base_stations_info"></a><a name="oid_wwan_base_stations_info"></a>OID_WWAN_BASE_STATIONS_INFO

[OID_WWAN_BASE_STATIONS_INFO](oid-wwan-base-stations-info.md)MBIM_CID_BASE_STATIONS_INFO 的 NDIS 等效项。

