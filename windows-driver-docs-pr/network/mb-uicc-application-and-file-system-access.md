---
title: MB UICC 应用程序和文件系统访问权限
description: MB UICC 应用程序和文件系统访问权限
ms.assetid: 9A9BFCCE-2481-412F-AEBB-9919F6916224
keywords:
- MB UICC 应用程序和文件系统访问，移动宽带 UICC 应用程序和文件系统访问
ms.date: 03/07/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 5462e874d16d1de9a612a808d61b7394d9fefcfd
ms.sourcegitcommit: b8876f616ac625bb3f38218a32b2dc35ac7b3399
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2019
ms.locfileid: "73443053"
---
# <a name="mb-uicc-application-and-file-system-access"></a>MB UICC 应用程序和文件系统访问权限

## <a name="overview"></a>概述

本主题指定移动宽带接口模型（MBIM）接口的扩展，以允许访问 UICC 智能卡应用程序和文件系统。 此 MBIM 扩展公开了对 UICC 的[ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)兼容应用程序和文件系统的逻辑访问，Windows 10 版本1903及更高版本中支持。

## <a name="uicc-access-and-security"></a>UICC 访问和安全

UICC 提供了文件系统并支持一组可同时运行的应用程序。 其中包括 USIM for UMTS、CSIM for CDMA 和 ISIM for IMS。 SIM 是 UICC 的旧部分，可以建模为这些应用程序之一（适用于 GSM）。

[ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)第8.1 节中的下图显示了一个示例卡应用程序结构。

![示例 UICC 应用程序结构](images/mb-uicc-application-structure.png "UICC 应用程序结构的示例。")

UICC 文件系统可视为目录树的林。 旧的 SIM 树以 Master 文件（MF）为根，最多包含两个级别的子目录（专用文件或 DFs），其中包含保存各种类型信息的 Elemental 文件（EFs）。 SIM 在 MF 下定义 DFs，其中一个是 DFTelecom，其中包含多个访问类型（如公用电话簿）的通用信息。 附加的应用程序实际上是作为单独的树实现的，每个树都位于其自己的应用程序目录文件（ADF）中。 每个 ADF 都由应用程序标识符标识，最大长度为128位。 卡根下的文件（关系图中的 MF 下的 EFDir）包含应用程序名称和对应的标识符。 在树（MF 或 ADF）中，DFs 和 EFs 可能由文件 id 的路径标识，其中文件 ID 是16位整数。

## <a name="ndis-interface-extensions"></a>NDIS 接口扩展

定义了以下 Oid，以支持 UICC 应用程序和文件系统访问。

- [OID_WWAN_UICC_APP_LIST](oid-wwan-uicc-app-list.md)
- [OID_WWAN_UICC_FILE_STATUS](oid-wwan-uicc-file-status.md)
- [OID_WWAN_UICC_ACCESS_BINARY](oid-wwan-uicc-access-binary.md)
- [OID_WWAN_UICC_ACCESS_RECORD](oid-wwan-uicc-access-record.md)
- [OID_WWAN_PIN_EX2](oid-wwan-pin-ex2.md)

## <a name="mbim-service-and-cid-values"></a>MBIM 服务和 CID 值

| 服务名称 | UUID | UUID 值 |
| --- | --- | --- |
| Microsoft 低级别 UICC 访问 | UUID_MS_UICC_LOW_LEVEL | C2F6588E-F037-4BC9-8665-F4D44BD09367 |
| Microsoft 基本 IP 连接扩展插件 | UUID_BASIC_CONNECT_EXTENSIONS | 3D01DCC5-FEF5-4D05-9D3A-BEF7058E9AAF |

下表为每个 CID 指定了 UUID 和命令代码，以及 CID 是否支持设置、查询或事件（通知）请求。 有关其参数、数据结构和通知的详细信息，请参阅本主题中的每个 CID 的各个部分。 

| CID | UUID | 命令代码 | 设置 | 查询 | 通知 |
| --- | --- | --- | --- | --- | --- |
| MBIM_CID_MS_UICC_APP_LIST | UUID_MS_UICC_LOW_LEVEL | 7 | N | Y | N |
| MBIM_CID_MS_UICC_FILE_STATUS | UUID_MS_UICC_LOW_LEVEL | 8 | N | Y | N |
| MBIM_CID_MS_UICC_ACCESS_BINARY | UUID_MS_UICC_LOW_LEVEL | 9 | Y | Y | N |
| MBIM_CID_MS_UICC_ACCESS_RECORD | UUID_MS_UICC_LOW_LEVEL | 10 | Y | Y | N |
| MBIM_CID_MS_PIN_EX | UUID_BASIC_CONNECT_EXTENSIONS | 15 | Y | Y | N |

