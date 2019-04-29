---
title: MB UICC 应用程序和文件系统访问权限
description: MB UICC 应用程序和文件系统访问权限
ms.assetid: 9A9BFCCE-2481-412F-AEBB-9919F6916224
keywords:
- MB UICC 应用程序和文件系统访问权限，移动宽带 UICC 应用程序和文件系统访问
ms.date: 03/07/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: ac43797904bb5bce69b5bd28b21f0a181b55928c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367609"
---
# <a name="mb-uicc-application-and-file-system-access"></a>MB UICC 应用程序和文件系统访问权限

## <a name="overview"></a>概述

本主题指定为允许访问 UICC 智能卡应用程序和文件系统的移动宽带接口模型 (MBIM) 接口的扩展。 MBIM 向此扩展会公开逻辑访问 UICC [ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)-兼容的应用程序和文件系统，Windows 10，版本 1903年及更高版本中受支持。

## <a name="uicc-access-and-security"></a>UICC 访问权限和安全性

UICC 提供文件系统，并支持一组可同时运行的应用程序。 其中包括 USIM UMTS、 CSIM CDMA，和 ISIM IMS 的。 Sim 卡是旧的 UICC，可以建模为其中一个应用程序 （GSM) 的一部分。

下图中的章节 8.1 [ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)显示了示例卡应用程序结构。

![示例应用程序结构 UICC](images/mb-uicc-application-structure.png "示例 UICC 应用程序结构。")

UICC 文件系统可以视为目录树的林。 旧的 SIM 树已取得 root 权限在主文件 (MF) 和包含最多两个级别的子目录 （专用文件或 DFs） 包含 Elemental 存放各种类型的信息的文件 (EFs)。 SIM 定义下 MF，之一 DFs DFTelecom，其中包含信息普遍适用于多个访问类型，如公共电话薄。 其他应用程序有效地将作为单独的树，每个取得 root 权限在自己应用程序目录文件 (ADF)。 每个 ADF 由可长达 128 位应用程序标识符标识。 卡根 (下图中 MF EFDir) 下的文件包含应用程序名称和相应的标识符。 树 （MF 或 ADF），在 DFs 和 EFs 可能标识由文件 Id，其中的文件 ID 是 16 位整数的路径。

## <a name="ndis-interface-extensions"></a>NDIS 接口扩展

已定义了下列 Oid 为支持 UICC 应用程序和文件系统访问权限。

- [OID_WWAN_UICC_APP_LIST](oid-wwan-uicc-app-list.md)
- [OID_WWAN_UICC_FILE_STATUS](oid-wwan-uicc-file-status.md)
- [OID_WWAN_UICC_ACCESS_BINARY](oid-wwan-uicc-access-binary.md)
- [OID_WWAN_UICC_ACCESS_RECORD](oid-wwan-uicc-access-record.md)
- [OID_WWAN_PIN_EX2](oid-wwan-pin-ex2.md)

## <a name="mbim-service-and-cid-values"></a>MBIM 服务和 CID 值

| 服务名称 | UUID | UUID 值 |
| --- | --- | --- |
| Microsoft 低级别 UICC 访问 | UUID_MS_UICC_LOW_LEVEL | C2F6588E-F037-4BC9-8665-F4D44BD09367 |
| Microsoft Basic IP 连接扩展 | UUID_BASIC_CONNECT_EXTENSIONS | 3D01DCC5-FEF5-4D05-9D3A-BEF7058E9AAF |

下表指定 UUID 和每个 CID 命令代码，以及是否 CID 支持设置，请查询，或事件 （通知） 请求。 请参阅在本主题中详细了解其参数、 数据结构和通知的每个 CID 的各个部分。 

| CID | UUID | 命令代码 | 设置 | 查询 | 通知 |
| --- | --- | --- | --- | --- | --- |
| MBIM_CID_MS_UICC_APP_LIST | UUID_MS_UICC_LOW_LEVEL | 7 | N | Y | N |
| MBIM_CID_MS_UICC_FILE_STATUS | UUID_MS_UICC_LOW_LEVEL | 8 | N | Y | N |
| MBIM_CID_MS_UICC_ACCESS_BINARY | UUID_MS_UICC_LOW_LEVEL | 9 | Y | Y | N |
| MBIM_CID_MS_UICC_ACCESS_RECORD | UUID_MS_UICC_LOW_LEVEL | 10 | Y | Y | N |
| MBIM_CID_MS_PIN_EX | UUID_BASIC_CONNECT_EXTENSIONS | 15 | Y | Y | N |

