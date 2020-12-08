---
title: MagneticStripeReaderErrorOccured
description: 当磁条读取器 (MSR) 错误（如扫描错误）时，将发生 MagneticStripeReaderErrorOccured 事件。
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 38ad55255460643e643c4ec2214564a87e4a7adf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794311"
---
# <a name="magneticstripereadererroroccured"></a>MagneticStripeReaderErrorOccured

当磁条读取器 (MSR) 错误（如扫描错误）时发生此事件。

## <a name="syntax"></a>语法

```cpp
typedef struct _MSR_ERROR_EVENT
{
    PosEventDataHeader Header;
    MsrTrackErrorType Track1Status;
    MsrTrackErrorType Track2Status;
    MsrTrackErrorType Track3Status;
    MsrTrackErrorType Track4Status;
    UnifiedPosErrorSeverity Severity;
    UnifiedPosErrorReason Reason;
    UINT32 ExtendedReason;
    MSR_DATA_RECEIVED CardData;
    wchar_t Message[MSR_ERROR_MAX_MESSAGE_LENGTH];
} MSR_ERROR_EVENT, *PMSR_ERROR_EVENT;
```

下表显示此事件的数据缓冲区的内存布局。

| 内存值                                                                   | 描述                                                                                                                               |
|--------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| 0x00000009                                                          | **事件 = PosEventType：： MagneticStripeReaderErrorOccurred**                                                               |
| UINT32                                                              | **DataLength** = Sizeof (**PosEventDataHeader**) + sizeof (**MSR \_ 错误 \_ 事件**)                                                 |
| 32位 [MsrTrackErrorType](/windows-hardware/drivers/ddi/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrtrackerrortype)                   | **Track1Status**                                                                                                               |
| 32位 [MsrTrackErrorType](/windows-hardware/drivers/ddi/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrtrackerrortype)                   | **Track2Status**                                                                                                               |
| 32位 [MsrTrackErrorType](/windows-hardware/drivers/ddi/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrtrackerrortype)                   | **Track3Status**                                                                                                               |
| 32位 [MsrTrackErrorType](/windows-hardware/drivers/ddi/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrtrackerrortype)                   | **Track4Status**                                                                                                               |
| 32位 [UnifiedPosErrorSeverity](/windows-hardware/drivers/ddi/pointofservicecommontypes/ne-pointofservicecommontypes-driverunifiedposerrorseverity)       | **严重性**                                                                                                                   |
| 32位 [UnifiedPosErrorReason](/windows-hardware/drivers/ddi/pointofservicecommontypes/ne-pointofservicecommontypes-driverunifiedposerrorreason)           | **原因**                                                                                                                     |
| UINT32                                                              | **扩展原因**                                                                                                            |
| 32位 [MsrCardType](/windows-hardware/drivers/ddi/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrcardtype)                               | **CardType**                                                                                                                   |
| unsigned char                                                       | **Track1EncryptedDataLength**                                                                                                  |
| unsigned char                                                       | **Track2EncryptedDataLength**                                                                                                  |
| unsigned char                                                       | **Track3EncryptedDataLength**                                                                                                  |
| unsigned char                                                       | **Track4EncryptedDataLength**                                                                                                  |
| 无符号字符 \[ MSR \_ 跟踪 \_ 大小\]                                  | 加密磁道1数据的 **Track1EncryptedDataLength** 字节                                                                  |
| 无符号字符 \[ MSR \_ 跟踪 \_ 大小\]                                  | 加密磁道2数据的 **Track2EncryptedDataLength** 字节                                                                  |
| 无符号字符 \[ MSR \_ 跟踪 \_ 大小\]                                  | 加密磁道3数据的 **Track3EncryptedDataLength** 字节                                                                  |
| 无符号字符 \[ MSR \_ 跟踪 \_ 大小\]                                  | 加密磁道4数据的 **Track4EncryptedDataLength** 字节                                                                  |
| unsigned char                                                       | **Track1MaskedDataLength**                                                                                                     |
| unsigned char                                                       | **Track2MaskedDataLength**                                                                                                     |
| unsigned char                                                       | **Track3MaskedDataLength**                                                                                                     |
| unsigned char                                                       | **Track4MaskedDataLength**                                                                                                     |
| 无符号字符 \[ MSR \_ 跟踪 \_ 大小\]                                  | 屏蔽轨迹1数据的 **Track1MaskedDataLength** 字节数                                                                        |
| 无符号字符 \[ MSR \_ 跟踪 \_ 大小\]                                  | **Track2MaskedDataLength** bytes of 遮掩 track 2 数据                                                                        |
| 无符号字符 \[ MSR \_ 跟踪 \_ 大小\]                                  | **Track3MaskedDataLength** bytes of 遮掩 track 3 数据                                                                        |
| 无符号字符 \[ MSR \_ 跟踪 \_ 大小\]                                  | **Track4MaskedDataLength** bytes of 遮掩 track 4 数据                                                                        |
| unsigned char                                                       | **Track1DiscretionaryDataLength**                                                                                              |
| unsigned char                                                       | **Track2DiscretionaryDataLength**                                                                                              |
| 无符号字符 \[ MSR \_ 跟踪 \_ 大小\]                                  | 任意磁道1数据的 **Track1DiscretionaryDataLength** 字节数                                                          |
| 无符号字符 \[ MSR \_ 跟踪 \_ 大小\]                                  | 随机跟踪2数据的 **Track2DiscretionaryDataLength** 字节数                                                          |
| unsigned char                                                       | **CardAuthenicationDataLength** -加密后的数据长度，包括填充                                       |
| unsigned char                                                       | **CardAuthenticationDataAbsoluteLength** -在加密过程中，可能需要 (数据的长度才能在解密过程中去除填充)  |
| 无符号字符 \[ MSR \_ 附加的 \_ 安全 \_ 信息 \_ 数据 \_ 大小\] | 卡身份验证数据的 **CardAuthenticationDataAbsoluteLength** 字节数                                                     |
| unsigned char                                                       | **AdditionalSecurityInformationLength**                                                                                        |
| 无符号字符 \[ MSR \_ 附加的 \_ 安全 \_ 信息 \_ 大小\]       | 额外安全信息的 **AdditionalSecurityInformationLength** 字节数                                               |
| wchar \_ T \[ MSR \_ 错误 \_ 最大 \_ 消息 \_ 长度\]                       | 最多 **MSR \_ 错误 \_ 最大 \_ 消息 \_ 长度** wchar \_ t of 错误 **Null** 终止消息文本                                  |


## <a name="remarks"></a>备注

如果发生扫描错误，并且获取了某些扫描数据，则事件数据将包含部分扫描数据。

## <a name="requirements"></a>要求

**标头：** pointofservicedriverinterface