## <a name="mbim_cid_ms_uicc_app_list"></a>MBIM_CID_MS_UICC_APP_LIST

此 CID 会检索 UICC 中的应用程序列表以及这些应用程序的相关信息。 当调制解调器中的 UICC 完全初始化并准备向移动运营商注册时，必须选择 UICC 应用程序进行注册，并且具有此 CID 的查询应返回 MBIM_UICC 中的**ActiveAppIndex**字段中的所选应用程序。用于响应的 _APP_LIST 结构。

### <a name="parameters"></a>参数

|  | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| 命令 | 不适用 | 空 | 不适用 |
| 响应 | 不适用 | MBIM_UICC_APP_LIST | 不适用 |

### <a name="query"></a>查询

MBIM_COMMAND_MSG 的 InformationBuffer 为空。

### <a name="set"></a>设置

不适用。

### <a name="response"></a>响应

MBIM_COMMAND_DONE 中的 InformationBuffer 包含以下 MBIM_UICC_APP_LIST 结构。

#### <a name="mbim_uicc_app_list-version-1"></a>MBIM_UICC_APP_LIST （版本1）

| 偏移量 | Size | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | 版本 | UINT32 | 后面的结构的版本号。 对于此结构的版本1，此字段必须设置为**1** 。 |
| 4 | 4 | AppCount | UINT32 | 此响应中返回的 UICC application **MBIM_UICC_APP_INFO**结构的数目。 |
| 8 | 4 | ActiveAppIndex | UINT32 （0） | 调制解调器选择的用于向移动网络注册的应用程序的索引。 此字段必须介于**0**到**AppCount-1**之间。 它将索引到此响应返回的应用程序数组。 如果没有为注册选择任何应用程序，则此字段将包含**0xffffffff**。 |
| 12 | 4 | AppListOffset | 抵销 | 从该结构的开头计算的偏移量（以字节为单位），该偏移量为包含应用列表的缓冲区。 |
| 16 | 4 | AppListSize | SIZE （0 ... AppCount * 312） | 应用列表数据的大小（以字节为单位）。 |
| 20 | AppListSize | DataBuffer | DATABUFFER | **AppCount** * **MBIM_UICC_APP_INFO**结构的数组。 |

#### <a name="mbim_uicc_app_info"></a>MBIM_UICC_APP_INFO

| 偏移量 | Size | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | AppType | MBIM_UICC_APP_TYPE | UICC 应用程序的类型。 |
| 4 | 4 | AppIdSize | 大小（0到16） | [ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)的8.3 节中定义的应用程序 ID 的大小（以字节为单位）。 对于**MBIMUiccAppTypeMf**、 **MBIMUiccAppTypeMfSIM**或**MBIMUiccAppTypeMfRUIM**应用类型，此字段设置为零。 |
| 8 | 16 | AppId | 字节数组 | 应用程序 ID。 只有第一个**AppIdSize**字节是有意义的。 如果应用程序 ID 的长度超过**MBIM_MAXLENGTH_APPID**个字节，则 AppIdSize 指定实际长度，但此字段中仅有前**MBIM_MAXLENGTH_APPID**个字节。 仅当**AppType**不是**MBIMUiccAppTypeMf**、 **MBIMUiccAppTypeMfSIM**或**MBIMUiccAppTypeMfRUIM**时，此字段才有效。 |
| 24 | 4 | AppNameLength | 大小（0-256） | 应用程序名称的长度（以字符为字符）。 |
| 28 | 256 | AppName | ASCII 字符数组 | 指定应用程序名称的 UTF-8 字符串。 此字段的长度由**AppNameLength**指定。 如果长度大于或等于**MBIM_MAXLENGTH_APPNAME**字节，则此字段包含名称的第一个**MBIM_MAXLENGTH_APPNAME**字节。 字符串始终以 null 结尾。 |
| 284 | 4 | NumPins | 大小（0到8） | 应用程序 PIN 引用的数目。 换言之， **PinRef**的元素数是有效的。 虚拟 R-UIM 上的应用程序没有 PIN 引用。 |
| 288 | 8 | PinRef | 字节数组 | 一个字节数组，为此应用程序指定应用程序 PIN 引用（适用于 PIN1 的键，可能是 UPIN），如[ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)的部分9.4.2 中所定义。 对于单一验证卡，或者不支持不同应用程序的不同应用程序密钥的 MBB 驱动程序和/或调制解调器，此字段必须为**0x01**。 |