## <a name="mbimcidmsuiccapplist"></a>MBIM_CID_MS_UICC_APP_LIST

此 CID 检索 UICC 中的应用程序和其相关信息的列表。 当在调制解调器 UICC 完全初始化和准备好注册到移动运营商，UICC 应用程序必须选择用于注册和具有此 CID 的查询应返回在所选应用程序**ActiveAppIndex**在响应中使用的 MBIM_UICC_APP_LIST 结构中的字段。

### <a name="parameters"></a>Parameters

|  | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| Command | 不适用 | 空 | 不适用 |
| 响应 | 不适用 | MBIM_UICC_APP_LIST | 不适用 |

### <a name="query"></a>查询

MBIM_COMMAND_MSG InformationBuffer 为空。

### <a name="set"></a>设置

不适用。

### <a name="response"></a>响应

在 MBIM_COMMAND_DONE InformationBuffer 包含以下 MBIM_UICC_APP_LIST 结构。

#### <a name="mbimuiccapplist-version-1"></a>MBIM_UICC_APP_LIST （版本 1）

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | Version | UINT32 | 遵循的结构的版本号。 此字段必须设置为**1**的版本 1 的此结构。 |
| 4 | 4 | AppCount | UINT32 | UICC 应用程序数**MBIM_UICC_APP_INFO**在此响应中返回的结构。 |
| 8 | 4 | ActiveAppIndex | UINT32(0..NumApp - 1) | 选择注册到移动网络调制解调器的应用程序的索引。 此字段必须介于**0**并**AppCount-1**。 它为应用程序返回此响应的数组索引。 如果为注册选择没有任何应用程序，则此字段包含**0xFFFFFFFF**。 |
| 12 | 4 | AppListOffset | 偏移量 | 偏移量，以字节为单位，计算从此结构的开头到缓冲区，其中包含的应用列表。 |
| 16 | 4 | AppListSize | SIZE (0..AppCount * 312) | 应用列表数据，以字节为单位的大小。 |
| 20 | AppListSize | DataBuffer | DATABUFFER | 一个数组**AppCount** * **MBIM_UICC_APP_INFO**结构。 |

#### <a name="mbimuiccappinfo"></a>MBIM_UICC_APP_INFO

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | AppType | MBIM_UICC_APP_TYPE | UICC 应用程序的类型。 |
| 4 | 4 | AppIdSize | 大小 (0..16) | 应用程序 ID，以字节为单位的部分 8.3 中定义的大小[ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)。 此字段设置为零**MBIMUiccAppTypeMf**， **MBIMUiccAppTypeMfSIM**，或**MBIMUiccAppTypeMfRUIM**应用类型。 |
| 8 | 16 | AppId | 字节数组 | 应用程序 id。 仅在首**AppIdSize**字节是有意义。 如果应用程序 ID 的长度超过**MBIM_MAXLENGTH_APPID**字节，则 AppIdSize 指定实际的长度限制，但仅在首**MBIM_MAXLENGTH_APPID**字节是在此字段中。 此字段是仅当**AppType**不是**MBIMUiccAppTypeMf**， **MBIMUiccAppTypeMfSIM**，或者**MBIMUiccAppTypeMfRUIM**。 |
| 24 | 4 | AppNameLength | 大小 (0..256) | 以字符为单位，应用程序名称的长度。 |
| 28 | 256 | AppName | ASCII 字符数组 | 指定的应用程序名称的 utf-8 字符串。 通过指定此字段的长度**AppNameLength**。 如果长度大于或等于**MBIM_MAXLENGTH_APPNAME**字节，此字段中包含第一个**MBIM_MAXLENGTH_APPNAME-1**名称个字节。 字符串始终以 null 终止。 |
| 284 | 4 | NumPins | 大小 (0..8) | 应用程序 PIN 引用的数目。 换而言之的元素数量**PinRef**中的有效。 虚拟的 R UIM 上的应用程序有没有 PIN 的引用。 |
| 288 | 8 | PinRef | 字节数组 | 指定应用程序 PIN 的字节数组引用此应用程序 （针对 PIN1 或 UPIN 密钥）、 9.4.2 节中定义[ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)。 对于单验证卡或 MBB 驱动程序和/或调制解调器不支持不同的应用程序密钥的不同应用程序，此字段必须是**0x01**。 |

#### <a name="mbimuiccapptype"></a>MBIM_UICC_APP_TYPE

