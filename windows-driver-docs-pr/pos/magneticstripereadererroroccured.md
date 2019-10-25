---
title: MagneticStripeReaderErrorOccured
description: 出现磁条读取器（MSR）错误（如扫描错误）时，将发生 MagneticStripeReaderErrorOccured 事件。
ms.assetid: c2402411-1bbf-44c1-bf7f-813f6d967822
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2db6d8d03132912d7804c31af70d7ffc90c24a8c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843128"
---
# <a name="magneticstripereadererroroccured"></a>MagneticStripeReaderErrorOccured

出现磁条读取器（MSR）错误（如扫描错误）时，将发生此事件。

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
| UINT32                                                              | **DataLength** = Sizeof （**PosEventDataHeader**） + SIZEOF （**MSR\_错误\_事件**）                                                |
| 32位[MsrTrackErrorType](https://docs.microsoft.com/windows-hardware/drivers/ddi/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrtrackerrortype)                   | **Track1Status**                                                                                                               |
| 32位[MsrTrackErrorType](https://docs.microsoft.com/windows-hardware/drivers/ddi/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrtrackerrortype)                   | **Track2Status**                                                                                                               |
| 32位[MsrTrackErrorType](https://docs.microsoft.com/windows-hardware/drivers/ddi/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrtrackerrortype)                   | **Track3Status**                                                                                                               |
| 32位[MsrTrackErrorType](https://docs.microsoft.com/windows-hardware/drivers/ddi/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrtrackerrortype)                   | **Track4Status**                                                                                                               |
| 32位[UnifiedPosErrorSeverity](https://docs.microsoft.com/windows-hardware/drivers/ddi/pointofservicecommontypes/ne-pointofservicecommontypes-driverunifiedposerrorseverity)       | **对应**                                                                                                                   |
| 32位[UnifiedPosErrorReason](https://docs.microsoft.com/windows-hardware/drivers/ddi/pointofservicecommontypes/ne-pointofservicecommontypes-driverunifiedposerrorreason)           | **在于**                                                                                                                     |
| UINT32                                                              | **扩展原因**                                                                                                            |
| 32位[MsrCardType](https://docs.microsoft.com/windows-hardware/drivers/ddi/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrcardtype)                               | **CardType**                                                                                                                   |
| 无符号字符型                                                       | **Track1EncryptedDataLength**                                                                                                  |
| 无符号字符型                                                       | **Track2EncryptedDataLength**                                                                                                  |
| 无符号字符型                                                       | **Track3EncryptedDataLength**                                                                                                  |
| 无符号字符型                                                       | **Track4EncryptedDataLength**                                                                                                  |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | 加密磁道1数据的**Track1EncryptedDataLength**字节                                                                  |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | 加密磁道2数据的**Track2EncryptedDataLength**字节                                                                  |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | 加密磁道3数据的**Track3EncryptedDataLength**字节                                                                  |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | 加密磁道4数据的**Track4EncryptedDataLength**字节                                                                  |
| 无符号字符型                                                       | **Track1MaskedDataLength**                                                                                                     |
| 无符号字符型                                                       | **Track2MaskedDataLength**                                                                                                     |
| 无符号字符型                                                       | **Track3MaskedDataLength**                                                                                                     |
| 无符号字符型                                                       | **Track4MaskedDataLength**                                                                                                     |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | 屏蔽轨迹1数据的**Track1MaskedDataLength**字节数                                                                        |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | **Track2MaskedDataLength** bytes of 遮掩 track 2 数据                                                                        |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | **Track3MaskedDataLength** bytes of 遮掩 track 3 数据                                                                        |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | **Track4MaskedDataLength** bytes of 遮掩 track 4 数据                                                                        |
| 无符号字符型                                                       | **Track1DiscretionaryDataLength**                                                                                              |
| 无符号字符型                                                       | **Track2DiscretionaryDataLength**                                                                                              |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | 任意磁道1数据的**Track1DiscretionaryDataLength**字节数                                                          |
| 无符号 char \[MSR\_跟踪\_大小\]                                  | 随机跟踪2数据的**Track2DiscretionaryDataLength**字节数                                                          |
| 无符号字符型                                                       | **CardAuthenicationDataLength** -加密后的数据长度，包括填充                                       |
| 无符号字符型                                                       | **CardAuthenticationDataAbsoluteLength** -加密之前的数据长度（可能需要在解密过程中去除填充） |
| 无符号 char\[MSR\_其他\_安全\_信息\_数据\_大小\] | 卡身份验证数据的**CardAuthenticationDataAbsoluteLength**字节数                                                     |
| 无符号字符型                                                       | **AdditionalSecurityInformationLength**                                                                                        |
| 无符号 char\[MSR\_额外\_安全\_信息\_大小\]       | 额外安全信息的**AdditionalSecurityInformationLength**字节数                                               |
| wchar\_T \[MSR\_错误\_最大\_消息\_长度\]                       | 最多**MSR\_错误\_最大\_消息\_长度**wchar\_错误**Null**终止消息文本的 t                                  |


## <a name="remarks"></a>备注

如果发生扫描错误，并且获取了某些扫描数据，则事件数据将包含部分扫描数据。

## <a name="requirements"></a>要求

**标头：** pointofservicedriverinterface