#### <a name="mbim_uicc_app_type"></a>MBIM_UICC_APP_TYPE

| 在任务栏的搜索框中键入 | Value | 描述 |
| --- | --- | --- |
| MBIMUiccAppTypeUnknown | 0 | 未知类型。 |
| MBIMUiccAppTypeMf | 1 | MF 上的旧版 SIM 目录。 |
| MBIMUiccAppTypeMfSIM | 2 | DF_GSM 上的旧版 SIM 目录。 |
| MBIMUiccAppTypeMfRUIM | 3 | DF_CDMA 上的旧版 SIM 目录。 |
| MBIMUiccAppTypeUSIM | 4 | USIM 应用程序。 |
| MBIMUiccAppTypeCSIM | 5 | CSIM 应用程序。 |
| MBIMUiccAppTypeISIM | 6 | ISIM 应用程序。 |

#### <a name="constants"></a>常量

以下常量是为 MBIM_CID_MS_UICC_APP_INFO 定义的。

`const int MBIM_MAXLENGTH_APPID = 16`  
`const int MBIM_MAXLENGTH_APPNAME = 256`  
`const int MBIM_MAXNUM_PINREF = 8`  

### <a name="unsolicited-events"></a>未经请求的事件

不适用。

### <a name="status-codes"></a>状态代码

以下状态代码适用：

| 状态代码 | 描述 |
| --- | --- |
| MBIM_STATUS_SUCCESS | 为所有命令定义的基本 MBIM 状态。 |
| MBIM_STATUS_BUSY | 为所有命令定义的基本 MBIM 状态。 |
| MBIM_STATUS_FAILURE | 为所有命令定义的基本 MBIM 状态。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | 为所有命令定义的基本 MBIM 状态。 |
| MBIM_STATUS_SIM_NOT_INSERTED | 无法执行 UICC 操作，因为缺少 UICC。 |
| MBIM_STATUS_BAD_SIM | 无法执行 UICC 操作，因为 UICC 处于错误状态。 |
| MBIM_STATUS_NOT_INITIALIZED | 无法执行 UICC 操作，因为 UICC 尚未完全初始化。 |

## <a name="mbim_cid_ms_uicc_file_status"></a>MBIM_CID_MS_UICC_FILE_STATUS

此 CID 检索有关指定 UICC 文件的信息。

### <a name="parameters"></a>参数

|  | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| 命令 | 不适用 | MBIM_UICC_FILE_PATH | 不适用 |
| 响应 | 不适用 | MBIM_UICC_FILE_STATUS | 不适用 |

### <a name="query"></a>查询

MBIM_COMMAND_MSG 的 InformationBuffer 将目标 EF 包含为 MBIM_UICC_FILE_PATH 结构。

#### <a name="mbim_uicc_file_path-version-1"></a>MBIM_UICC_FILE_PATH （版本1）

| 偏移量 | Size | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | 版本 | UINT32 | 后面的结构的版本号。 对于此结构的版本1，此字段必须为**1** 。 |
| 4 | 4 | AppIdOffset | 抵销 | 从该结构的开头计算的偏移量（以字节为单位），该偏移量为包含应用程序 ID 的缓冲区。 |
| 8 | 4 | AppIdSize | 大小（0到16） | [ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)的8.3 节中定义的应用程序 ID 的大小（以字节为单位）。 对于2G 卡，此字段必须设置为零（0）。 |
| 12 | 4 | FilePathOffset | 抵销 | 从此结构开始到包含文件路径的缓冲区计算的偏移量（以字节为单位）。 文件路径是16位文件 Id 的数组。 第一个 ID 必须是**0x7FFF**或**0x3F00**。 如果第一个 ID 为**0x7FFF**，则该路径相对于**AppId**的应用程序 desginated 的 ADF。 否则，它是从 MF 开始的绝对路径。 |
| 16 | 4 | FilePathSize | 大小（0到8） | 文件路径的大小（以字节为单位）。 |
| 20 |   | DataBuffer | DATABUFFER | 包含 AppId 和 FilePath 的数据缓冲区。 |

### <a name="set"></a>设置

不适用。

### <a name="response"></a>响应

在 InformationBuffer 中使用以下 MBIM_UICC_FILE_STATUS 结构。

#### <a name="mbim_uicc_file_status-version-1"></a>MBIM_UICC_FILE_STATUS （版本1）