| 在任务栏的搜索框中键入 | 值 | 描述 |
| --- | --- | --- |
| MBIMUiccAppTypeUnknown | 0 | 未知的类型。 |
| MBIMUiccAppTypeMf | 1 | 旧有 SIM 目录根节点的 MF。 |
| MBIMUiccAppTypeMfSIM | 2 | 旧有 SIM 目录根节点的 DF_GSM。 |
| MBIMUiccAppTypeMfRUIM | 3 | 旧有 SIM 目录根节点的 DF_CDMA。 |
| MBIMUiccAppTypeUSIM | 4 | USIM 应用程序。 |
| MBIMUiccAppTypeCSIM | 5 | CSIM 应用程序。 |
| MBIMUiccAppTypeISIM | 6 | ISIM 应用程序。 |

#### <a name="constants"></a>常量

为 MBIM_CID_MS_UICC_APP_INFO 定义以下常量。

`const int MBIM_MAXLENGTH_APPID = 16`  
`const int MBIM_MAXLENGTH_APPNAME = 256`  
`const int MBIM_MAXNUM_PINREF = 8`  

### <a name="unsolicited-events"></a>未经请求的事件

不适用。

### <a name="status-codes"></a>状态代码

下面的状态代码均适用：

| 状态代码 | 描述 |
| --- | --- |
| MBIM_STATUS_SUCCESS | 基本 MBIM 状态为已定义的所有命令。 |
| MBIM_STATUS_BUSY | 基本 MBIM 状态为已定义的所有命令。 |
| MBIM_STATUS_FAILURE | 基本 MBIM 状态为已定义的所有命令。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | 基本 MBIM 状态为已定义的所有命令。 |
| MBIM_STATUS_SIM_NOT_INSERTED | 无法执行 UICC 操作，因为 UICC 缺少。 |
| MBIM_STATUS_BAD_SIM | 无法执行 UICC 操作，因为 UICC 处于错误状态。 |
| MBIM_STATUS_NOT_INITIALIZED | 无法执行 UICC 操作，因为 UICC 尚未完全初始化。 |

## <a name="mbimcidmsuiccfilestatus"></a>MBIM_CID_MS_UICC_FILE_STATUS

此 CID 检索有关指定 UICC 文件的信息。

### <a name="parameters"></a>Parameters

|  | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| Command | 不适用 | MBIM_UICC_FILE_PATH | 不适用 |
| 响应 | 不适用 | MBIM_UICC_FILE_STATUS | 不适用 |

### <a name="query"></a>查询

MBIM_COMMAND_MSG InformationBuffer 作为 MBIM_UICC_FILE_PATH 结构包含 EF 的目标。

#### <a name="mbimuiccfilepath-version-1"></a>MBIM_UICC_FILE_PATH （版本 1）

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | Version | UINT32 | 遵循的结构的版本号。 此字段必须是**1**的版本 1 的此结构。 |
| 4 | 4 | AppIdOffset | 偏移量 | 偏移量，以字节为单位，计算从此结构的开头到缓冲区，其中包含应用程序 id。 |
| 8 | 4 | AppIdSize | 大小 (0..16) | 应用程序 ID，以字节为单位的部分 8.3 中定义的大小[ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)。 2g 卡为此字段必须设置为零 (0)。 |
| 12 | 4 | FilePathOffset | 偏移量 | 偏移量，以字节为单位，计算从此结构的开头到包含文件路径的缓冲区。 文件路径是 16 位文件 Id 的数组。 第一个 ID 必须是**0x7FFF**或**0x3F00**。 如果第一个 ID 为**0x7FFF**，则该路径是相对于由应用程序 desginated 的 ADF **AppId**。 否则，将从 MF 开始的绝对路径。 |
| 16 | 4 | FilePathSize | 大小 (0..8) | 文件路径，以字节为单位的大小。 |
| 20 |   | DataBuffer | DATABUFFER | 包含 AppId 和文件路径的数据缓冲区。 |

### <a name="set"></a>设置

不适用。

### <a name="response"></a>响应

以下 MBIM_UICC_FILE_STATUS 结构 InformationBuffer 中使用。

