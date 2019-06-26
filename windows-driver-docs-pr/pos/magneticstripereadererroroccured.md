---
title: MagneticStripeReaderErrorOccured
description: 磁条阅读器 (MSR) 错误，例如扫描错误时，将发生 MagneticStripeReaderErrorOccured 事件。
ms.assetid: c2402411-1bbf-44c1-bf7f-813f6d967822
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: a8bafd029ac4bdbabc63cecc5dbe56559e3afddf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363374"
---
# <a name="magneticstripereadererroroccured"></a>MagneticStripeReaderErrorOccured

磁条阅读器 (MSR) 错误，例如扫描错误时，会发生此事件。

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

下表显示了此事件的数据缓冲区的内存布局。

| 内存值                                                                   | 描述                                                                                                                               |
|--------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| 0x00000009                                                          | **事件类型 = PosEventType::MagneticStripeReaderErrorOccurred**                                                               |
| UINT32                                                              | **DataLength** = sizeof(**PosEventDataHeader**) + sizeof(**MSR\_ERROR\_EVENT**)                                                |
| 32 位[MsrTrackErrorType](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrtrackerrortype)                   | **Track1Status**                                                                                                               |
| 32 位[MsrTrackErrorType](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrtrackerrortype)                   | **Track2Status**                                                                                                               |
| 32 位[MsrTrackErrorType](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrtrackerrortype)                   | **Track3Status**                                                                                                               |
| 32 位[MsrTrackErrorType](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrtrackerrortype)                   | **Track4Status**                                                                                                               |
| 32 位[UnifiedPosErrorSeverity](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pointofservicecommontypes/ne-pointofservicecommontypes-driverunifiedposerrorseverity)       | **Severity**                                                                                                                   |
| 32 位[UnifiedPosErrorReason](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pointofservicecommontypes/ne-pointofservicecommontypes-driverunifiedposerrorreason)           | **Reason**                                                                                                                     |
| UINT32                                                              | **扩展的原因**                                                                                                            |
| 32 位[MsrCardType](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrcardtype)                               | **CardType**                                                                                                                   |
| 无符号字符型                                                       | **Track1EncryptedDataLength**                                                                                                  |
| 无符号字符型                                                       | **Track2EncryptedDataLength**                                                                                                  |
| 无符号字符型                                                       | **Track3EncryptedDataLength**                                                                                                  |
| 无符号字符型                                                       | **Track4EncryptedDataLength**                                                                                                  |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | **Track1EncryptedDataLength**加密的跟踪 1 数据的字节                                                                  |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | **Track2EncryptedDataLength**加密的跟踪 2 数据的字节                                                                  |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | **Track3EncryptedDataLength**加密的跟踪 3 数据的字节                                                                  |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | **Track4EncryptedDataLength**加密的跟踪 4 数据的字节                                                                  |
| 无符号字符型                                                       | **Track1MaskedDataLength**                                                                                                     |
| 无符号字符型                                                       | **Track2MaskedDataLength**                                                                                                     |
| 无符号字符型                                                       | **Track3MaskedDataLength**                                                                                                     |
| 无符号字符型                                                       | **Track4MaskedDataLength**                                                                                                     |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | **Track1MaskedDataLength**字节的掩码跟踪 1 个数据                                                                        |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | **Track2MaskedDataLength**字节的掩码跟踪 2 数据                                                                        |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | **Track3MaskedDataLength**字节的掩码跟踪 3 个数据                                                                        |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | **Track4MaskedDataLength**字节的掩码跟踪 4 数据                                                                        |
| 无符号字符型                                                       | **Track1DiscretionaryDataLength**                                                                                              |
| 无符号字符型                                                       | **Track2DiscretionaryDataLength**                                                                                              |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | **Track1DiscretionaryDataLength**字节的自定义跟踪 1 个数据                                                          |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | **Track2DiscretionaryDataLength**字节的自定义跟踪 2 数据                                                          |
| 无符号字符型                                                       | **CardAuthenicationDataLength** -加密，包括填充后的数据的长度                                       |
| 无符号字符型                                                       | **CardAuthenticationDataAbsoluteLength** -加密 （可能需要去除解密期间填充） 之前的数据的长度 |
| 无符号 char\[MSR\_其他\_安全\_信息\_数据\_大小\] | **CardAuthenticationDataAbsoluteLength**卡身份验证数据的字节数                                                     |
| 无符号字符型                                                       | **AdditionalSecurityInformationLength**                                                                                        |
| 无符号 char\[MSR\_其他\_安全\_信息\_大小\]       | **AdditionalSecurityInformationLength**字节的额外的安全信息                                               |
| wchar\_T \[MSR\_ERROR\_MAX\_MESSAGE\_LENGTH\]                       | 最多**MSR\_错误\_最大\_消息\_长度**wchar\_t 错误**Null**-终止消息文本                                  |


## <a name="remarks"></a>备注

如果扫描出错，并获取一些扫描数据，事件数据包含部分扫描数据。

## <a name="requirements"></a>要求

**标头：** pointofservicedriverinterface.h