| 偏移量 | Size | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | 版本 | UINT32 | 后面的结构的版本号。 对于此结构的版本1，此字段必须为**1** 。 |
| 4 | 4 | StatusWord1 | UINT32 （0） | 特定于 UICC 命令的返回参数。 |
| 8 | 4 | StatusWord2 | UINT32 （0） | 特定于 UICC 命令的返回参数。 |
| 12 | 4 | FileAccessibility | MBIM_UICC_FILE_ACCESSIBILITY | UICC 文件可访问性。 |
| 16 | 4 | FileType | MBIM_UICC_FILE_TYPE | UICC 文件类型。 |
| 20 | 4 | FileStructure | MBIM_UICC_FILE_STRUCTURE | UICC 文件结构。 |
| 24 | 4 | ItemCount | UINT32 | UICC 文件中的项数。 对于透明和 TLV 文件，此设置为**1**。 |
| 28 | 4 | Size | UINT32 | 每个项的大小（以字节为单位）。 对于透明或 TLV 文件，这是整个 EF 的大小。 对于基于记录的文件，这表示记录的总数。 |
| 32 | 16 | FileLockStatus | MBIM_PIN_TYPE_EX\[4\] | MBIM_PIN_TYPE_EX 类型的数组，它描述该文件上每个操作（读取、更新、激活和停用）的访问条件。 |

#### <a name="mbim_uicc_file_accessibility"></a>MBIM_UICC_FILE_ACCESSIBILITY

MBIM_UICC_FILE_ACCESSIBILITY 枚举用于前面的 MBIM_UICC_FILE_STATUS 结构。

| 在任务栏的搜索框中键入 | Value | 描述 |
| --- | --- | --- |
| MBIMUiccFileAccessibilityUnknown | 0 | 文件可共享性未知。 |
| MBIMUiccFileAccessibilityNotShareable | 1 | 不可共享的文件。 |
| MBIMUiccFileAccessibilityShareable | 2 | 可共享文件。 |

#### <a name="mbim_uicc_file_type"></a>MBIM_UICC_FILE_TYPE

MBIM_UICC_FILE_TYPE 枚举用于前面的 MBIM_UICC_FILE_STATUS 结构。

| 在任务栏的搜索框中键入 | Value | 描述 |
| --- | --- | --- |
| MBIMUiccFileTypeUnknown | 0 | 文件类型未知。 |
| MBIMUiccFileTypeWorkingEf | 1 | 正在运行 EF。 |
| MBIMUiccFileTypeInternalEf | 2 | 内部 EF。 |
| MBIMUiccFileTypeDfOrAdf | 3 | 专用文件，是其他节点的父目录。 这可能是一种 DF 或 ADF。 |

#### <a name="mbim_uicc_file_structure"></a>MBIM_UICC_FILE_STRUCTURE

MBIM_UICC_FILE_STRUCTURE 枚举用于前面的 MBIM_UICC_FILE_STATUS 结构。

| 在任务栏的搜索框中键入 | Value | 描述 |
| --- | --- | --- |
| MBIMUiccFileStructureUnknown | 0 | 未知的文件结构。 |
| MBIMUiccFileStructureTransparent | 1 | 长度可变的单个记录。 |
| MBIMUiccFileStructureCyclic | 2 | 循环的记录集，每个记录都具有相同的长度。 |
| MBIMUiccFileStructureLinear | 3 | 线性记录集，每个记录都具有相同的长度。 |
| MBIMUiccFileStructureBerTLV | 4 | 标记可访问的一组数据值。 |

#### <a name="mbim_pin_type_ex"></a>MBIM_PIN_TYPE_EX

MBIM_PIN_TYPE_EX 枚举用于前面的 MBIM_UICC_FILE_STATUS 结构。