#### <a name="mbimuiccfilestatus-version-1"></a>MBIM_UICC_FILE_STATUS （版本 1）

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | Version | UINT32 | 遵循的结构的版本号。 此字段必须是**1**的版本 1 的此结构。 |
| 4 | 4 | StatusWord1 | UINT32(0..256) | 特定于 UICC 命令返回参数。 |
| 8 | 4 | StatusWord2 | UINT32(0..256) | 特定于 UICC 命令返回参数。 |
| 12 | 4 | FileAccessibility | MBIM_UICC_FILE_ACCESSIBILITY | UICC 文件可访问性。 |
| 16 | 4 | FileType | MBIM_UICC_FILE_TYPE | UICC 文件类型。 |
| 20 | 4 | FileStructure | MBIM_UICC_FILE_STRUCTURE | UICC 文件结构。 |
| 24 | 4 | ItemCount | UINT32 | UICC 文件中的项目数。 有关透明和 TLV 文件，则此值设置为**1**。 |
| 28 | 4 | 大小 | UINT32 | 每个项，以字节为单位的大小。 有关透明或 TLV 文件，这是整个 EF 的大小。 对于基于记录的文件，这表示记录的总数。 |
| 32 | 16 | FileLockStatus | MBIM_PIN_TYPE_EX\[4\] | 类型对该文件描述每个操作 （读取、 更新、 激活和停用此顺序） 的访问条件的 MBIM_PIN_TYPE_EX 的数组。 |

#### <a name="mbimuiccfileaccessibility"></a>MBIM_UICC_FILE_ACCESSIBILITY

上述 MBIM_UICC_FILE_STATUS 结构中使用 MBIM_UICC_FILE_ACCESSIBILITY 枚举。

| 在任务栏的搜索框中键入 | ReplTest1 | 描述 |
| --- | --- | --- |
| MBIMUiccFileAccessibilityUnknown | 0 | 文件共享性未知。 |
| MBIMUiccFileAccessibilityNotShareable | 1 | 没有可共享的文件。 |
| MBIMUiccFileAccessibilityShareable | 2 | 可共享的文件。 |

#### <a name="mbimuiccfiletype"></a>MBIM_UICC_FILE_TYPE

上述 MBIM_UICC_FILE_STATUS 结构中使用 MBIM_UICC_FILE_TYPE 枚举。

| 在任务栏的搜索框中键入 | ReplTest1 | 描述 |
| --- | --- | --- |
| MBIMUiccFileTypeUnknown | 0 | 文件类型未知。 |
| MBIMUiccFileTypeWorkingEf | 1 | 使用 EF。 |
| MBIMUiccFileTypeInternalEf | 2 | 内部 EF。 |
| MBIMUiccFileTypeDfOrAdf | 3 | 专用的文件，其他节点的父目录。 这可能是 DF 或 ADF。 |

#### <a name="mbimuiccfilestructure"></a>MBIM_UICC_FILE_STRUCTURE

上述 MBIM_UICC_FILE_STATUS 结构中使用 MBIM_UICC_FILE_STRUCTURE 枚举。

| 在任务栏的搜索框中键入 | 值 | 描述 |
| --- | --- | --- |
| MBIMUiccFileStructureUnknown | 0 | 未知的文件结构。 |
| MBIMUiccFileStructureTransparent | 1 | 可变长度的单个记录。 |
| MBIMUiccFileStructureCyclic | 2 | 循环记录集的记录，每个长度相同。 |
| MBIMUiccFileStructureLinear | 3 | 线性一系列记录，每个长度相同。 |
| MBIMUiccFileStructureBerTLV | 4 | 通过标记可访问的数据值的一组。 |

#### <a name="mbimpintypeex"></a>MBIM_PIN_TYPE_EX

上述 MBIM_UICC_FILE_STATUS 结构中使用 MBIM_PIN_TYPE_EX 枚举。

| 在任务栏的搜索框中键入 | ReplTest1 | 描述 |
| --- | --- | --- |
| MBIMPinTypeNone | 0 | 没有 PIN 正在等待输入。 |
| MBIMPinTypeCustom | 1 | PIN 类型是自定义类型并无其他固定类型的此枚举中列出。 |
| MBIMPinTypePin1 | 2 | PIN1 键。 |
| MBIMPinTypePin2 | 3 | Pin2 码键。 |
| MBIMPinTypeDeviceSimPin | 4 | SIM 键到设备。 |
| MBIMPinTypeDeviceFirstSimPin | 5 | 第一次 SIM 键到设备。 |
| MBIMPinTypeNetworkPin | 6 | 网络个性化设置键。 |
| MBIMPinTypeNetworkSubsetPin | 7 | 网络子集个性化设置键。 |
| MBIMPinTypeServiceProviderPin | 8 | 服务提供商 (SP) 个性化设置密钥。 |
| MBIMPinTypeCorporatePin | 9 | 公司的个性化设置键。 |
| MBIMPinTypeSubsidyLock | 10 | Subsidy 解锁密钥。 | 
| MBIMPinTypePuk1 | 11 | 个人识别号 1 解锁密钥 (PUK1)。 |
| MBIMPinTypePuk2 | 12 | 个人识别号 2 解锁密钥 (PUK2)。 |
| MBIMPinTypeDeviceFirstSimPuk | 13 | 设备连接到第一个 SIM PIN 解锁密钥。 |
| MBIMPinTypeNetworkPuk | 14 | 网络个性化解锁密钥。 |
| MBIMPinTypeNetworkSubsetPuk | 15 | 网络子集个性化解锁密钥。 |
| MBIMPinTypeServiceProviderPuk | 16 | 服务提供商 (SP) 个性化解锁密钥。 |
| MBIMPinTypeCorporatePuk | 17 | 公司的个性化设置解锁密钥。 |
| MBIMPinTypeNev | 18 | NEV 键。 |
| MBIMPinTypeAdm | 19 | 管理密钥。 |

### <a name="unsolicited-events"></a>未经请求的事件

不适用。

### <a name="status-codes"></a>状态代码

下面的状态代码均适用：

| 状态代码 | 描述 |
| --- | --- |
| MBIM_STATUS_BUSY | 基本 MBIM 状态为已定义的所有命令。 |
| MBIM_STATUS_FAILURE | 基本 MBIM 状态为已定义的所有命令。 |
| MBIM_STATUS_SIM_NOT_INSERTED | 无法执行 UICC 操作，因为 UICC 缺少。 |
| MBIM_STATUS_BAD_SIM | 无法执行 UICC 操作，因为 UICC 处于错误状态。 |
| MBIM_STATUS_SHAREABILITY_CONDITION_ERROR | 不能选择该文件，因为它不是可共享，并且当前正在由另一个应用程序访问。 Sim 卡返回状态字是 6985。 |

## <a name="mbimcidmsuiccaccessbinary"></a>MBIM_CID_MS_UICC_ACCESS_BINARY

此 CID 发送特定命令访问 UICC 二进制文件，具有结构类型**MBIMUiccFileStructureTransparent**或**MBIMUiccFileStructureBerTLV**。

### <a name="parameters"></a>Parameters

|  | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| Command | MBIM_UICC_ACCESS_BINARY | MBIM_UICC_ACCESS_BINARY | 不适用 |
| 响应 | MBIM_UICC_RESPONSE | MBIM_UICC_RESPONSE | 不适用 |

### <a name="query"></a>查询

读取二进制文件。 MBIM_COMMAND_MSG InformationBuffer 包含 MBIM_UICC_ACCESS_BINARY 结构。 MBIM_COMMAND_DONE InformationBuffer 返回 MBIM_UICC_RESPONSE 结构。

#### <a name="mbimuiccaccessbinary-version-1"></a>MBIM_UICC_ACCESS_BINARY （版本 1）

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | Version | UINT32 | 遵循的结构的版本号。 此字段必须设置为**1**的版本 1 的此结构。 |
| 4 | 4 | AppIdOffset | 偏移量 | 偏移量，以字节为单位，从缓冲区，其中包含应用程序 id。 向此结构的开头 |
| 8 | 4 | AppIdSize | 大小 (0..16) | 应用程序 ID，以字节为单位的部分 8.3 中定义的大小[ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)。 2g 卡为此字段必须设置为零 (0)。 |
| 12 | 4 | FilePathOffset | 偏移量 | 偏移量，以字节为单位，计算从此结构的开头到包含文件路径的缓冲区。 文件路径是 16 位文件 Id 的数组。 第一个 ID 必须是**0x7FFF**或**0x3F00**。 如果第一个 ID 为**0x7FFF**，则该路径是相对于由应用程序 desginated 的 ADF **AppId**。 否则，将从 MF 开始的绝对路径。 |
| 16 | 4 | FilePathSize | 大小 | 文件路径，以字节为单位的大小。 |
| 20 | 4 | FileOffset | UINT32 | 要从文件读取数据时使用的偏移量。 此字段可以是超过 256 个字符，更大，它结合了偏移量的高和低中定义的偏移量[ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)。 |
| 24 | 4 | NumberOfBytes | UINT32 | 要读取的字节数。 例如，客户端驱动程序可以使用此函数读取大于 256 个字节，尽管可读取或写入单个 UICC 操作的最长为 256 个字节，每个透明 （二进制） 文件[ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)。 它是函数的由负责将此拆分为多个 Apdu 和单个响应中发送回结果。 |
| 28 | 4 | LocalPinOffset | 偏移量 | 偏移量，以字节为单位，计算从此结构的开头到包含密码的缓冲区。 这是本地的 PIN (PIN2)，该操作需要本地 PIN 验证的情况使用。 |
| 32 | 4 | LocalPinSize | 大小 (0..16) | 密码，以字节为单位的大小。 |
| 36 | 4 | BinaryDataOffset | 偏移量 | 偏移量，以字节为单位，计算从此结构的开头到包含特定于命令的数据的缓冲区。 二进制数据仅用于组操作。 |
| 40 | 4 | BinaryDataSize | 大小 (0..32768) | 数据，以字节为单位的大小。 |
| 44 |   | DataBuffer | DATABUFFER | 包含 AppId、 文件路径、 LocalPin 和 BinaryData 数据缓冲区。 |