| 在任务栏的搜索框中键入 | Value | 描述 |
| --- | --- | --- |
| MBIMPinTypeNone | 0 | 未等待输入任何 PIN。 |
| MBIMPinTypeCustom | 1 | PIN 类型为自定义类型，并且不是此枚举中列出的其他任何类型的 PIN 类型。 |
| MBIMPinTypePin1 | 2 | PIN1 键。 |
| MBIMPinTypePin2 | 3 | PIN2 密钥。 |
| MBIMPinTypeDeviceSimPin | 4 | 设备到 SIM 密钥。 |
| MBIMPinTypeDeviceFirstSimPin | 5 | 设备到首个 SIM 密钥。 |
| MBIMPinTypeNetworkPin | 6 | 网络个性化项。 |
| MBIMPinTypeNetworkSubsetPin | 7 | 网络子集个性化设置密钥。 |
| MBIMPinTypeServiceProviderPin | 8 | 服务提供程序（SP）个性化设置密钥。 |
| MBIMPinTypeCorporatePin | 9 | 公司个性化键。 |
| MBIMPinTypeSubsidyLock | 10 | Subsidy 解锁密钥。 | 
| MBIMPinTypePuk1 | 11 | 个人识别码1解锁密钥（PUK1）。 |
| MBIMPinTypePuk2 | 12 | 个人识别码2解锁密钥（PUK2）。 |
| MBIMPinTypeDeviceFirstSimPuk | 13 | 设备到非常第一个 SIM 卡 PIN 解锁密钥。 |
| MBIMPinTypeNetworkPuk | 14 | 网络个性化解锁密钥。 |
| MBIMPinTypeNetworkSubsetPuk | 15 | 网络子集个性化设置解锁密钥。 |
| MBIMPinTypeServiceProviderPuk | 16 | 服务提供程序（SP）个性化设置解锁密钥。 |
| MBIMPinTypeCorporatePuk | 17 | 公司个性化设置解锁密钥。 |
| MBIMPinTypeNev | 18 | NEV 键。 |
| MBIMPinTypeAdm | 19 | 管理密钥。 |

### <a name="unsolicited-events"></a>未经请求的事件

不适用。

### <a name="status-codes"></a>状态代码

以下状态代码适用：

| 状态代码 | 描述 |
| --- | --- |
| MBIM_STATUS_BUSY | 为所有命令定义的基本 MBIM 状态。 |
| MBIM_STATUS_FAILURE | 为所有命令定义的基本 MBIM 状态。 |
| MBIM_STATUS_SIM_NOT_INSERTED | 无法执行 UICC 操作，因为缺少 UICC。 |
| MBIM_STATUS_BAD_SIM | 无法执行 UICC 操作，因为 UICC 处于错误状态。 |
| MBIM_STATUS_SHAREABILITY_CONDITION_ERROR | 无法选择此文件，因为它不可共享且当前正在被另一个应用程序访问。 SIM 返回的状态字为6985。 |

## <a name="mbim_cid_ms_uicc_access_binary"></a>MBIM_CID_MS_UICC_ACCESS_BINARY

此 CID 发送特定命令来访问 UICC 二进制文件，结构类型为**MBIMUiccFileStructureTransparent**或**MBIMUiccFileStructureBerTLV**。

### <a name="parameters"></a>参数

|  | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| 命令 | 不适用 | MBIM_UICC_ACCESS_BINARY | 不适用 |
| 响应 | 不适用 | MBIM_UICC_RESPONSE | 不适用 |

### <a name="query"></a>查询

读取二进制文件。 MBIM_COMMAND_MSG 的 InformationBuffer 包含 MBIM_UICC_ACCESS_BINARY 结构。 MBIM_UICC_RESPONSE 结构在 MBIM_COMMAND_DONE 的 InformationBuffer 中返回。

#### <a name="mbim_uicc_access_binary-version-1"></a>MBIM_UICC_ACCESS_BINARY （版本1）