### <a name="set"></a>设置

更新透明文件。 MBIM_COMMAND_MSG InformationBuffer 包含 MBIM_UICC_ACCESS_BINARY 结构。 MBIM_COMMAND_DONE InformationBuffer 返回 MBIM_UICC_RESPONSE 结构。

### <a name="response"></a>响应

以下 MBIM_UICC_RESPONSE 结构 InformationBuffer 中使用。

#### <a name="mbimuiccresponse-version-1"></a>MBIM_UICC_RESPONSE （版本 1）

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | Version | UINT32 | 遵循结构的版本号。 此字段必须是**1**的版本 1 的此结构。 |
| 4 | 4 | StatusWord1 | UINT32(0..256) | 特定于 UICC 命令返回参数。 |
| 8 | 4 | StatusWord2 | UINT32(0..256) | 特定于 UICC 命令返回参数。 |
| 12 | 4 | ResponseDataOffset | 偏移量 | 偏移量，以字节为单位，计算从此结构的开头到包含响应数据的缓冲区。 响应数据仅用于查询操作。 |
| 16 | 4 | ResponseDataSize | 大小 (0..32768) | 数据，以字节为单位的大小。 |
| 20 |   | DataBuffer | DATABUFFER | 包含 ResponseData 的数据缓冲区。 |

### <a name="unsolicited-events"></a>未经请求的事件

不适用。

### <a name="status-codes"></a>状态代码

下面的状态代码均适用：

| 状态代码 | 描述 |
| --- | --- |
| MBIM_STATUS_BUSY | 基本 MBIM 状态为已定义的所有命令。 |
| MBIM_STATUS_FAILURE | 基本 MBIM 状态为已定义的所有命令。 |
| MBIM_STATUS_SIM_NOT_INSERTED | 无法执行 UICC 操作，因为 UICC 缺少。 |
| MBIM_STATUS_BAD_SIM | 无法执行 UICC 操作，因为 UICC 处于错误状态。 |
| MBIM_STATUS_SHAREABILITY_CONDITION_ERROR | 不能选择该文件，因为它不是可共享，并且当前正在由另一个应用程序访问。 Sim 卡返回状态字是 6985。 |
| MBIM_STATUS_PIN_FAILURE | 由于 PIN 错误，操作失败。 |

## <a name="mbimcidmsuiccaccessrecord"></a>MBIM_CID_MS_UICC_ACCESS_RECORD

此 CID 发送特定命令来访问 UICC 线性固定或循环文件中的，结构类型为**MBIMUiccFileStructureCyclic**或**MBIMUIccFileStructureLinear**。

### <a name="parameters"></a>Parameters

|  | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| Command | MBIM_UICC_ACCESS_RECORD | MBIM_UICC_ACCESS_RECORD | 不适用 |
| 响应 | MBIM_UICC_RESPONSE | MBIM_UICC_RESPONSE | 不适用 |

### <a name="query"></a>查询

读取一条记录的内容。 MBIM_COMMAND_MSG InformationBuffer 包含以下 MBIM_UICC_ACCESS_RECORD 结构。 MBIM_UICC_RESPONSE MBIM_COMMAND_DONE InformationBuffer 中返回。

#### <a name="mbimuiccaccessrecord-version-1"></a>MBIM_UICC_ACCESS_RECORD （版本 1）

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | Version | UINT32 | 遵循的结构的版本号。 此字段必须设置为**1**的版本 1 的此结构。 |
| 4 | 4 | AppIdOffset | 偏移量 | 偏移量，以字节为单位，从缓冲区，其中包含应用程序 id。 向此结构的开头 |
| 8 | 4 | AppIdSize | 大小 (0..16) | 应用程序 ID，以字节为单位的部分 8.3 中定义的大小[ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)。 2g 卡为此字段必须设置为零 (0)。 |
| 12 | 4 | FilePathOffset | 偏移量 | 偏移量，以字节为单位，计算从此结构的开头到包含文件路径的缓冲区。 文件路径是 16 位文件 Id 的数组。 第一个 ID 必须是**0x7FFF**或**0x3F00**。 如果第一个 ID 为**0x7FFF**，则该路径是相对于由应用程序 desginated 的 ADF **AppId**。 否则，将从 MF 开始的绝对路径。 |
| 16 | 4 | FilePathSize | 大小 | 文件路径，以字节为单位的大小。 |
| 20 | 4 | RecordNumber | UINT32(0..256) | 记录编号。 这在所有时间表示记录的绝对索引。 不支持相对记录访问，因为调制解调器上的文件 （下一步上, 一步) 可以执行多个访问。 |
| 24 | 4 | LocalPinOffset | 偏移量 | 偏移量，以字节为单位，计算从此结构的开头到包含密码的缓冲区。 锁定密码是十进制数字的以 null 结尾的 utf-8 字符串。 | 
| 28 | 4 | LocalPinSize | 大小 (0..16) | 密码，以字节为单位的大小。 |
| 32 | 4 | RecordDataOffset | 偏移量 | 偏移量，以字节为单位，计算从此结构的开头到包含特定于命令的数据的缓冲区。 记录数据仅用于组操作。 |
| 36 | 4 | RecordDataSize | 大小 (0..256) | 数据，以字节为单位的大小。 |
| 40 |   | DataBuffer | DATABUFFER | 包含 AppId、 文件路径、 LocalPin 和 RecordData 的数据缓冲区。 |

### <a name="set"></a>设置

更新线性固定或循环文件。 MBIM_COMMAND_MSG InformationBuffer 包含以下 MBIM_UICC_ACCESS_RECORD 结构。 MBIM_UICC_RESPONSE MBIM_COMMAND_DONE InformationBuffer 中返回。

### <a name="response"></a>响应

MBIM_UICC_RESPONSE 结构 InformationBuffer 中使用。

### <a name="unsolicited-events"></a>未经请求的事件

不适用。

### <a name="status-codes"></a>状态代码

下面的状态代码均适用：

| 状态代码 | 描述 |
| --- | --- |
| MBIM_STATUS_BUSY | 基本 MBIM 状态为已定义的所有命令。 |
| MBIM_STATUS_FAILURE | 基本 MBIM 状态为已定义的所有命令。 |
| MBIM_STATUS_SIM_NOT_INSERTED | 无法执行 UICC 操作，因为 UICC 缺少。 |
| MBIM_STATUS_BAD_SIM | 无法执行 UICC 操作，因为 UICC 处于错误状态。 |
| MBIM_STATUS_SHAREABILITY_CONDITION_ERROR | 不能选择该文件，因为它不是可共享，并且当前正在由另一个应用程序访问。 Sim 卡返回状态字是 6985。 |
| MBIM_STATUS_PIN_FAILURE | 由于 PIN 错误，操作失败。 |

## <a name="mbimcidmspinex"></a>MBIM_CID_MS_PIN_EX

此 CID 用于执行所有的 PIN 安全操作中的第 9 节定义[ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)。 CID 类似于 MBIM_CID_MS_PIN，但将其扩展到支持多应用 UICC 卡。 支持仅单验证能够 UICCs。 支持多 verification 的 UICCs 支持多个应用程序不支持固定的。 一个应用程序 PIN (PIN1) 分配给所有 ADFs/DFs 和 UICC 上的文件。 但是，每个应用程序可以指定为级别 2 用户验证要求，从而需要为每个访问命令的其他验证为本地固定 (PIN2)。 这种情况下是 MBIM_CID_MS_PIN_EX 的支持。

就像 MBIM_CID_MS_PIN，与 MBIM_CID_MS_PIN_EX 设备只报告一个插针一次。 如果启用了多个插针，并且也启用报告多个插针，然后函数必须报告 PIN1 第一次。 例如，如果启用 subsidy 锁报告和启用 SIM 的 PIN1，然后 subsidy 锁定 PIN 应报告后续查询请求中仅后 PIN1 已成功验证。 一个空的插针是 MBIMPinOperationEnter 以及允许的。 一个空的插针指定 PinSize 设置为零。 在这种情况下，SET 命令类似于查询并返回所引用的 PIN 的状态。 这完全对齐的行为的验证命令的节指定 11.1.9 [ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)。

### <a name="parameters"></a>Parameters