| 偏移量 | Size | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | 版本 | UINT32 | 后面的结构的版本号。 对于此结构的版本1，此字段必须设置为**1** 。 |
| 4 | 4 | AppIdOffset | 抵销 | 从此结构开始到包含应用程序 ID 的缓冲区的偏移量（以字节为单位）。 |
| 8 | 4 | AppIdSize | 大小（0到16） | [ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)的8.3 节中定义的应用程序 ID 的大小（以字节为单位）。 对于2G 卡，此字段必须设置为零（0）。 |
| 12 | 4 | FilePathOffset | 抵销 | 从此结构开始到包含文件路径的缓冲区计算的偏移量（以字节为单位）。 文件路径是16位文件 Id 的数组。 第一个 ID 必须是**0x7FFF**或**0x3F00**。 如果第一个 ID 为**0x7FFF**，则该路径相对于**AppId**的应用程序 desginated 的 ADF。 否则，它是从 MF 开始的绝对路径。 |
| 16 | 4 | FilePathSize | 规格 | 文件路径的大小（以字节为单位）。 |
| 20 | 4 | FileOffset | UINT32 | 从文件读取时使用的偏移量。 此字段可以大于256，并且它结合了[ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)中定义的 offset 高低和 offset low。 |
| 24 | 4 | NumberOfBytes | UINT32 | 要读取的字节数。 例如，客户端驱动程序可以使用此函数读取大于256字节的透明（二进制）文件，不过，可以读取或写入单个 UICC 操作的最大数量为每[ETSI TS 102 221 技术规范的256字节](https://go.microsoft.com/fwlink/p/?linkid=864594). 函数负责将此拆分为多个 Apdu，并在单个响应中返回结果。 |
| 28 | 4 | LocalPinOffset | 抵销 | 从此结构开始到包含密码的缓冲区计算的偏移量（以字节为单位）。 这是本地 PIN （PIN2），并且在操作需要本地 PIN 验证的情况下使用。 |
| 32 | 4 | LocalPinSize | 大小（0到16） | 密码的大小（以字节为单位）。 |
| 36 | 4 | BinaryDataOffset | 抵销 | 从该结构的开头计算的偏移量（以字节为单位），该偏移量为包含命令特定数据的缓冲区。 二进制数据仅用于设置操作。 |
| 40 | 4 | BinaryDataSize | 大小（0） | 数据的大小（以字节为单位）。 |
| 44 |   | DataBuffer | DATABUFFER | 包含 AppId、FilePath、LocalPin 和 BinaryData 的数据缓冲区。 |

### <a name="set"></a>设置

不适用。

### <a name="response"></a>响应

在 InformationBuffer 中使用以下 MBIM_UICC_RESPONSE 结构。

#### <a name="mbim_uicc_response-version-1"></a>MBIM_UICC_RESPONSE （版本1）

| 偏移量 | Size | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | 版本 | UINT32 | 接下来的 structurethat 版本号。 对于此结构的版本1，此字段必须为**1** 。 |
| 4 | 4 | StatusWord1 | UINT32 （0） | 特定于 UICC 命令的返回参数。 |
| 8 | 4 | StatusWord2 | UINT32 （0） | 特定于 UICC 命令的返回参数。 |
| 12 | 4 | ResponseDataOffset | 抵销 | 从该结构的开头计算的偏移量（以字节为单位），该偏移量为包含响应数据的缓冲区。 响应数据仅用于查询操作。 |
| 16 | 4 | ResponseDataSize | 大小（0） | 数据的大小（以字节为单位）。 |
| 20 |   | DataBuffer | DATABUFFER | 包含 ResponseData 的数据缓冲区。 |

### <a name="unsolicited-events"></a>未经请求的事件

不适用。

### <a name="status-codes"></a>状态代码

以下状态代码适用：

| 状态代码 | 描述 |
| --- | --- |
| MBIM_STATUS_BUSY | 为所有命令定义的基本 MBIM 状态。 |
| MBIM_STATUS_FAILURE | 为所有命令定义的基本 MBIM 状态。 |
| MBIM_STATUS_SIM_NOT_INSERTED | 无法执行 UICC 操作，因为缺少 UICC。 |
| MBIM_STATUS_BAD_SIM | 无法执行 UICC 操作，因为 UICC 处于错误状态。 |
| MBIM_STATUS_SHAREABILITY_CONDITION_ERROR | 无法选择此文件，因为它不可共享且当前正在被另一个应用程序访问。 SIM 返回的状态字为6985。 |
| MBIM_STATUS_PIN_FAILURE | 由于 PIN 错误，操作失败。 |

## <a name="mbim_cid_ms_uicc_access_record"></a>MBIM_CID_MS_UICC_ACCESS_RECORD

此 CID 发送特定命令来访问 UICC 线性固定或循环文件，结构类型为**MBIMUiccFileStructureCyclic**或**MBIMUIccFileStructureLinear**。

### <a name="parameters"></a>参数

|  | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| 命令 | 不适用 | MBIM_UICC_ACCESS_RECORD | 不适用 |
| 响应 | 不适用 | MBIM_UICC_RESPONSE | 不适用 |

### <a name="query"></a>查询

读取记录的内容。 MBIM_COMMAND_MSG 的 InformationBuffer 包含以下 MBIM_UICC_ACCESS_RECORD 结构。 MBIM_UICC_RESPONSE 在 MBIM_COMMAND_DONE 的 InformationBuffer 中返回。

#### <a name="mbim_uicc_access_record-version-1"></a>MBIM_UICC_ACCESS_RECORD （版本1）

| 偏移量 | Size | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | 版本 | UINT32 | 后面的结构的版本号。 对于此结构的版本1，此字段必须设置为**1** 。 |
| 4 | 4 | AppIdOffset | 抵销 | 从此结构开始到包含应用程序 ID 的缓冲区的偏移量（以字节为单位）。 |
| 8 | 4 | AppIdSize | 大小（0到16） | [ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)的8.3 节中定义的应用程序 ID 的大小（以字节为单位）。 对于2G 卡，此字段必须设置为零（0）。 |
| 12 | 4 | FilePathOffset | 抵销 | 从此结构开始到包含文件路径的缓冲区计算的偏移量（以字节为单位）。 文件路径是16位文件 Id 的数组。 第一个 ID 必须是**0x7FFF**或**0x3F00**。 如果第一个 ID 为**0x7FFF**，则该路径相对于**AppId**的应用程序 desginated 的 ADF。 否则，它是从 MF 开始的绝对路径。 |
| 16 | 4 | FilePathSize | 规格 | 文件路径的大小（以字节为单位）。 |
| 20 | 4 | RecordNumber | UINT32 （0） | 记录号。 这表示始终是绝对记录索引。 不支持相对记录访问，因为调制解调器可以对文件执行多个访问（接下来、上一个）。 |
| 24 | 4 | LocalPinOffset | 抵销 | 从此结构开始到包含密码的缓冲区计算的偏移量（以字节为单位）。 锁定密码是以 null 结尾的十进制数字的 UTF-8 字符串。 | 
| 28 | 4 | LocalPinSize | 大小（0到16） | 密码的大小（以字节为单位）。 |
| 32 | 4 | RecordDataOffset | 抵销 | 从该结构的开头计算的偏移量（以字节为单位），该偏移量为包含命令特定数据的缓冲区。 记录数据仅用于设置操作。 |
| 36 | 4 | RecordDataSize | 大小（0-256） | 数据的大小（以字节为单位）。 |
| 40 |   | DataBuffer | DATABUFFER | 包含 AppId、FilePath、LocalPin 和 RecordData 的数据缓冲区。 |

### <a name="set"></a>设置

不适用。

### <a name="response"></a>响应

MBIM_UICC_RESPONSE 结构在 InformationBuffer 中使用。

### <a name="unsolicited-events"></a>未经请求的事件

不适用。

### <a name="status-codes"></a>状态代码

以下状态代码适用：

| 状态代码 | 描述 |
| --- | --- |
| MBIM_STATUS_BUSY | 为所有命令定义的基本 MBIM 状态。 |
| MBIM_STATUS_FAILURE | 为所有命令定义的基本 MBIM 状态。 |
| MBIM_STATUS_SIM_NOT_INSERTED | 无法执行 UICC 操作，因为缺少 UICC。 |
| MBIM_STATUS_BAD_SIM | 无法执行 UICC 操作，因为 UICC 处于错误状态。 |
| MBIM_STATUS_SHAREABILITY_CONDITION_ERROR | 无法选择此文件，因为它不可共享且当前正在被另一个应用程序访问。 SIM 返回的状态字为6985。 |
| MBIM_STATUS_PIN_FAILURE | 由于 PIN 错误，操作失败。 |

## <a name="mbim_cid_ms_pin_ex"></a>MBIM_CID_MS_PIN_EX

此 CID 用于执行[ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)第9节中定义的所有 PIN 安全操作。 CID 类似于 MBIM_CID_MS_PIN，但扩展它以支持多应用 UICC 卡。 仅支持单一验证功能的 UICCs。 不支持支持多个应用程序 PIN 的多验证功能的 UICCs。 将一个应用程序 PIN （PIN1）分配给 UICC 上的所有 ADFs/DFs 和文件。 但是，每个应用程序都可以将本地 PIN （PIN2）指定为级别2用户验证要求，因此需要对每个访问命令进行其他验证。 这是 MBIM_CID_MS_PIN_EX 支持的方案。

与 MBIM_CID_MS_PIN 一样，在 MBIM_CID_MS_PIN_EX 中，设备一次只报告一个 PIN。 如果启用多个 Pin 并同时启用多个 Pin，则函数必须先报告 PIN1。 例如，如果启用了 subsidy 锁定报告并启用了 SIM 的 PIN1，则只有在成功验证 PIN1 后，才应在后续查询请求中报告 subsidy 锁定 PIN。 允许空 PIN 与 MBIMPinOperationEnter 一起使用。 通过将 PinSize 设置为零来指定空的 PIN。 在这种情况下，SET 命令类似于查询，并返回引用的 PIN 状态。 这与 "验证" 命令的行为完全一致，如 " [ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)" 的 "11.1.9" 部分中所指定。

### <a name="parameters"></a>参数

|  | 设置 | 查询 | 通知 |
| --- | --- | --- | --- |
| 命令 | MBIM_SET_PIN_EX | MBIM_PIN_APP | 不适用 |
| 响应 | MBIM_PIN_INFO_EX | MBIM_PIN_INFO_EX | 不适用 |

### <a name="query"></a>查询

在 InformationBuffer 中使用以下 MBIM_PIN_APP 结构。

#### <a name="mbim_pin_app-version-1"></a>MBIM_PIN_APP （版本1）

| 偏移量 | Size | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | 版本 | UINT32 | 后面的结构的版本号。 对于此结构的版本1，此字段必须设置为**1** 。 |
| 4 | 4 | AppIdOffset | 抵销 | 从此结构开始到包含应用程序 ID 的缓冲区的偏移量（以字节为单位）。 |
| 8 | 4 | AppIdSize | 大小（0到16） | [ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)的8.3 节中定义的应用程序 ID 的大小（以字节为单位）。 对于2G 卡，此字段必须设置为零（0）。 |
| 12 |   | DataBuffer | DATABUFFER | [ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)中定义的 AppId。 |

### <a name="set"></a>设置

在 InformationBuffer 中使用以下 MBIM_SET_PIN_EX 结构。

#### <a name="mbim_set_pin_ex"></a>MBIM_SET_PIN_EX

| 偏移量 | Size | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | PinType | MBIM_PIN_TYPE_EX | 固定类型。 请参阅本主题中的 MBIM_PIN_TYPE_EX 表。 |
| 4 | 4 | PinOperation | MBIM_PIN_OPERATION | PIN 运算。 请参阅 MBIM 1.0。 |
| 8 | 4 | PinOffset | 抵销 | 从该结构的开头算起的偏移量（以字节为单位），该偏移量是从该结构的开头到表示要用于执行操作的 PIN 值的字符串 PIN，或是启用或禁用 PIN 设置所需的 PIN 值。 此字段适用于**PinOperation**的所有值。 |
| 12 | 4 | PinSize | 大小（0-32） | 用于 PIN 的大小（以字节为单位）。 |
| 16 | 4 | NewPinOffset | 抵销 | 从该结构的开头计算的偏移量（以字节为单位），该偏移量为**NewPin**字符串，表示在**PinOperation**为 MBIMPinOperationChange 或 MBIMPinOperationEnter 时要设置的新 PIN 值，用于 PinTypeMBIMPinTypePuk1 或PinTypeMBIMPinTypePuk2. |
| 20 | 4 | NewPinSize | 大小（0-32） | 用于 NewPin 的大小（以字节为单位）。 |
| 24 | 4 | AppIdOffset | 抵销 | 从该结构的开头计算的偏移量（以字节为单位），该偏移量为包含应用程序 ID 的缓冲区。 |
| 28 | 4 | AppIdSize | 大小（0到16） | [ETSI TS 102 221 技术规范](https://go.microsoft.com/fwlink/p/?linkid=864594)的8.3 节中定义的应用程序 ID 的大小（以字节为单位）。 对于2G 卡，此字段必须设置为零（0）。 |
| 32 |   | DataBuffer | DATABUFFER | 包含 Pin、NewPin 和 AppId 的数据缓冲区。 |

### <a name="response"></a>响应

在 InformationBuffer 中使用以下 MBIM_PIN_INFO_EX 结构。

| 偏移量 | Size | 字段 | 在任务栏的搜索框中键入 | 描述 |
| --- | --- | --- | --- | --- |
| 0 | 4 | PinType | MBIM_PIN_TYPE_EX | 固定类型。 请参阅本主题中的 MBIM_PIN_TYPE_EX 表。 |
| 4 | 4 | PinState | MBIM_PIN_STATE | PIN 状态。 请参阅 MBIM 1.0。 |
| 8 | 4 | RemainingAttempts | UINT32 | 任何与 PIN 相关的操作的剩余尝试次数，如 enter、enable 或 disable。 不支持此信息的设备必须将此成员设置为0xFFFFFFFF。 |

### <a name="unsolicited-events"></a>未经请求的事件

不适用。

### <a name="status-codes"></a>状态代码

以下状态代码适用：

| 状态代码 | 描述 |
| --- | --- |
| MBIM_STATUS_BUSY | 为所有命令定义的基本 MBIM 状态。 |
| MBIM_STATUS_FAILURE | 为所有命令定义的基本 MBIM 状态。 |
| MBIM_STATUS_SIM_NOT_INSERTED | 无法执行 UICC 操作，因为缺少 UICC。 |
| MBIM_STATUS_BAD_SIM | 无法执行 UICC 操作，因为 UICC 处于错误状态。 |
| MBIM_STATUS_PIN_DISABLED | 由于 PIN 已禁用，操作失败。 |
| MBIM_STATUS_PIN_REQUIRED | 操作失败，因为必须输入 PIN 才能继续。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | 操作失败，因为设备不支持对相应的 PIN 类型设置设置。 |