|  | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| Command | MBIM_SET_PIN_EX | MBIM_PIN_APP | 不适用 |
| 响应 | MBIM_PIN_INFO_EX | MBIM_PIN_INFO_EX | 不适用 |

### <a name="query"></a>查询

以下 MBIM_PIN_APP 结构 InformationBuffer 中使用。

#### <a name="mbimpinapp-version-1"></a>MBIM_PIN_APP （版本 1）

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | Version | UINT32 | 遵循的结构的版本号。 此字段必须设置为**1**的版本 1 的此结构。 |
| 4 | 4 | AppIdOffset | 偏移量 | 偏移量，以字节为单位，从缓冲区，其中包含应用程序 id。 向此结构的开头 |
| 8 | 4 | AppIdSize | 大小 (0..16) | 应用程序 ID，以字节为单位的部分 8.3 中定义的大小[ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)。 2g 卡为此字段必须设置为零 (0)。 |
| 12 |   | DataBuffer | DATABUFFER | 如中所定义的 AppId [ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)。 |

### <a name="set"></a>设置

以下 MBIM_SET_PIN_EX 结构 InformationBuffer 中使用。

#### <a name="mbimsetpinex"></a>MBIM_SET_PIN_EX

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | PinType | MBIM_PIN_TYPE_EX | PIN 类型中。 请参阅本主题中的 MBIM_PIN_TYPE_EX 表。 |
| 4 | 4 | PinOperation | MBIM_PIN_OPERATION | PIN 操作中。 MBIM 1.0，请参阅。 |
| 8 | 4 | PinOffset | 偏移量 | 偏移量，以字节为单位，计算从此结构的开头到一个字符串，表示要对其执行操作的 PIN 值的 PIN 或固定值所需启用或禁用 PIN 设置。 此字段适用于的所有值**PinOperation**。 |
| 12 | 4 | PinSize | 大小 (0..32) | 以字节为单位，用于固定大小。 |
| 16 | 4 | NewPinOffset | 偏移量 | 为此结构的开头的偏移量，以字节为单位，计算**NewPin**字符串，表示新的 PIN 值，设置何时**PinOperation**是 MBIMPinOperationChange 或PinTypeMBIMPinTypePuk1 或 PinTypeMBIMPinTypePuk2 MBIMPinOperationEnter。 |
| 20 | 4 | NewPinSize | 大小 (0..32) | 以字节为单位，用于 NewPin 大小。 |
| 24 | 4 | AppIdOffset | 偏移量 | 偏移量，以字节为单位，计算从此结构的开头到缓冲区，其中包含应用程序 id。 |
| 28 | 4 | AppIdSize | 大小 (0..16) | 应用程序 ID，以字节为单位的部分 8.3 中定义的大小[ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)。 2g 卡为此字段必须设置为零 (0)。 |
| 32 |   | DataBuffer | DATABUFFER | 包含的 Pin、 NewPin 和应用程序标识的数据缓冲区。 |

### <a name="response"></a>响应

以下 MBIM_PIN_INFO_EX 结构 InformationBuffer 中使用。

| 偏移量 | 大小 | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | PinType | MBIM_PIN_TYPE_EX | PIN 类型中。 请参阅本主题中的 MBIM_PIN_TYPE_EX 表。 |
| 4 | 4 | PinState | MBIM_PIN_STATE | PIN 状态中。 MBIM 1.0，请参阅。 |
| 8 | 4 | RemainingAttempts | UINT32 | 剩余尝试次数对于任何与 PIN 相关的操作，如输入，启用或禁用。 不支持此信息的设备必须将此成员设置为 0xFFFFFFFF。 |

### <a name="unsolicited-events"></a>未经请求的事件

不适用。

### <a name="status-codes"></a>状态代码

下面的状态代码均适用：

| 状态代码 | 描述 |
| --- | --- |
| MBIM_STATUS_BUSY | 基本 MBIM 状态为已定义的所有命令。 |
| MBIM_STATUS_FAILURE | 基本 MBIM 状态为已定义的所有命令。 |
| MBIM_STATUS_SIM_NOT_INSERTED | 无法执行 UICC 操作，因为 UICC 缺少。 |
| MBIM_STATUS_BAD_SIM | 无法执行 UICC 操作，因为 UICC 处于错误状态。 |
| MBIM_STATUS_PIN_DISABLED | 操作失败，因为 PIN 已被禁用。 |
| MBIM_STATUS_PIN_REQUIRED | 操作失败，因为必须输入 PIN 以继续。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | 操作失败，因为设备不支持上相应的固定类型的集。 |
